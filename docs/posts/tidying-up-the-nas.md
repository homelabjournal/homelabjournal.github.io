---
description: Our old NAS was open to the internet, 83% full and nobody was keeping an eye on it, so I spent a few days locking it down, setting up health alerts, freeing half its space and tidying the layout.
date: 2026-11-04
authors: [lab]
categories: [Foundations]
draft: true
---

# Tidying up the NAS

Our NAS has all the family's photos, home videos, music and films on it, and for years we just used it without ever really looking after it. Before building anything new on top of it, I went through it properly, then spent a few days fixing what I found: shutting it off from the internet, sorting out who can see what, setting up health checks and freeing up half the space.

<!-- more -->

My son was away for part of the school holiday, so this one was just me.

## What I found

I went through the settings, the shared folders and a report of what was taking up the space. It wasn't great.

- It could be reached from the internet. The maker's remote access feature was on, and the NAS still had rules telling the router to open ports to it, left over from old apps.
- The only administrator was the default `admin` account, the first name anyone would try, with no two-step sign-in.
- If a drive was failing, nobody would have known. Only a quick weekly check ran. There had never been a deep test, the data had never been checked for silent corruption, and email alerts were off.
- It was 83% full, past the point where the NAS itself starts warning you.
- It had 22 apps installed, a lot of them old, stopped or never used, on a box with one slow processor.

It's an old NAS too, so locking it down mattered even more.

## Shutting it off from the internet

The first job was making sure nothing outside the house could reach it. I turned remote access off and deleted the dynamic name that pointed at our house. I removed the old router rules, then checked the router itself wasn't forwarding anything to the NAS. And I turned on the NAS's own firewall, set to let in the home network and block everything else.

To check, I took a phone, turned the Wi-Fi off and tried to reach the NAS over 4G. Nothing answered, which is what I wanted.

While I was in there, I made it always use a secure (HTTPS) connection, with a certificate the family's Macs trust, so the browser shows a padlock instead of a warning.

## Accounts and permissions

Permissions now go to groups rather than to people. There's a group for the family (watch, listen, look at photos), one for the adults (manage the photos, videos and documents) and one for the lab. When someone needs access, they join a group and nothing else has to change.

- I made a new administrator account with a long password and two-step sign-in, and two-step is now required for every administrator. The default `admin` account is disabled.
- We each have an everyday account, and none of them are administrators.
- Machines get their own accounts, and each one can reach only what it needs. The kitchen dashboard's account can read one photo folder and nothing else.
- Guest access is gone from every folder, and SSH (the remote command-line login) is off until the lab needs it.

## Health checks

The drives were the good news. Each has about 70,000 hours on it, roughly eight years of running, with no bad sectors, and all four passed a full deep test.

To keep it that way, the NAS now:

- emails me about drive problems, a failing or nearly full volume, and failed backups;
- runs a deep test of every drive once a month;
- checks all the data against its parity every three months. That's called scrubbing, and it catches silent corruption before a drive failure turns it into lost files.

They're healthy but old, so I look at the numbers each month. The first bad sector is my cue to start planning replacements.

## Making room

Most of the space came back in one go. There was an old Mac backup of more than 1.5TB, for a computer last backed up in 2021. Deleting it took the NAS from 83% full to 50%. Later, after the photo and document clean-ups (more on those in the next posts), and once I'd emptied their holding folders and the recycle bins, it got down to 41%.

The Mac we still use now backs up to a fresh, encrypted backup, under its own account with a size limit. Before, it signed in as the administrator, so the limit had never applied and its backups could have filled the NAS.

I also cut the 22 apps down to about four, the ones it actually needs, and turned off old ways of connecting that we don't use any more.

## A tidier layout

I renamed and reorganised the shared folders into a simple set: films and TV, music, photos, home videos, documents, the Mac backups, config backups and lab files. Renaming on the NAS is instant, where copying would have taken days.

The music took more work. It was in an old iTunes library with 44 duplicate artist folders, left behind by a sync app from years ago. I copied it into a clean `Artist/Album` layout with beets, a free music organiser, which merged the duplicates as it went. Because it copies rather than moves, the old library stayed as it was until I'd checked the new one, and only then did I delete it.

## Backups

Not everything needs an offsite backup. Films can be ripped from the discs again, and the Mac backups are already backups. The things we can't replace (the photos, the home videos and now our documents) get copied offsite. For the photos and videos, anything deleted or overwritten can be got back for 90 days. The documents are encrypted before they leave the house and keep their own version history.

I didn't want to just assume the backup worked, so I downloaded a few old photos from the offsite copy and opened them. They were fine.

## Things that bit me

**The films disappeared.** After I'd uninstalled the old apps, the new administrator couldn't see the films at all. They hadn't gone anywhere. On this NAS an administrator can *manage* every folder but can only *open* the ones it's been given access to, and the new account hadn't been given any. Now the administrators group can open every folder.

**Then nobody could open anything.** A second check found the family groups had been created but never given access to any folders, so I fixed that too.

**The Mac kept using the old login.** Its backup runs as a system service with its own saved password, so it carried on signing in as the old administrator until I changed that password.

**The Mac lost the NAS.** A VPN app on the laptop had put its own name servers first, so the Mac couldn't find the NAS by name. Allowing local network access in the VPN app, plus a fixed entry on the Mac, sorted it.

## How I did it

There wasn't much code in this one. It was mostly settings, worked through step by step from a plan written with Claude. The code that did come out of it, for the photos and the documents, gets its own posts.

## Where it's up to

All of the above is done. Still to do:

- Converting the films from their old DVD format to a much smaller modern one, which should free up about another 1.2TB.
- A proper media server at some point, once the Pi cluster is running.

## What it cost

Nothing to buy. The offsite backup is a monthly bill, which goes up a bit now the documents are in it.

## What's next

The photos: 20 years of family pictures from old laptops, phones and drives, and a surprising number of copies of each one.
