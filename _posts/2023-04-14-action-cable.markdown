---
layout: post
title: 'Rails Action Cable for External Applications'
date: 2023-03-21
image: 'actioncable.jpg'
image-alt: 'Rails Action Cable graphic'
---

I recently had to implement WebSockets in a Rails 6 app for use by an external application. I found that the existing tutorials were outdated or missing key details. So, I hope this tutorial will fill the gap.

## Config

If you are using Rails 6, Action Cable is already installed. The only additional gem you will need is Redis, so add this line to your gemfile and run `bundle install`:

```
gem 'redis', '~> 4.0'
```

In your config folder, add `cable.yml` containing the following:

```
development:
  adapter: redis
  url: redis://localhost:6379

test:
  adapter: test

staging:
  adapter: redis
  url: <%= ENV['REDISCLOUD_URL'] %>

production:
  adapter: redis
  url: <%= ENV['REDISCLOUD_URL'] %>
```

`ENV['REDISCLOUD_URL']` will be automatically set in Heroku by the Redis Enterprise Cloud add-on later.

Now, add this line to your `config/environments` files so that Action Cable will accept all hosts for now:

```
config.action_cable.disable_request_forgery_protection = true
```

Next, create file `redis.rb` in `config/initializers` with this code:

```
require 'redis'

# Define the redis server url
redis_url = ENV["REDISCLOUD_URL"] || "redis://redis:6379"

# Create a new redis client using the url
$redis = Redis.new(url: redis_url)
```

Last, mount the Action Cable server in `config/routes.rb` with this line:

```
mount ActionCable.server => '/cable'
```

## Creating a Channel

Now that Action Cable is configured, we can make our Channel by running `rails g channel Chat`

This will create a `channels` folder with the Action Cable base classes and the ChatChannel class.

I want to be able to connect to this channel and send a 'room' id to connect to the stream for a specific room. To do this, I need a method for subscribing to the Channel, and another for starting the specified stream:

```
class ChatChannel < ApplicationCable::Channel
  def subscribed
    puts 'subscribed'
  end

  def stream_from_room(data)
    stream_from "chat_#{data['room_id']}"
  end
end
```

To test this, run `redis-server` and `rails s` in seperate terminal windows. Install [Simple WebSocket Client](https://chrome.google.com/webstore/detail/simple-websocket-client/pfdhoblngboilpfeibdedpjgfnlcodoo?hl=en) for Chrome and connect to Action Cable through `ws://localhost:3000/cable`.

Once connected, send the following messages to subscribe to the channel and stream from the room:

```
{"command": "subscribe", "identifier": "{\"channel\": \"ChatChannel\"}"}
```

```
{"command": "message", "identifier": "{\"channel\": \"ChatChannel\"}", "data":"{\"action\": \"stream_from_room\", \"room_id\":\"1234\"}"}
```

You will now recieve all data broadcasted to `chat_1234`. To broadcast data, do something like this in your ChatController create action:

```
ActionCable.server.broadcast "chat_#{chat_params[:room_id]}", chat_params
```

Hopefully, you can easily adapt my generic chat app example to your code. In my case, I had to take data sent from an external service's web hooks and stream the tranformed data to connected iOS apps. How the external app connects to the web socket, sends messages, and recieves stream data is language/framework dependent - so that part is out of scope for this tutorial. Happy coding!