---
title: Why Rails is Awesome
date: 2020-03-15
cover:
  image: "logo.png"
  relative: true
summary: Volunteering at iOverlander made me realize what a productivity enabler Rails is.
tags: ["blog", "rails"]
hideLastModified: true
---

I'm not a developer! Nevertheless, this doesn't stop me from trying to code things. It might not be pretty but it usually works ;-)

When we were traveling we've used an online service called [iOverlander](https://ioverlander.com) a lot. It was a super helpful tool for us and pretty much any other overlander we met.

> iOverlander is a mapping project started by overlanders Sam Christiansen of [Song of the Road](http://www.songoftheroad.com/) and Jessica Mans of [Life Remotely](http://www.liferemotely.com/). It began with the simple desire to combine many of the current overlander accommodation listings on the web.

While we were traveling I was helping out with reviewing new places and apply corrections reported by other overlanders. Once we were back and we've settled in I started to improve the technical side of things. The first order of business was to update the Rails version. iOverlander was built in 2014 by Sam on Rails 3.2. With his help I've updated it first to Rails 4.2 and than to Rails 5.2. While doing this, I've also dockerized the whole stack and automated the deployment.

Once the foundation was set, I've started to fix some of the old bugs and add new features. The first one was the ability to add places to favorites, something I've missed while travelling.

{{< figure src="favorites.png" width="830" >}}

Then I've restructured the profile page. Every user has now one central place where they can see and edit all the data about themselves.

{{< figure src="profile.png" width="830" >}}

A few weeks ago we introduced the option to report check-ins and images. Unfortunately, spammers don't spare the non-profit services. And today we've released another feature: Our users can now have an avatar picture.

{{< figure src="avatar.png" width="830" >}}

All the new features are part of a bigger change that will be introduced with the new and modern iOverlander app which we hopefully will be able to release soon.

---

You probably wonder, what has all of this to do with the title of the post?
As I said in the beginning, I am not a developer. But thanks to Rails even I can create these features.

- Thanks to [ActiveStorage](https://edgeguides.rubyonrails.org/active_storage_overview.html), adding avatars was a piece of cake.
- Making favorites searchable? An easy feat thanks to [Ransack](https://github.com/activerecord-hackery/ransack).
- Reducing the number of spam accounts be requiring email confirmation? Don't fret, [Devise](https://github.com/heartcombo/devise) has you covered.
- Implement hCaptcha? Again, there's a [Gem](https://github.com/CapSens/hcaptcha) available that will do the heavy lifting for you.
- You need to delete thousands of parent-child relations in your database (hello spammers...)? Luckily, [somebody](https://blog.getcensus.com/cascading-deletes-in-rails/) has already solved that for you too.

Rails might not be the most flashy technology but the productivity it enables even for amateurs is mind blowing. You don't have to solve the everything anew, you can focus on providing new features for your yours. In addition to that, it just works: Thousands of travellers are using our service, we have over 25'000 visitors per day, the Android app has been installed over 500'000 times. And all of that with a core development "team" of two to three people.

There's a lot of work to do, especially our current app is not up to the standards. We are working hard on a new one and if you are a React Native developer, we really could use your help! Send us an email to ioverlander.com@gmail.com.

So for now, enjoy this little teaser of the new app and safe travels!

{{< figure src="rn_app.png" width="375" >}}
