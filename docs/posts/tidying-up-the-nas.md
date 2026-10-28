---
description: Our old NAS was open to the internet, 83% full and quietly unwatched, so I spent a few days locking it down, adding health alerts, freeing half its space and giving it a tidy layout.
date: 2026-11-03
authors: [lab]
categories: [Foundations]
draft: true
---

# Tidying up the NAS

Our NAS holds the family's photos, home videos, music and films, and for years we'd simply used it without looking after it. Before building anything new on top of it, I gave it a proper review, then spent a few days putting right what I found: closing it off from the internet, fixing who can see what, adding health checks, and freeing up half its space.

<!-- more -->

My son was away for part of the school holiday, so this one was just me, working with Claude.

## What the review found

With Claude, I went through its settings, its shared folders and a report of what was using the space. It wasn't pretty.

- **It could be reached from the internet.** The maker's remote access feature was switched on, and the NAS still had rules for the router to open ports to it, left over from old apps.
- **One all-powerful account.** The only administrator was the default `admin` account, the first name anyone would try, with no two-step sign-in.
- **Nobody would know if a drive was failing.** Only a quick weekly drive check ran. There had never been a deep one, the data had never been checked for silent corruption, and email alerts were off.
- **83% full,** past the point where the NAS itself starts warning.
- **22 apps installed,** many of them old, stopped or unused, on a NAS with a single slow processor.

It's an old box, too, which made locking it down matter all the more.

## Closing the doors

First, nothing from outside should be able to reach it:

- **Remote access off,** and the dynamic name that pointed at our house deleted.
- **Router rules removed,** and the router checked to make sure it wasn't forwarding anything to the NAS.
- **A firewall on the NAS** that allows the home network and blocks everything else.
- **The test that matters:** on a phone with Wi-Fi off, I tried to reach the NAS over 4G. Nothing answered, which is exactly right.

While I was there, I made the NAS always use a secure (HTTPS) connection, with a certificate the family's Macs trust, so the browser shows a padlock instead of a warning.

## Accounts and permissions

The new rule: **permissions go to groups, not people.** There's a group for the family (watch, listen, view photos), one for the adults (manage the photos, videos and documents), and one for the lab. When someone needs access, they join a group, and nothing else changes.

- **A new administrator account** with a long password and two-step sign-in, which is now required for every administrator. The default `admin` account is disabled.
- **Everyday accounts** for each of us, and none of them are administrators.
- **Machines get their own accounts,** each able to reach only what it needs. The kitchen dashboard's account, for example, can read one photo folder and nothing else.
- **Guest access removed** from every folder, and the remote command-line login (SSH) switched off until the lab needs it.

## Health checks

The drives turned out to be in good shape: about **70,000 hours** of running each, roughly eight years, with **no bad sectors** on any of them. All four passed a full, deep test.

To keep it that way, the NAS now:

- **emails me** about drive problems, a failing or nearly full volume, and failed backups;
- **runs a deep test of every drive monthly;**
- **checks all the data against its parity every three months** (called scrubbing), which catches silent corruption before a drive failure turns it into lost files.

The drives are healthy but old, so the numbers get a look each month. The first sign of a bad sector is the signal to start planning a replacement.

## Making room

The biggest win was simple: **an old Mac backup of more than 1.5TB**, for a computer last backed up in 2021. Deleting it took the NAS from **83% to 50% full.**

The Mac we do use now backs up to a fresh, encrypted backup, under its own account with a size limit. Before, it signed in as the administrator, so the limit had never applied, and its backups could have filled the NAS.

I also cut the 22 apps down to about four, the ones it actually needs, and turned off old ways of connecting that we no longer use.

## A tidier layout

The shared folders were renamed and reorganised into a simple set: films and TV, music, photos, home videos, documents, the Mac backups, config backups and lab files. Renaming is instant on the NAS, where copying would have taken days.

The music needed more care. It lived in an old iTunes library, with **44 duplicate artist folders** left behind by a sync app from long ago. I copied it into a clean `Artist/Album` layout with **beets**, a free music organiser, which merged the duplicates as it went. It copies rather than moves, so the old library stayed untouched until the new one had been checked, and only then was it deleted.

## Backups

Not everything needs an offsite backup. Films can be ripped from the discs again, and the Mac backups are already backups. The things that can't be replaced, the photos, home videos and now our documents, are copied offsite. For the photos and videos, deleted or overwritten files can be recovered for 90 days. The documents are encrypted before they leave the house, and keep their own history of versions.

A backup you haven't restored from is only a hope, so I **downloaded a few old photos from the offsite copy and opened them.** They were fine.

## Things that bit me

- **The films vanished.** After I'd uninstalled the old apps, the new administrator couldn't see the films at all. They hadn't gone anywhere. On this NAS, an administrator can *manage* every folder but can only *open* the ones it's been given access to, and the new account hadn't been. So now the administrators group can open every folder.
- **Nobody could open anything.** A second check found the family groups had been created but never given any access to the folders, so that was put right too.
- **The Mac kept using the old login.** Its backup runs as a system service with its own saved password, so it carried on quietly signing in as the old administrator until that password was changed.
- **The Mac lost the NAS.** A VPN app on the laptop had put its own name servers first, so the Mac couldn't find the NAS by name. Allowing local network access in the VPN app, plus a fixed entry on the Mac, sorted it.

## Built with Claude

There wasn't much code in this one: it was mostly settings, worked through step by step from a plan written with Claude. The code that did come out of it, for the photos and the documents, was all written by Claude, and has its own posts.

## Where it's up to

All of the above is done. Still to come:

- **Converting the films** from their old DVD format to a much smaller modern one, which should free about another 1.2TB.
- **Emptying the holding folders** from the photo and document clean-ups, once they've had a week to prove nothing's missing.
- **A proper media server** later on, once the Pi cluster is running.

## What it cost

Nothing to buy. The offsite backup has a monthly bill, which grows a little now the documents are in it.

## What's next

The photos: 20 years of family pictures from old laptops, phones and drives, and a surprising number of copies of each one.
