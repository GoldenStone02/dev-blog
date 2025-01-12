---
title: Self-Hosted Home Server
date: 2023-09-08
description: Homelab Setup on a Raspberry Pi 4 with Ansible.
summary: Homelab Setup on a Raspberry Pi 4 with Ansible.
slug: "home-server"
tags: ["ansible","self-hosted", "server"]
---

Before I start on my rambling on how I began off my mini little homelab server on my Raspberry Pi 4, I would have to first thank 
- `{{< icon "github" >}} notthebee` for the initial inspiration for this project and,
- `{{< icon "github" >}} alex27riva` for his ansible playbook for his own self-hosted server

## The beginning

Ever since I've started entered IT, I have always wanted to try starting up a homelab server as a fun little mini project. Little did I know, I've just entered a deep rabbit hole that consisted of many self-hosted applications from both github and the wonderful people over at `{{< icon "reddit">}} r/selfhosted`.

This all began when I first stumbled upon when I was recommended `{{< icon "youtube" >}}Wolfgang's Channel` on the applications he runs on his home server. If you're curious, it shouldn't take you long to find the video in question ;)

Alternatively, you could watch the video here if you fancy it that way.

{{< youtubeLite id="f5jNJDaztqk">}}

## Starting Out
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

*explain it via the dir example.*

## Scope Creep
We all love and hate scope creep T-T

A phenomenon where a once relatively simple project somehow managed to balloon into a mangled monstrosity that was once called **"small"** and **"simple"**.

Started researching random topics 

### Eventually Resolved
How I got out of scope creep

## Completed?
At least for now, I felt that my homelab is at a stable place, where I can enjoy all my selfhosted services while still being able to tinker with its inner workings.


If you're curious on my ansible playbook which I used for my Raspberry Pi, feel free to check out my github repo below.
{{< github repo="GoldenStone02/ansible-home-selfhosted" >}}
