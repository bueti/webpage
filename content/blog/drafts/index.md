---
title: Drafts? Drafts!
summaryImage: "drafts2.png"
keepImageRatio: true
summary: Store unfinished entries as drafts!
tags: [ "blog" ]
---

After writing a few entries on Gobbledygook I realized that a draft feature would be useful. I rarely have time to write a whole entry in one go, I also like to read it a bit later to spot typos and other inconsistencies. Luckily Rails makes it super easy to add columns to a database and adding a drafts feature was straight forward.

{{< figure src="drafts.png" width="812" >}}

In addition to that, every user can now see the entries created by themselves. This is also the place where drafts are visible, with a neat little `Draft`-badge.

{{< figure src="drafts2.png" width="350" >}}

But wait, there's more! You can also filter (and search) your posts in case you only want to see your drafts. It's not the prettiest implementation, but it works.

{{< figure src="drafts3.png" width="812" >}}
