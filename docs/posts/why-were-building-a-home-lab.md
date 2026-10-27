---
date: 2026-10-27
authors: [lab]
categories: [The plan]
---

# Why we're building a home lab

It started with my son asking if he could run a Minecraft server for his friends. I said yes, and then I said "but let's do it properly".

<!-- more -->

## The real reason

If I'm honest, this wasn't really about Minecraft. My son is a teenager, and like most teenagers he can lose an evening to gaming or scrolling on his phone. I wanted to find something we could do together that would get him building rather than just consuming: something where he'd learn genuinely useful things, how networks, servers and the internet actually work, and enjoy himself along the way.

The Minecraft server was the hook. Running one properly means a server that stays up, backups, keeping strangers out, and letting his friends in from their own houses. That leads straight into firewalls, networks, Linux and a bit of code. It turned out to be the perfect excuse.

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

## The rules we set ourselves

- **Write everything down.** The plan, every decision and every config backup live in a private Git repository.
- **Never break the family's internet.** Anything risky happens on the lab network, or late at night.
- **Scripts never delete.** They move things aside and keep an undo log, and a human empties the bin a week later.
- **He drives.** I explain, he types. When it breaks, we work out why together.

## What's next

The first few weeks went on foundations and a lot of tidying. Coming up: how we found 50,000 duplicate photos, building a dashboard for an iPad stuck on Safari 12, and turning 6,000 files from old hard drives into about 540 neatly named documents.
