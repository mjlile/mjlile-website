---
title: "Daily Dickie Videos"
date: 2023-06-24T16:23:40-04:00
type: "post"
description: "A website to share different videos of the beloved pomeranian, Dickie"
tags: [projects, aws]
---

Dickie, one of my parent's dog, was an adorable pomeranian (see below for evidence). I often got requests to send pictures of him when I would visit home. Unfortunately, that was only once in a while, so I stockpiled some videos of him. I was encouraged to make a website to share new videos of Dickie on a daily basis, loosely inspired by the Wordle craze.

The implementation is a bit wonky, but it works and it was fun to build. In short, there is an S3 bucket that contains 1. a static website and 2. a bunch of Dickie videos. Everyday at midnight Eastern Time, EventBridge triggers a Lambda which "rotates" the videos in the S3 bucket. It picks a new video (or the least recently used video), and marks that as the new target video. A "shared-on" metadata tag is added to track which video to pick next. The Lambda also invalidates the CloudFront cache so the new video is pushed to viewers.

Again, this isn't a great implementation. For one, you can't actually "move" S3 objects, or add metadata. The objects are destroyed and recreated with new metadata. Also, the web browser cache sometimes holds on to yesterday's video. But this was the first approach that came to mind, it works fine, and it's still in the AWS free tier, so that's all good in my book. The Lambda code is on [my GitHub](https://github.com/mjlile/daily-dickie-rotator).

You can check it out at https://dailydickie.mjlile.com. 

---

![Dickie with his Halloween bandana](dickie.jpg)