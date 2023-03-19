---
layout: post
title: Multiple Ghost Blogs on One Server
date: 2020-02-25
image: 'ghost.jpg'
---

I love [Ghost](https://ghost.org/). In the past year I've migrated all of my sites from WordPress and I have never looked back. However, the increased cost of running a VPS for each site adds up. There are a lot of forum discussions on how to install multiple ghost blogs on one server, but they all suggest complicated [Docker](https://www.docker.com/) setups or post [this outdated article](https://www.digitalocean.com/community/tutorials/how-to-serve-multiple-ghost-blogs-on-one-vps-using-nginx-server-blocks) from 2013.

It turns out it's very simple - so I will show you how.

First, get your Ubuntu server (I can vouch for [Digital Ocean](https://www.digitalocean.com/) or [Linode](https://www.linode.com/)). Then, follow the Server Setup instructions [here](https://ghost.org/docs/install/ubuntu/#server-setup) up until the Install Ghost section. Be careful of using special characters in the password you choose. I had a backtick (`) in mine and it messed up the MySQL commands.

Now follow the instructions for Install Ghost, except make two directories, one for each site:

    # Make the first directory
    sudo mkdir -p /var/www/firstsite.com

    # Replace <user> with the name of your user who will own this directory
    sudo chown <user>:<user> /var/www/firstsite.com

    # Set the correct permissions
    sudo chmod 775 /var/www/firstsite.com


    # Make the second directory
    sudo mkdir -p /var/www/secondsite.com

    # Replace <user> with the name of your user who will own this directory
    sudo chown <user>:<user> /var/www/secondsite.com

    # Set the correct permissions
    sudo chmod 775 /var/www/secondsite.com

Finally, navigate into each folder and run `ghost install` - and it's that easy! Ghost takes care of the Nginx config for you. Just repeat the steps above and run as many blogs as your server can handle.
