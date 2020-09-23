---
title: Phoenix Project
hideLastModified: true
summaryImage: "phoenix_summary.jpg"
summary: "In DevOps, we typically define our technology value stream as the process required to convert a business hypothesis into a technology-enabled service that delivers value to the customer."
tags: [ "books", "devops"]
---


## The Technology Value Stream

In DevOps, we typically define our technology value stream as the process required to convert a business hypothesis into a technology-enabled service that delivers value to the customer.

Because value is created only when our services are running in production, we must ensure that we are not only delivering fast flow, but that our deployments can also be performed without causing chaos and disruptions such as service outages, service impairments, or security or compliance failures.

## The Three Ways

The Three Ways describe the values and philosophies that frame the processes, procedures, practices of DevOps, as well as the prescriptive steps.

![The Three Ways](/images/threeways.png)

### The Principles of Flow

> The Principles of Flow, which accelerate the delivery of work from Development to Operations to our customers

The First Way enables fast left-to-right flow of work from Development to Operations to the customer. In order to maximize flow, we need to make work visible, reduce our batch sizes and intervals of work, build in quality by preventing defects from being passed to downstream work centers, and constantly optimize for the global goals.

The outcomes of putting the First Way into practice include never passing a known defect to downstream work centers, never allowing local optimization to create global degradation, always seeking to increase flow, and always seeking to achieve profound understanding of the system (as per Deming).

### The Principles of Feedback

> The principles of Feedback, which enable us to create ever safer systems of work

The Second Way enables the fast and constant flow of feedback from right to left at all stages of our value stream. It requires that we amplify feedback to prevent problems from happening again, or enable faster detection and recovery.

By doing this, we create quality at the source and generate or embed knowledge where it is needed - this allows us to create ever-safer systems of work where problems are found and fixed long before a catastrophic failure occurs.

### The Principles of Continual Learning and Experimentation

> The principles of Continual Learning and Experimentation, which foster a high-trust culture and a scientific approach to organizational improvement risk-taking as part of our daily work

The Third Way enables the creation of a generative, high-trust culture that supports a dynamic, disciplined, and scientific approach to experimentation and risk-taking, facilitating the creation of organizational learning, both from our successes and failures. Furthermore, by continually shortening and amplifying our feedback loops, we create ever-safer systems of work and are better able to take risks and perform experiments that help us learn faster than our competition and win in the marketplace.

As part of the Third Way, we also design our system of work so that we can multiply the effects of new knowledge, transforming local discoveries into global improvements. Regardless of where someone performs work, they do so with the cumulative and collective experience of everyone in the organization.

The outcomes of the Third Way include allocating time for the improvement of daily work, creating rituals that reward the team for taking risks, and introducing faults into the system to increase resilience.

## Continuous Delivery

In order for you to keep up with customer demand, which includes your upstream comrades in Development,you need to create what Humble and Farley called a deployment pipeline. That’s your entire value stream from code check-in to production. That’s not an art. That’s production. You need to get everything in version control. Everything. Not just the code, but everything required to build the environment. Then you need to automate the entire environment creation process. You need a deployment pipeline where you can create test and production environments, and then deploy code into them, entirely on-demand. That’s how you reduce your setup times and eliminate errors, so you can finally match whatever rate of change Development sets the tempo at.

## Reliability Engineering

* Resilience engineering tells us that we should routnely inject faults into the system, doing them frequently, to make them less painful.

> If it hurts, do it more often!

* To achieve a goal, a continual two-week improvement cycle is useful. Each cycle must follow the Plan-Do-Check-Act project, to keep them marching towards the goal.

> Get humans out of the deployment business.

## People

* To tell the truth is an act of love. To withhold the truth is an act of hate. Or worse, apathy.
* Ask youself, what differentiates a good day from a bad day for you?

## Memorable Quotes

* Any improvements made anywhere besides the bottleneck are an illusion
* Improving daily work is even more important than doing daily work.
* Mike Rother says that it almost doesn’t matter what you improve, as long as you’re improving something. Why? Because if you are not improving, entropy guarantees that you are actually getting worse, which ensures that there is no path to zero errors, zero work-related accidents, and zero loss.

## Further Reading

| Title | Topic |
|---------|-------|
| The Goal | ... |
| The Five Disfunctions of a Team | ... |
