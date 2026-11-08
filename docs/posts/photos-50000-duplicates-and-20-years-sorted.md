---
description: How I found and set aside over 50,000 duplicate photos and videos, then sorted 20 years of family pictures into folders by date, without letting a script delete anything.
date: 2026-11-08
authors: [lab]
categories: [Foundations]
---

# Photos: 50,000 duplicates, then 20 years sorted by date

Our family photos were on the NAS, in theory. In practice they were spread across year folders, camera dumps, phone dumps and copies of old laptops, often several times over. Over three days I set aside more than 50,000 spare copies and sorted everything left into one folder per month. Two scripts did the work, with one rule: no script ever deletes anything.

<!-- more -->

## The mess

The photo share had grown the way these things do. There were year folders, plus a folder for every camera and phone that had ever been plugged in, and some of those had been copied into the year folders as well. On top of that, I copied in everything from old PCs, an old hard drive and an old laptop, so it was all in one place before I started.

Before changing anything, I scanned the lot from the laptop, read-only. It found:

- 36,946 files taking up 171GB: about 33,700 JPEGs, 2,200 videos (75GB of the total) and a few hundred iPhone photos.
- About 11,000 exact copies, 52GB of them, found by comparing what's inside the files rather than their names. Half of that was videos, with the same clips sitting in two camera folders and a year folder.
- Junk: hundreds of thumbnail caches from an old iPod and Apple TV, which look like photos but aren't, plus leftovers from old photo libraries and 14 zip files whose photos were all already on the share.

And that was before the newest photos. Almost everything since 2018 was only in iCloud.

## Nothing gets deleted by a script

Deleting the wrong copy of a family photo is the one mistake I couldn't undo, so the scripts never delete. They move things into holding folders, `_duplicates` and `_junk`, keeping each file's original folder path, and they log every move so one command can put the lot back. I empty the holding folders myself, and only after using the library for a while and finding nothing missing.

There was a second safety net too. The photos already had an offsite backup, and I'd tested restoring a few old photos from it a couple of days before.

Every step had a dry run as well. Each script first writes a report, a spreadsheet with a row per file saying what it would do and why. I read through the report, and only then ran the move.

## Step 1: get iCloud down first

I downloaded both of the family's iCloud libraries onto the NAS *before* looking for duplicates, so one pass would cover everything. For that I used icloudpd (iCloud Photos Downloader), which is free and only downloads. It never deletes anything from iCloud.

It didn't go entirely smoothly:

- My laptop is an older Intel Mac, and the usual install of icloudpd includes a program built only for Apple's newer chips. Installing it from source instead fixed that.
- One account failed with "Apple iCloud setup is not complete". It turned out Apple had new iCloud terms waiting to be accepted. Signing in on the iCloud website and accepting them sorted it.

I also decided I didn't want the Live Photo clips, the two or three seconds of video an iPhone records around each picture. So the download skipped them, and the roughly 1,560 clips already on the share (4.8GB) went to `_junk`. The photos themselves are complete without them.

## Step 2: find the duplicates

Two files can only be identical if they're the same size, so the script only compares files that share a size with another file. It checks those with a quick fingerprint first, then a full checksum (SHA-256) of the whole file. The checksums are saved, so a second scan only has to read the new files.

The hard part is deciding which copy to keep. A photo in a folder called something like `Holiday April 2005` is worth more than the same photo in a camera dump, because the folder name tells you what it is. So the script ranks folders: year and named folders first, then the camera and phone folders, then the old dumps. Within the same rank, a descriptive name beats a vague one like `Hol1`.

Where the fresh iCloud downloads went in that ranking mattered. Rank them too high and 1,109 photos in named folders would have lost out to their iCloud copies. Putting them alongside the camera and phone folders kept the named ones.

Just before each move, the script checks both files are still exactly as they were when it read them. If either has changed, it compares them byte by byte again and skips them if they differ.

Once iCloud was in, it moved 50,326 spare copies, about 232GB, to `_duplicates`. Downloading iCloud had brought in a lot of photos I already had. Another 6,409 junk files (4.6GB, mostly that iPod thumbnail cache) went to `_junk`.

## Step 3: sort 20 years by date

Everything now goes into one folder per month, named `YYYY/YYYY-MM Event`, for example `2005/2005-04 Holiday`, or just `YYYY/YYYY-MM` when there's no event name.

The date comes from the one the camera recorded inside each photo (its EXIF data), read with a free tool called exiftool. The file's own date is almost useless, because copying from PC to PC over the years had reset most of them.

Real photo collections are messier than that, so the script has a few extra rules:

- **When the camera clock was wrong.** Some photos claimed to be years older than the folder they were in. If a named folder's year disagrees with the camera by more than a year, the folder wins.
- **When a photo has no date at all.** It borrows the month from the other photos in the same folder. If none of those have a date either, it reads the date from the folder name, so `Holiday April 2005` becomes 2005-04.
- **When a trip crosses the end of a month.** If all the photos in a named folder fall within 45 days, they stay together in one folder under the first month.
- **Folder names like `iPhone` or `Camera`.** They aren't events, so they don't end up in the new folder names.
- **Videos.** They go to their own share, next to our other home videos. They're copied rather than moved, each copy is checked against a checksum of the original, and the original is parked in another holding folder rather than deleted.

93% of the files had a camera date. The folder rules cut the undated files from 1,962 to 976, and in the end only 835 had no date anywhere. Those are waiting in an `_undated` folder for me to sort by eye.

## Things that bit me

**Real videos mistaken for Live Photo clips.** Some short `.mp4` videos saved from messaging apps come with a preview picture of the same name, which looks just like a Live Photo. Now only `.MOV` files count as Live Photo clips.

**The NAS says a move failed when it didn't.** Our NAS is old, and sometimes it finishes a move and then reports "No such file". Both scripts now check, and treat that as a success.

**Videos that were already in the home videos share.** About 200 old camera clips were already there, so after a full checksum check they went to `_duplicates` instead of being copied in again.

**Empty shells left behind.** Once everything had moved, the old dump folders were empty or held only clutter like `Thumbs.db`. A tidy-up command removes those, after a dry run like everything else. Another strips the pointless " (2)" that years of copying had added to file names.

## How I worked

This one was just me. The duplicate finder and the date sorter were written with Claude Code. My part was deciding what I wanted (keep the named folders, drop the Live Photo clips, never delete), reading the dry-run reports and running the moves. Each problem turned into a short request, a fix and another dry run.

## Where it's up to

The sort finished on the third day. The final scan shows 47,561 photos and videos, 226GB, all in their year and month folders, with just the 835 undated ones left over. A few days later, with nothing missing, I emptied the holding folders by hand, and that's when the space actually came back. Still to do:

- Check the next backup run succeeds. Moving files means the backup has to upload them again in their new places.
- Date the undated photos. Most are in a few named groups, so picking a year and month per folder will do.
- Near-duplicates. Checksums don't catch resized or edited copies. A photo library app planned for later can find those by how they look.
- Keep iCloud in step. Until the Pi cluster exists, that's a monthly job by hand: download the new photos, then run the same two scripts.

## What it cost

Nothing. Every tool I used is free.

## What's next

Documents: 6,000 files from old drives, down to about 540 real ones, each named from what's inside it.
