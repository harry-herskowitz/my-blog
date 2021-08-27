---
layout: post
title: Where Video Meets Code
date: 2020-02-26
categories: [Electron, Javascript]
image: 'perennial.jpg'
author: 'Harry Herskowitz'
author_blurb: 'Harry is a web developer and videographer with a focus on using technology to empower local artists and communities'
author_link: 'https://github.com/roldyclark'
avatar: 'roldy.png'
---

<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/214118670?h=bc60f79d0f&title=0&byline=0&portrait=0" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

I started college as a Cinema major. I've been making films since I was 10 years old, so I was excited to go to film school and learn the industry. However, after taking a computer science course, I found myself just as excited about coding. As a technical person it came easy to me. I decided to create an interdisciplinary major that encompassed both film making and coding. With the internet becoming the most popular medium for video, I saw new possibilities in the intersection of film and code.

The most obvious intersection is in Web Design. Websites can display video in a customized layout of textual and visual content. My music blog Tapedrop.com is an example of this. But in the last year of my studies, I wanted to go further. So I asked the question: How can code be used to program the content of the video itself?

That's when I created [Perennial](https://github.com/roldyclark/Perennial). Perennial is a Mac application for making Variable Audio Movies. I came up with the idea after watching The Neverending Story. It's a great movie, but it had one problem - it ended! I began thinking about what an actual neverending movie would look like. It could just be a story that loops perfectly, maybe by involving time travel or parallel dimensions. This would be cool and all, but it would just be the same movie again.

I wanted to write code that took individual scenes and added variables, in this case the audio, making each rewatch entirely unique. Thanks to permutation math, just a small amount of variables could result in a massive amount of unique combinations. If done right, a filmmaker could make a film with a seemingly neverending timeline.

For my example I made a film about a guy waking up everyday and doing various things around his apartment. With each loop he listened to a different radio station, played a different song on his piano, and read a different letter he'd received in the mail. These variables gave the illusion that he was actually living in the computer screen, going through variations of his daily routine forever.

I coded the program in JavaScript because I originally wanted it to be a web app. I soon realized that I couldn't afford to have users upload their videos to my server, and that web apps can't reference a users local files for obvious security reasons. Luckily Electron makes converting a web app to desktop easy. The Perennial app is available to all Mac users [here](https://github.com/roldyclark/Perennial/releases/tag/v1.0). Download it to start making variable audio movies today! I would love to see this technology be used to its full potential.
