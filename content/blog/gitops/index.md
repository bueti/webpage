---
title: GitOps Without Git
date: 2025-07-07
summary: What if we don't use Git to manage which version of a service is deployed in GitOps?
tags: ["blog", "devops", "gitops"]
hideLastModified: true
---

> **Disclaimer**: All thoughts and opinions shared here are my own and don't represent my employer's views or positions.

When I first encountered GitOps, I was immediately drawn to its philosophy. It seemed like the natural evolution from the DevOps automation tools we were using at the time — Ansible, Puppet, and their contemporaries. The promise of automatic reconciliation, with the traceability of Git seemed the ideal match.

But as I began implementing GitOps in practice, two fundamental challenges emerged that made me question whether the conventional approach was truly optimal.

## The Two Core Problems with Traditional GitOps

### The Configuration-Code Divide

Traditional GitOps often separates application code from its configuration, storing them in different repositories. While this separation can be bridged by colocating everything in a single repository, this approach becomes unwieldy when managing dozens or hundreds of services across multiple teams.

### The Multi-Commit Release Problem

Usually GitOps is used in Kubernetes environments. When you want to deploy a version of your service, you simply update the image tag. There are different ways how to tag images but I think the most common ones are to use a version tag (e.g. v1.0.0) or the short commit SHA ID.

Since GitOps requires the deployed image tag to be committed to Git, we encounter a classic chicken-and-egg problem:

Imagine we want to use the short commit SHA as our image tag. The typical flow looks like this:

- We merge a PR to the main branch
- The CI system builds a Docker image tagged with the commit SHA
- We need that SHA to update our deployment configuration
- This requires a second commit, separate from our original code change

The conventional solution involves creating an automated pipeline that triggers after the build completes, retrieves the new tag, updates the configuration, and commits the change back to the repository. However, this approach introduces several risks:

- Automated commits can create merge conflicts
- Pipeline failures can leave deployments in inconsistent states
- The complexity of managing automated Git operations grows over time

I would also argue that this pollutes the Git history with meaningless "Bump Tag" commits.

## Existing Solutions Fall Short

Tools like ArgoCD Image Updater attempt to solve this problem, but they're tightly coupled to specific GitOps platforms. If you prefer simpler alternatives to ArgoCD's complexity, you're out of luck.

Flux offers a similar solution, but it still requires automated commits to your repository—inheriting all the same problems we're trying to avoid.

## Questioning the Git Requirement

This led me to revisit the fundamental principles of GitOps. According to the [OpenGitOps](https://opengitops.dev/) specification, GitOps is built on four core principles:

1. **Declarative**: System desired state must be expressed declaratively
2. **Versioned and Immutable**: Desired state is stored with immutability, versioning, and complete history
3. **Pulled Automatically**: Software agents automatically pull desired state declarations
4. **Continuously Reconciled**: Agents continuously observe and apply desired state

Notice something interesting? Git isn't mentioned once in these principles.

Moreover, I'd say that principles 3 and 4 are implementation details rather than core requirements. Whether you push changes or pull them doesn't fundamentally alter the operational model. Similarly, continuous reconciliation makes sense in some environments but may be overkill in others (ever tried to quickly update a Kubernetes object during an incident, only to have ArgoCD immediately revert it?).

## A New Path Forward

When we free ourselves from Git-centric constraints, we can design a deployment system that addresses our core requirements:

- **No commits for version updates**: Eliminate the need to create repository commits just to update deployed version tags
- **Automatic latest deployments**: Provide a convenient way to automatically deploy the latest version -- whether that's a short SHA commit ID, a version tag, or even `latest`.
- **Flexible deployment triggers**: Enable both manual and automated deployment triggers as needed

### Implementation with Helmfile

I’m convinced that for many environments ArgoCD et al are an overkill and introduce needless complexity.

Therefore, we'll use Helmfile to manage all charts deployed on each cluster through cluster-specific `helmfile.yaml` files. The key is introducing a new Helmfile label: `deployment: [auto|manual]`.

- **Auto Mode**: The deployment pipeline deploys whatever tag is specified in the values file on merge. Perfect for services that should automatically track the latest stable version.
- **Manual Mode**: Helmfile explicitly sets the `image.tag` and deploys the requested version. Ideal for production services that require explicit promotion.

This simple distinction enables powerful CI/CD workflows. For example, to enable PR-based deployments on staging environments, we can trigger a deployment with a simple PR comment like `/deploy my-release cluster=staging`. This would build and deploy `my-release` using the current SHA on the staging cluster.

The same workflow can be triggered manually for version promotions, giving teams full control over when and what gets deployed.

### The Complete Vision

While the Helmfile approach covers our base requirements, a production-ready solution might include:

- **Infrastructure API**: A dedicated API endpoint for triggering deployments programmatically
- **Developer Interface**: A web UI built on top of the API, providing an intuitive interface for developers to manage their deployments
- **CI/CD Integration**: Seamless interaction between the API and existing CI/CD systems
- **History Datastore:** A dedicated datastore that tracks which versions of a service have been deployed by whom. Useful for when the history by the CI/CD system isn’t enough

This approach maintains the declarative benefits of GitOps while eliminating the operational friction that makes traditional implementations cumbersome. Most importantly, it puts deployment control back in the hands of developers without forcing them into Git-based workflows that create more complexity than value.

# Acknowledging the Trade-offs

While this approach solves significant problems with traditional GitOps, it's important to recognize that we're making trade-offs rather than finding a universally superior solution.

## Where This Approach Excels

- **Small to medium teams** that can move quickly without extensive approval processes
- **Rapid iteration environments** where deployment velocity is prioritized over governance overhead
- **Organizations that value developer autonomy** and want to minimize operational friction
- **Teams comfortable with custom tooling** and willing to invest in building and maintaining deployment infrastructure

## Where Traditional GitOps May Be Better

- **Highly regulated industries** requiring extensive audit trails
- **Large organizations** with complex approval workflows and multiple stakeholders who need visibility into deployment decisions
- **Teams with limited operational capacity** who prefer leveraging existing GitOps ecosystems over building custom solutions
- **Environments requiring strict change control** where every deployment decision needs documented rationale and approval

## Key Considerations

- You're trading Git's distributed, auditable history for deployment flexibility. This is powerful for rapid iteration but may complicate compliance requirements
- Custom infrastructure requires ongoing maintenance and specialized knowledge, whereas GitOps tooling has established communities and support
- You need to invest more heavily in your History Datastore and deployment API to match the governance capabilities that Git provides out of the box, though this can enable more flexible rollback scenarios than Git-based approaches

The goal isn't to replace GitOps universally, but to provide a better path for teams where traditional GitOps creates more friction than value. For organizations that have already invested heavily in GitOps tooling and processes, the switching cost may outweigh the benefits. However, for teams starting fresh or those frustrated by GitOps complexity, this approach offers a compelling alternative that maintains the core benefits while reducing operational overhead.
