---
title: PromLens Helm Chart
summaryImage: "logo.png"
keepImageRatio: true
#summary: Abscence of Trust, Fear of Conflict, Lack of Commitment, Avoidance of Accountability & Inattention to Results.
tags: [ "blog", "helm"]
---

Constructing proper PromQL queries for you data is hard. One tool that helps a lot to understand the data that is available and to construct queries is [PromLens](https://promlens.com). If you don't know PromLens yet, I suggest to read [this blog post](https://promlabs.com/blog/2020/10/19/showcasing-promlens-0.10.0).

A few days ago we open-sourced the Helm Chart we use at Ricardo to deploy PromLens and we've made it available on [Artifacthub](https://artifacthub.io/packages/helm/ricardo/promlens). I hope this Chart will be as useful to you as it is to us.

{{< figure src="promlens.png" width="900" >}}
