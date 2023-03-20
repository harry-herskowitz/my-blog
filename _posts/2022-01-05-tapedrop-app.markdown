---
layout: post
title: 'Building an iOS app with Svelte, Capacitor and Firebase'
date: 2022-01-05
image: 'tapedrop-app.jpg'
---

![app screenshot](/assets/images/posts/tapedrop-app.jpg)

I had the idea for the [Tapedrop app](https://tapedrop.com/2022/01/01/tapedrop-app.html) years ago. At the time, I knew little more than basic HTML, CSS, and JS. Diving into native app development was daunting, and still is. Luckily, web technology has advanced to the point where making an iOS app is as simple as adding [Capacitor](https://capacitorjs.com/) to a web app. With [Svelte](https://svelte.dev/) as my frontend framework and [Firebase](https://firebase.google.com/) on the backend, building this app was a joy. In this post I will go over my experience with this stack.

I'd been eager to try [Svelte](https://svelte.dev/) since it offered reactivity, while keeping the simplicity of plain HTML and JS. I can't speak for Vue or Angular, but I have plenty of experience wrestling with React. JSX quickly becomes a tangled mess, and writing logic within a component is ugly and limited. Why can you only use ternary operators for inline conditions? Svelte's logic operators are fool proof and keep the HTML looking like HTML. Just take 5 minutes to go through the examples [here](https://svelte.dev/tutorial/if-blocks) and you will be a convert. The dealbreaker for me though is Svelte's built in [stores](https://svelte.dev/tutorial/writable-stores), which make state management simple. It's even more painful to use Redux or React Context at work now that I've seen the light.

On the backend I used [Firebase](https://firebase.google.com/) for authorization, data and image storage. Firebase cut my dev time in half. However, there were a few hangups. I had some issues with authorization in iOS, which I wrote about [here](http://harryherskowitz.com/2021/08/23/firebase-capacitor.html) and [here](https://github.com/firebase/firebase-js-sdk/issues/5553#event-5412439549). Also, geolocation was a challenge since queries are one dimensional. I used Geohashes to query nearby artists, along with latitude and longitude to filter out outliers. You can read more about this approach [here](https://firebase.google.com/docs/firestore/solutions/geoqueries).

Converting my web app for iOS with Capacitor was smooth, and didn't require me to build it in a specific framework like React Native or Ionic would have. With Capacitor, you simply call modules within plain JS that will run native functionality when available. For example, Capacitor's [Geolocation](https://capacitorjs.com/docs/apis/geolocation) module will use a device's GPS within a Native app, and use the [Geolocation Web API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API) within a browser.

Building the iOS app is done through a single CLI command. The difficult part is configuration. Apple requires a lot of configuration through Xcode and their developer program, and the documentation isn't great. It was also a headache to submit to the App Store, but their feedback was quick and concise. It took me only two attempts to get it approved, each review taking about 3 days.

This is the only iOS app I have made, so I don't have other tech stacks to compare it to. But, if you are looking for a framework-agnostic way to build a cross-platform app, I can highly recommend Capacitor. Firebase has its pains, but not having to code my own backend makes up for it - also it's free. So is the frontend, which I host on Github Pages. The only money going into this app is Apple's $100 developer fee.

So, for anyone hesitant to dive into the native app world, I hope this gives you the reassurance to go for it. You got this!
