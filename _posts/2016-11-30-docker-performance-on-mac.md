---
layout: post
title: Docker performance on Mac
image: docker-performance-on-mac.png
categories:
  - devops
tags:
  - docker
  - vmware
  - virtualbox
  - macos
  - devops
  - performance
  - rails
  - ror
  - hypervisor
author:
  login: ain
  name: Ain Tohvri
excerpt_separator: <!--more-->
assets:
  external:
    js:
      - https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.17/d3.min.js
  inline:
    css:
      - docker-performance-on-mac.css
    js:
      - docker-performance-on-mac.js
---
Docker performance on Mac is infamous esp. on larger applications. But what about different hypervisors?<!--more-->

There are 4 options to run Docker on macOS:

- Docker for Mac
- VirtualBox
- VMware
- Parallels

Without further ado, Docker can not achieve near-native experience on any of them. Not at least on a legacy Rails application that runs some 30 locales, 19 GB of content and 1000+ queries per page. It takes ~1 min to reload a page on such system.

To improve, you can go for things that are normally not done on development environment:

- Add [rails-dev-boost](https://github.com/thedarkone/rails-dev-boost) gem
- Enable caching in _config/environments/development.rb_:

  ```
  config.cache_classes = true
  ```

On Rails 3, this would get the speed up by 3x.

Now, after some testing with [rack-mini-profiler](https://github.com/MiniProfiler/rack-mini-profiler), the numbers for the 4 hypervisors stack up as follows:

<svg class="speed-chart"></svg>

Docker's performance problems on Mac are not new. There're multiple topics on forum and some of them, e.g. [File access in mounted volumes extremely slow, CPU bound](https://forums.docker.com/t/file-access-in-mounted-volumes-extremely-slow-cpu-bound/8076), will soon celebrate its 1-year anniversaries. Unfortunately so.
