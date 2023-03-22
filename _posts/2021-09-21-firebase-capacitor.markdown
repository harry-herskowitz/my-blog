---
layout: post
title: 'Firebase Auth with Capacitor 3'
date: 2021-08-23
image: 'firebase.jpg'
image-alt: 'Firebase logo'
---

I recently built my first native iOS app with Svelte, Capacitor, and Firebase (coming soon!). The stack is a breeze to work with, but I ran into a snag getting Firebase to work in the iOS builds. Non of the firebase calls were returning. Luckily, a friendly redditor pointed out the problem: Firebase auth needs to be initialized manually on iOS, or else signInWithPopUp and signInWithRedirect will hold things up - even when using a capacitor plugin that authorizes natively like [capacitor-firebase-authentication](https://github.com/robingenz/capacitor-firebase-authentication). So here's my code to manually authorize on iOS:

```js
function whichAuth() {
  let auth
  if (Capacitor.isNativePlatform()) {
    auth = initializeAuth(app, {
      persistence: indexedDBLocalPersistence
    })
  } else {
    auth = getAuth()
  }
  return auth
}

export const auth = whichAuth()
```

With this code, my app is working flawlessly - and development has been a joy!
