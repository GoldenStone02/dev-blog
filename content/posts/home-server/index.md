---
title: Self-Hosted Home Server
date: 2025-06-16
description: Homelab Setup on a Raspberry Pi 4 with Ansible.
summary: Homelab Setup on a Raspberry Pi 4 with Ansible.
slug: "home-server"
tags: ["ansible","self-hosted", "server"]
---

Before I start on my rambling on how I began off my mini little homelab server on my Raspberry Pi 4, I would have to first thank 
- `{{< icon "github" >}} notthebee` for the initial inspiration for this project and,
- `{{< icon "github" >}} alex27riva` for his ansible playbook for his own self-hosted server

## Humble Beginning

Ever since I've started entered IT, I have always wanted to try starting up a homelab server as a fun little mini project. Little did I know, I've just entered a deep rabbit hole that consisted of many self-hosted applications from both github and the wonderful people over at `{{< icon "reddit">}} r/selfhosted`.

This all began when I first stumbled upon when I was recommended `{{< icon "youtube" >}}Wolfgang's Channel` on the applications he runs on his home server. If you're curious, it shouldn't take you long to find the video in question ;)

Alternatively, you could watch the video here if you fancy it that way.

{{< youtubeLite id="f5jNJDaztqk">}}

## The Calm Before the Storm
Initially, I used my Raspberry Pi 4, which I obtained from an old old project of mine. As such, the end goal was to have all the services I would ever want installed onto a Raspberry Pi 4.

Was it going to be a challenge? Well, I'll soon find out the true challenge wasn't setting up the server, but what **applications I should even begin to selfhost**. As although it would be fun to attempt running a game server on a Pi, let's face the truth that we'll barely have enough time to even play on said "game" server if you're a student like me ;-;

This also doesn't include the fact that I would have a limited amount of space on the Raspberry Pi, though that didn't really stop me from installing and tinkering with applications such as `NextCloud`.

After doing countless hours on researching, aka scrolling through `{{< icon "reddit" >}}r/selfhosted` for new and old selfhosted applications other people were running xD, I managed to came up with a small list of applications that I felt were useful.

Mainly:
- **PiHole + UnBound**: For adblocking and DNS
- **Portainer**: For managing containers
- **VaultWarden**: Password manager
- **Watchtower**: Update containers automatically :D
- **Homer**: A simple dashboard

## How Ansible came to be part
{{< alert "circle-info" >}}
I am not an expert for Ansible by any means, so take my methodology with a grain of salt.
{{< /alert >}}

While deploying all my self-hosted applications by hand might be the easiest solution, it's not necessarily the most optimal solution. As such, after considering between a docker compose file and ansible, I ended up picking `Ansible` for its idempotent functionalities.

For the uninitiated on what idempotency is, it ensures that a task can be executed multiple times without modifying or changing the system beyond the initial application. This means that an idempotent task would behave the same way every time it is ran, which would allow for predictable and reliable deployments.

A simple example would be creating a new directory. If we were to use the command `mkdir /test` to create a new directory, it would run perfectly fine on the first attempt. However, every subsequent attempts would result in the following error.
```
~$ mkdir /test
mkdir: cannot create directory ‘/test’: File exists
```

To solve this issue, we can simply use the `-p` flag to ensure the command doesn't fail on its subsequent attempts.

Although this specific example would seem quite trivial to solve, it may not be as straight forward to solve for other commands such as `curl` or `rsync`. As such, simply writing a bash script for the deployment of multiple services would be both naive and an extremely daunting task. As a result, using Ansible would be the **smart** move to ensure consistent deployments.
> In addition, it was also an excuse to learn Ansible as I already had some experience with {{< icon "docker" >}} docker & docker-compose oops.


## Sc0pe Cr33p
We all love and hate scope creep T-T

A phenomenon where a once relatively simple project somehow managed to balloon into a mangled monstrosity that was once called **"small"** and **"simple"**. This was the position I found myself in, well not initially but you get the gist of it.

So at first, I started conducting basic research on the different services that I listed out above, and their varying methods of installing, configuring and deployment. I thought it would be a trivial task.

*"Just write a few Ansible scripts for each Docker container. How hard could it be"*

{{< lead >}}
Famous last words.
{{< /lead >}}

### Down the Rabbit Hole
Oh boy, where do I even begin?

Lets start quick firing my development cycle that explains how the project become to be:
- **Adblocking?**: Setup Pihole for adblocking and Unbound for a local DNS for my services
- **Password Management**: Deploy Vaultwarden for my secrets >:)
- **Managing Containers?**: Hmmm, let's download Portainer... and this fancy docker cli ( [lazydocker](https://github.com/jesseduffield/lazydocker) )
- **Dashboard?**: Oh right, can't forget my Homer dashboard
- **Reddit?**: Let's go with Libreddit (now Redlib)......................wait, why do we need this?
- **Updating containers?**: Errrr, let's go with Watchtower
- **Monitoring?**: Huh? Isn't Homer enough?? NO! WE NEED UPTIME KUMA
- **Reverse Proxy?**: Can't forget about our dear NGINX proxy!
- **Local Cloud???**: OOO, wouldn't it be fun to host a local cloud? Let's try NextCloud and MariaDB!
- **Jellyfin?**: Why stop there? might as well make this a place to host all my linux ISOs!
- **Openbook?**: While we are at it, might as well get to reading
- **Testing?**: Wouldn't it be fun to try testing this script on a Virtualbox VM?
- **Security?**: How can I forget security?! `ufw` ftw!!!!

It was at his moment I realised that I wasn't using Ansible to manage my mini-homelab. I was building the infrastructure for Ansible to manage itself.

### Finally found the light
After developing, reiterating, testing, rinse, and repeat, I've arrived at the final version of my Ansible playbook project! Glad to be finally done with this *mini* project of mine!

It only took, \*checks clock\* wait...**two months?!** Whoa. What started as a small project turned into a full-blown odyssey. I guess scope creep is one tough cookie to swallow...
## Completed?
At least for now, I felt that my homelab is at a stable place, where I can enjoy all my selfhosted services while still being able to tinker with its inner workings.

Although I might have plans of integrating other services such as Authelia into my hosted web application, it's not my current main priority :]


If you're curious on my ansible playbook which I used for my Raspberry Pi, feel free to check out my github repo below.
{{< github repo="GoldenStone02/ansible-home-selfhosted" >}}
