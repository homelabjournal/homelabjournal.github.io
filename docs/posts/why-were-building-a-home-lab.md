---
date: 2026-10-27
authors: [lab]
categories: [The plan]
draft: true
---

# Why we're building a home lab

It started with a NAS that was 83% full, a cupboard full of cables, and a teenager who wanted to run a Minecraft server for his friends.

<!-- more -->

## Where we started

Like a lot of houses, ours had grown its network by accident. The internet provider's router sat in a cupboard next to a 24-port switch, a patch panel, and a 2012 Synology NAS. The cabinet floor had become a pile of power adapters. We'd never properly mapped which wall socket went to which switch port, and the NAS was full of a decade of family photos, old laptops' worth of documents, and backups of computers we no longer own.

I've been writing code for more than 30 years. My son is a teenager. He's curious about how the internet actually works, and he wants to host things for his friends. A home lab gives us both a project, and him a place where breaking things is part of learning.

## The plan

We wrote the whole thing down first: a plan in phases, each one small enough to finish in a few evenings, and each one leaving the house working.

1. **Foundations:** a Pi-hole on an original Raspberry Pi (512MB of RAM, a single 700MHz core) to block ads across the house, and a proper look at what's actually plugged into what.
2. **A kitchen dashboard:** an old iPad on the wall showing the family calendar, weather, bin day, our trains and a photo of the day, served by that same Pi.
3. **Tidying the NAS:** locking it down, de-duplicating 50,000 photos, and turning years of scanned paperwork into something you can find things in.
4. **A real firewall,** with a separate lab network so our experiments can't reach the family's devices.
5. **A Raspberry Pi cluster** running Kubernetes, for everything that comes after.
6. **Game night:** Minecraft for his friends, with backups and a Discord bot.
7. **A VPN, a domain and proper HTTPS,** so we can reach the lab from anywhere without opening it to everyone.
8. **The whole house behind the firewall,** with new Wi-Fi and separate networks for family, guests, smart plugs and cameras.
9. **Going public, carefully:** a website (this one, eventually) served from home, and cameras that don't send video to someone else's cloud.

## The rules we set ourselves

- **Write everything down.** The plan, every decision and every config backup live in a private Git repository.
- **Never break the family's internet.** Anything risky happens on the lab network or late at night.
- **Scripts never delete.** They move things aside, write an undo log, and a human empties the bin a week later.
- **He drives.** I explain, he types. When it breaks, we work out why together.

## What's next

The first weeks went on foundations and a lot of tidying. The next posts cover how we found 50,000 duplicate photos, a dashboard for an iPad stuck on Safari 12, and turning 6,000 files from old hard drives into about 540 neatly named documents.
