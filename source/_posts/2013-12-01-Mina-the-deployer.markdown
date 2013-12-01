---
layout: post
title: Mina, the deployer
date_string: 1 December 2013
---

I recently decided to setup a dedicated website for my company as opposed to just using my personal one. It’s a static site, with barely any content right now.

Now, I usually rely on capistrano for deployment, but since capistrano had recently undergone a major facelift, I sensed it as an opportunity to try [Mina](https://github.com/nadarei/mina). I have known about the gem since it’s very beginning, but the pressures of modern web developer life means less time for playing around, and more for getting things done. In other words, don’t change the deployer if it ain’t broken.

Mina is very similar to Capistrano, except one small yet pivotal fact. Instead of running commands one-by-one over SSH, it creates a bash script from your configuration and executes it remotely as one SSH command. Sounds astute to me. It has the same configuration and deploy setup as Capistrano, and anyone with some Capistrano experience will pick it up pretty quickly.

One thing that really stuck out for me and propelled me to write this post is it’s reliance on the existing SSH set-up on your machine. For example, In Capistrano, one has to explicitly set up the ssh forward agent in the deploy script itself. But, in Mina, one just needs to specify forward agent in their SSH config, and Mina will pick that up. It’s quite logical, no idea why it wasn’t the case for Capistrano.

Anyways, hope this will motivate you guys to try Mina as well.
