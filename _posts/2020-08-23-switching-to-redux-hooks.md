---
layout: post
title: Switching to Redux Hooks
date: 2020-08-23
categories: [React, Javascript, NodeJS]
image: 'hooks.jpg'
author: 'Harry Herskowitz'
author_blurb: 'Harry is a web developer and programmer with a focus on using technology to empower local artists and communities'
author_link: 'https://github.com/roldyclark'
avatar: 'roldy.png'
---

React Hooks are great. They are clean, easy to read, and save time typing boilerplate. However, they are very new, and many popular tutorials have yet to fully adopt them - particularly in Redux. In this post I will be taking a component from Brad Traversy's [MERN Stack Front To Back](https://www.udemy.com/course/mern-stack-front-to-back) tutorial and converting it to use Redux hooks.

Below is the Posts component. We will be using hooks to access the state of `post` and to dispatch `getPosts` without `connect`.

```
import React, { Fragment, useEffect } from 'react'
import PropTypes from 'prop-types'
import { connect } from 'react-redux'
import PostItem from './PostItem'
import PostForm from './PostForm'
import { getPosts } from '../../actions/post'

const Posts = ({ getPosts, post: { posts } }) => {
  useEffect(() => {
    getPosts()
  }, [getPosts])

  return (
    <Fragment>
      <h1 className="large text-primary">Posts</h1>
      <p className="lead">
        <i className="fas fa-user" /> Welcome to the community
      </p>
      <PostForm />
      <div className="posts">
        {posts.map((post) => (
          <PostItem key={post._id} post={post} />
        ))}
      </div>
    </Fragment>
  )
}

Posts.propTypes = {
  getPosts: PropTypes.func.isRequired,
  post: PropTypes.object.isRequired
}

const mapStateToProps = (state) => ({
  post: state.post
})

export default connect(mapStateToProps, { getPosts })(Posts)

```

First, we can replace  `import { connect } from 'react-redux'` with `import { useSelector, useDispatch } from 'react-redux'`.

```
import React, { Fragment, useEffect } from 'react'
import PropTypes from 'prop-types'
import { useSelector, useDispatch } from 'react-redux'
import PostItem from './PostItem'
import PostForm from './PostForm'
import { getPosts } from '../../actions/post'

const Posts = ({ getPosts, post: { posts } }) => {
  useEffect(() => {
    getPosts()
  }, [getPosts])

  return (
    <Fragment>
      <h1 className="large text-primary">Posts</h1>
      <p className="lead">
        <i className="fas fa-user" /> Welcome to the community
      </p>
      <PostForm />
      <div className="posts">
        {posts.map((post) => (
          <PostItem key={post._id} post={post} />
        ))}
      </div>
    </Fragment>
  )
}

Posts.propTypes = {
  getPosts: PropTypes.func.isRequired,
  post: PropTypes.object.isRequired
}

const mapStateToProps = (state) => ({
  post: state.post
})

export default connect(mapStateToProps, { getPosts })(Posts)
```

Next, delete `connect(mapStateToprops, {getPosts})` and the `const mapStateToProps` block.

```
import React, { Fragment, useEffect } from 'react'
import PropTypes from 'prop-types'
import { useSelector, useDispatch } from 'react-redux'
import PostItem from './PostItem'
import PostForm from './PostForm'
import { getPosts } from '../../actions/post'

const Posts = ({ getPosts, post: { posts } }) => {
  useEffect(() => {
    getPosts()
  }, [getPosts])

  return (
    <Fragment>
      <h1 className="large text-primary">Posts</h1>
      <p className="lead">
        <i className="fas fa-user" /> Welcome to the community
      </p>
      <PostForm />
      <div className="posts">
        {posts.map((post) => (
          <PostItem key={post._id} post={post} />
        ))}
      </div>
    </Fragment>
  )
}

Posts.propTypes = {
  getPosts: PropTypes.func.isRequired,
  post: PropTypes.object.isRequired
}

export default Posts
```

Now we're ready for the hooks. First is the `useSelector` hook, which will get `posts` from `state.post`.

```
import React, { Fragment, useEffect } from 'react'
import PropTypes from 'prop-types'
import { useSelector, useDispatch } from 'react-redux'
import PostItem from './PostItem'
import PostForm from './PostForm'
import { getPosts } from '../../actions/post'

const Posts = ({ getPosts, post: { posts } }) => {

  const { posts } = useSelector(state => state.post)

  useEffect(() => {
    getPosts()
  }, [getPosts])

  return (
    <Fragment>
      <h1 className="large text-primary">Posts</h1>
      <p className="lead">
        <i className="fas fa-user" /> Welcome to the community
      </p>
      <PostForm />
      <div className="posts">
        {posts.map((post) => (
          <PostItem key={post._id} post={post} />
        ))}
      </div>
    </Fragment>
  )
}

Posts.propTypes = {
  getPosts: PropTypes.func.isRequired,
  post: PropTypes.object.isRequired
}

export default Posts
```

After this we will add the `useDispatch` hook, which will allow us to run our function `getPosts` by taking it as an argument like so: `dispatch(getPosts())`.

```
import React, { Fragment, useEffect } from 'react'
import PropTypes from 'prop-types'
import { useSelector, useDispatch } from 'react-redux'
import PostItem from './PostItem'
import PostForm from './PostForm'
import { getPosts } from '../../actions/post'

const Posts = ({ getPosts, post: { posts } }) => {

  const { posts } = useSelector(state => state.post)

  const dispatch = useDispatch()

  useEffect(() => {
    dispatch(getPosts())
  }, [getPosts])

  return (
    <Fragment>
      <h1 className="large text-primary">Posts</h1>
      <p className="lead">
        <i className="fas fa-user" /> Welcome to the community
      </p>
      <PostForm />
      <div className="posts">
        {posts.map((post) => (
          <PostItem key={post._id} post={post} />
        ))}
      </div>
    </Fragment>
  )
}

Posts.propTypes = {
  getPosts: PropTypes.func.isRequired,
  post: PropTypes.object.isRequired
}

export default Posts
```

You can now remove the props from the Posts component, as well as PropTypes — since there aren’t any props to type check. And you’re done! Try it out for yourself.

```
import React, { Fragment, useEffect } from 'react'
import { useSelector, useDispatch } from 'react-redux'
import PostItem from './PostItem'
import PostForm from './PostForm'
import { getPosts } from '../../actions/post'

const Posts = () => {

  const { posts } = useSelector(state => state.post)

  const dispatch = useDispatch()

  useEffect(() => {
    dispatch(getPosts())
  }, [getPosts])

  return (
    <Fragment>
      <h1 className="large text-primary">Posts</h1>
      <p className="lead">
        <i className="fas fa-user" /> Welcome to the community
      </p>
      <PostForm />
      <div className="posts">
        {posts.map((post) => (
          <PostItem key={post._id} post={post} />
        ))}
      </div>
    </Fragment>
  )
}

export default Posts
```

Note: If you use any data that isn't from state, you will still need to pass that into props.

To me, this code looks much more clean. The `connect` and `mapStateToProps` syntax is cumbersome to type and ineloquent to read. Thank you Hooks!
