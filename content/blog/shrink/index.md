---
title: My Go-Based URL Shortener Project
summaryImage: "logo.png"
keepImageRatio: true
summary: Shrink.ch, a user-friendly Go-based URL shortener with features auto-generated and custom short URLs, QR-code generation, and visit tracking.
tags: [ "blog", "go"]
---

At work, I'm usually all about Go for CLI stuff and automation. After dabbling in Rails and creating a bunch of web apps, I figured it was time to try the web world with Go. The challenge? Building an URL shortener. And hey, since the [shrink.ch](https://shrink.ch) domain was up for grabs, why not give it a shot?

## What's Inside [shrink.ch](https://shrink.ch):

### 1. Features That Matter:
This little tool comes packed with some nifty features that make it more than just your average URL shortener.

- **User Registration with Email Verification:** Keep things secure with user registrations getting the email check before diving in.

- **Auto-Generated Short URLs:** When you just want a quick short URL, [shrink.ch](https://shrink.ch) whips one up for you on the spot.

- **Custom Path Short URLs:** Get creative and personalize your short URLs to fit your style or brand.

- **QR-Code Generation:** In a world filled with smartphones, QR codes make life easier. [shrink.ch](https://shrink.ch) makes them for your short URLs automatically.

- **Visit Counting:** Want to know how popular your links are? [shrink.ch](https://shrink.ch)'s got you covered with a visit count feature.

{{< figure src="page.png" width="1024" >}}

### 2. Tech Talk Made Simple:
Behind the scenes, [shrink.ch](https://shrink.ch) is running on a straightforward tech stack that gets the job done.

- **Frontend with Tailwind:** I'm no designer, but Tailwind made it easy to whip up a clean and functional frontend.

- **Go Templates:** Go isn't just for the backend. I used Go templates to build dynamic and efficient web pages.

- **Echo Web Framework and GORM:** Echo makes web development less of a headache, and GORM keeps things smooth when dealing with databases.

### 3. Deploying on a Budget:
Building [shrink.ch](https://shrink.ch) wasn't just about features; it was about doing it without breaking the bank. I opted for an OVH VPS because it's a steal at $1 per month. And to keep things simple, GitHub Actions handle the build and deployment.

### 4. Dive into the Code:
Curious about how it all works? The whole codebase is up on [GitHub](https://github.com/bueti/shrinkster). Feel free to check it out, maybe even lend a hand if you're up for it.
