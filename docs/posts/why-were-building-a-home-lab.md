---
description: Why a dad and his teenage son are turning an unused wired house and a drawer of old kit into a home lab, built with AI from day one.
date: 2026-10-27
authors: [lab]
categories: [The plan]
---

# Why we're building a home lab

It started with screens. My son is a teenager, and like most teenagers he can lose an evening to gaming or scrolling on his phone. I wanted to find something fun we could do together that would get him building rather than just consuming.

<!-- more -->

## Why a home lab

A home lab ticks both boxes. He learns genuinely useful things along the way: how networks, servers and the internet actually work. And there's no shortage of fun things to build with it.

A Minecraft server for his friends was one of the ideas. Running one properly means a server that stays up, backups, keeping strangers out, and letting his friends in from their own houses. That leads straight into firewalls, networks, Linux and a bit of code, which is exactly the point.

## A house that was already wired

When we had building work done on the house a few years ago, we had Ethernet run to most of the rooms. It all comes back to a patch panel and a 24-port switch in a small wall cabinet in a cupboard, next to the internet provider's router.

And then we never really used it. A few things were plugged in, the Wi-Fi did the rest, and the cabinet slowly filled up with power adapters and loose cables. Nobody had ever properly mapped which wall socket went to which switch port. So we have a wired house, a decent switch and a cabinet with room to spare, all massively under-used. That's a great place to start a home lab.

## What we found in drawers

Before buying anything, we went hunting. It's surprising what a house collects:

- **An original Raspberry Pi** from 2012: 512MB of RAM and a single 700MHz core. It now blocks ads for the whole house with Pi-hole.
- **A 2012 Synology NAS**, 83% full of a decade of family photos, old laptops' worth of documents, and backups of computers we no longer own.
- **An old iPad Air** that can't be updated past iOS 12. It's becoming a kitchen dashboard.
- **An iPad mini** that will become a little status screen for the rack.
- **A Philips Hue starter kit**, still in its box, and **three old TP-Link smart plugs**.
- **An old Kindle**, which might just become an e-ink train board by the front door.
- **A cable tester and a punch-down tool** from when the house was wired, for fixing the wall sockets that don't work.
- **A BBC micro:bit**, some old phones and laptops, and an **old desktop PC** that's getting a second life as a Linux From Scratch project.

None of it was bought for this, and most of it had been sitting unused for years.

## What we'll buy along the way

Some things we can't conjure from a drawer, so we'll buy them as each phase needs them, rather than all at once:

- **A small fanless firewall box**, to sit between the internet and the house. It's already ordered.
- **A couple of Raspberry Pi 5s** and a rack mount for them, to become a small Kubernetes cluster.
- **Shelves, fans and a temperature sensor** for the cabinet, so it stops being a pile on the floor.
- **Smart plugs** we can control locally, starting with one for the kitchen iPad's charger.
- **New Wi-Fi access points**, much later, once everything else is in place.
- **A domain name or two**, including the one this blog lives on.

I'll share what we bought, roughly what it cost, and whether it was worth it.

## The plan

We wrote the whole thing down first: a plan in phases, each one small enough to finish in a few evenings, and each one leaving the house working.

1. **Foundations:** the Pi-hole, and a proper survey of what's actually plugged into what.
2. **A kitchen dashboard:** the old iPad on the wall showing the family calendar, weather, bin day, our trains and a photo of the day.
3. **Tidying the NAS:** locking it down, de-duplicating tens of thousands of photos, and turning years of scanned paperwork into something you can find things in.
4. **A real firewall,** with a separate lab network so our experiments can't reach the family's devices.
5. **A Raspberry Pi cluster** running Kubernetes, for everything that comes after.
6. **Game night:** the Minecraft server, with backups and a Discord bot.
7. **A VPN and proper HTTPS,** so we can reach the lab from anywhere without opening it up to everyone.
8. **The whole house behind the firewall,** with new Wi-Fi and separate networks for family, guests, smart plugs and cameras.
9. **Going public, carefully:** a website served from home, and cameras that don't send video to someone else's cloud.

## An AI on the team

There's a third member of this project: **Claude**, Anthropic's AI assistant. We're using it for almost everything, and we want to be upfront about that from the start, because it's a big part of the story.

- **Planning.** The whole plan, phase by phase, was written in conversation with Claude: what to buy, what order to do things in, and what could go wrong.
- **Writing the code.** **All of the code is written by Claude**, using **Claude Code**, which works directly in our repository: it reads the code, makes changes, runs the tests and explains what it did. Our part is the spec, the feature requests and the brainstorming, and reviewing and testing what comes back.
- **Doing the work.** It walks us through each step, reads error messages and logs with us, and keeps the plan and notes up to date as we go.
- **This blog.** Posts are drafted by Claude from our plan, our notes and the project history, then edited by us so they say what we actually did and think.

None of this means switching your brain off. My son still has to understand what's being built and why it works, and that's the point. But it means a dad with a day job and a teenager can take on a project this size, and learn far more along the way than they would from a tutorial. Using AI well is a skill in itself, and he's learning that too.

## The rules we set ourselves

- **Write everything down.** The plan, every decision and every config backup live in a private Git repository.
- **Never break the family's internet.** Anything risky happens on the lab network, or late at night.
- **Scripts never delete.** They move things aside and keep an undo log, and a human empties the bin a week later.
- **He drives.** He decides what we try next, runs the commands and asks the questions. When it breaks, we work out why together.
- **The AI suggests, we decide.** Nothing runs on our network that we haven't read and understood, and it never gets our passwords.

## What's next

The first few weeks went on foundations and a lot of tidying. I'll write them up in the order we did them: first, blocking ads for the whole house with a 2012 Raspberry Pi; then building a dashboard for an iPad stuck on Safari 12; then finding 50,000 duplicate photos; and turning 6,000 files from old hard drives into about 540 neatly named documents.
