---
layout: post
title: 'Geolocation for Creative Collaboration'
date: 2020-09-04
image: 'closecreate2.jpeg'
image-alt: 'Screenshot of the Closecreate web app'
---

![closecreate screenshot]({{ site.baseurl }}/assets/images/posts/closecreate1.jpeg)

Today I am happy to release [Closecreate](https://github.com/harry-herskowitz/closecreate), an open source web app for bringing together creative collaborators. The app allows users to create a profile which includes a picture, location, bio, and social media links to showcase their work. They can then scroll through nearby profiles to match with in a tinder-like fashion. Once two users match they can instant message each other and discuss future collaborations.

![closecreate screenshot]({{ site.baseurl }}/assets/images/posts/closecreate2.jpeg)

The application is built with [React](https://reactjs.org/) on the client side, [Express](https://expressjs.com/) ([Node](https://nodejs.org/en/about/)) on the server side, and a [MongoDB](https://www.mongodb.com/) database - also known as the [MERN Stack](https://www.mongodb.com/mern-stack). Images are uploaded and served through [AWS S3](https://aws.amazon.com/s3/). Each user's current location is obtained at login through the [Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API) and profiles within 30km are displayed. The app is styled with [Halfmoon](https://www.gethalfmoon.com/docs/introduction/), a bootstrap alternative with built-in darkmode. [Socket.io](https://socket.io/) is used in the chat component for realtime messaging.

![closecreate screenshot]({{ site.baseurl }}/assets/images/posts/closecreate3.jpeg)

I am currently hosting the app live on Heroku at [closecreate.com](https://www.closecreate.com). I'd love to see the creative community get use out of it! I also hope the open source repo is taken advantage of as this code can be reused to create all kinds of interesting matchmaking apps.

UPDATE: I am no longer hosting this app, but the code will stay a available on my [Github](https://github.com/harry-herskowitz/closecreate). I am currently working on an updated concept for Closecreate. Stay tuned.
