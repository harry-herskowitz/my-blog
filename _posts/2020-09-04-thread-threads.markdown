---
layout: post
title: 'Archiving the Life of Secondhand Textiles'
date: 2020-09-04
image: 'threadthreadscover.jpg'
image-alt: "Screenshot of search form with prompt 'Enter code to access thread'"
---

![threadthreads screenshot]({{ site.baseurl }}/assets/images/posts/threadthreads.jpg)

Earlier this year I was approached by Abby Hollis, founder of the startup [Threads Threads](https://threadthreads.com/), to create a web application that archives the stories of secondhand clothing and textiles as they are passed on to new owners.

The app works like this: Each item has a tag sewn on with a alphanumeric code, which when entered into the site returns each owner's entry about the garment. The new owner now has a greater connection to the item and they can share their own stories before passing it along again.

As someone who loves thrifting, I was as excited about the idea as she was. I got on board with the project as the sole web developer.

Being a one man dev team, I had a lot of decisions to make. Since the site was a basic [CRUD](https://medium.com/@thorntonbrenden/whats-a-crud-app-e5a29cce03b5) application with no realtime features, I felt that using [React](https://reactjs.org/) would be overengineering. I made the decision to build with [Ruby On Rails](https://rubyonrails.org/) . Rails is a popular framework for building prototypes for startups because of its fast development and opinionated organization.

I was able to deploy the prototype after just two months of development. The app is fully functioning with users, threads, and an admin panel for managing data. The app can be accessed here: [https://threadthreads.herokuapp.com/](https://threadthreads.com/). Use example code **12345** to see how it works.

It had a great experience building this application and am excited for the future of Thread Threads. Follow them on [Instagram](https://www.instagram.com/mythreadthreads/) to keep up with their progress.
