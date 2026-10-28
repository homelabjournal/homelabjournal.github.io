---
description: How I found and set aside over 50,000 duplicate photos and videos, then sorted 20 years of family pictures into folders by date, without letting a script delete anything.
date: 2026-11-05
authors: [lab]
categories: [Foundations]
draft: true
---

# Photos: 50,000 duplicates, then 20 years sorted by date

Our family photos lived on the NAS, in theory. In practice they were spread across year folders, camera dumps, phone dumps and copies of old laptops, often several times over. Over three days I set aside more than 50,000 spare copies and sorted everything that was left into one folder per month, with two scripts written by Claude and one rule: no script ever deletes anything.

<!-- more -->

## The mess

The photo share had grown the way these things do. There were year folders, plus a folder for each camera and phone that had ever been plugged in, and some of those had also been copied into the year folders. Then I copied in everything from old PCs, an old hard drive and an old laptop, so it was all in one place before I started.

Before changing anything, I surveyed the lot from the laptop, reading only. It found:

- **36,946 files, 171GB:** about 33,700 JPEGs, 2,200 videos (75GB of the total) and a few hundred iPhone photos.
- **About 11,000 exact copies, 52GB,** found by comparing what's inside the files, not their names. Half of that space was videos, with the same clips in two camera folders and a year folder.
- **Junk:** hundreds of thumbnail caches from an old iPod and Apple TV, which look like photos but aren't, plus old photo-library leftovers and 14 zip files whose photos were all already on the share.

And that was before the newest photos. Almost everything since 2018 only existed in iCloud.

## The rule: nothing is deleted by a script

Deleting the wrong copy of a family photo is the one mistake I couldn't undo, so the scripts never delete. They *move* things into holding folders, `_duplicates` and `_junk`, keeping each file's original folder path, and they write a log of every move so a single command can put everything back. I empty the holding folders by hand, after a week of using the library and finding nothing missing.

There was a second safety net underneath: the photos already had an offsite backup, and I'd tested restoring a few old photos from it a couple of days before.

Every step also had a dry run. Each script first writes a report, a spreadsheet with one row per file saying what it would do and why. I looked through the report, and only then ran the move.

## Step 1: get iCloud down first

I downloaded both of the family's iCloud libraries onto the NAS *before* looking for duplicates, so one pass would cover everything. The tool was **icloudpd** (iCloud Photos Downloader), which is free and only ever downloads; it never deletes anything from iCloud.

Two snags:

- **My laptop is an older Intel Mac,** and the usual install of icloudpd includes a program built only for Apple's newer chips. Installing it from its source code instead fixed that.
- **One account failed with "Apple iCloud setup is not complete".** It turned out Apple had new iCloud terms waiting. Signing in on the iCloud website and accepting them fixed it.

I also decided I didn't want Live Photo clips, the two or three seconds of video an iPhone records around each picture. So the download skipped them, and the roughly 1,560 clips already on the share (4.8GB) went to `_junk`. The still photos are complete without them.

## Step 2: find the duplicates

Two files can only be identical if they're the same size, so the script only compares files that share a size with another file. It checks those with a quick fingerprint first, then a full checksum (SHA-256) of the whole file. The checksums are saved, so running the scan again only reads new files.

The interesting part is deciding **which copy to keep.** A photo in a folder called something like `Holiday April 2005` is worth more than the same photo in a camera dump, because the folder name tells you what it is. So the script ranks folders: year and named folders first, then the camera and phone folders, then the old dumps. Within a rank, a descriptive folder name beats a vague one like `Hol1`. Where to put the fresh iCloud downloads mattered: rank them too high and 1,109 photos in named folders would have lost to their iCloud copies. Ranking them alongside the camera and phone folders kept the named ones.

Just before each move, the script checks that both files are still exactly as they were when it read them. If either has changed, it compares them byte by byte again, and skips them if they differ.

The result, once iCloud was in: **50,326 spare copies, about 232GB,** moved to `_duplicates`. Downloading iCloud had brought in a lot of photos I already had. Another **6,409 junk files** (4.6GB, mostly that iPod thumbnail cache) went to `_junk`.

## Step 3: sort 20 years by date

Everything now goes into one folder per month, named `YYYY/YYYY-MM Event`, for example `2005/2005-04 Holiday`, or just `YYYY/YYYY-MM` when there's no event name.

**Where the date comes from:** the date the camera recorded inside each photo (its EXIF data), read with the free tool **exiftool**. The file's own date is almost useless, because copying from PC to PC over the years had reset most of them.

Real photo collections are messier than that, so the script has a few rules:

- **The camera clock was wrong.** Some photos claimed to be years older than the folder they were in. If a named folder's year disagrees with the camera by more than a year, the folder wins.
- **The photo has no date at all.** It borrows the month from the other photos in the same folder. If none of them has a date either, it reads the date from the folder name, so something like `Holiday April 2005` becomes 2005-04.
- **A trip that crosses a month end stays together.** If all the photos in a named folder fall within 45 days, they go to one folder under the first month.
- **Folder names like `iPhone` or `Camera` aren't events,** so they don't end up in the folder names.
- **Videos go to their own share,** next to our other home videos. They're copied rather than moved, each copy is checked against a checksum of the original, and the original is parked in another holding folder rather than deleted.

**93% of the files had a camera date.** The folder rules cut the undated files from 1,962 to 976, and in the end only **835** had no date anywhere. Those wait in an `_undated` folder to be sorted by eye.

## Things that bit me

- **Real videos taken for Live Photo clips.** Some short `.mp4` videos, saved from messaging apps, come with a preview picture of the same name, which looks exactly like a Live Photo. Only `.MOV` files count as Live Photo clips now.
- **The NAS says a move failed when it didn't.** Our NAS is old, and it sometimes completes a move but then reports "No such file". Both scripts now check, and treat that as a success.
- **Videos already in the home videos share.** About 200 old camera clips were already in the home videos share, so they went to `_duplicates` instead of being copied in again, after a full checksum check.
- **Leftovers.** Once everything had moved, the old dump folders were empty shells, so a tidy-up command removes empty folders (or ones holding only clutter like `Thumbs.db`), after a dry run like everything else. Another removes the needless " (2)" that years of copying had added to file names.

## Built with Claude Code

This one was just me, working with Claude. As with everything in this lab, **Claude wrote all the code**: the duplicate finder, the date sorter, and every fix above. My part was deciding what I wanted (keep the named folders, drop the Live Photo clips, never delete), reading the dry-run reports, and running the moves. Each of the snags became a short request, a fix, and another dry run.

## Where it's up to

The sort finished on the third day. The final scan shows **47,561 photos and videos, 226GB, all in their year and month folders,** with just the 835 undated ones left. Still to do:

- **Check the next backup run succeeds.** Moving files means the backup uploads them again in their new places.
- **Empty the holding folders** after a week of using the library with nothing missing. That's when the space actually comes back.
- **Date the undated photos.** Most are in a few named groups, so a year and a month per folder will do.
- **Near-duplicates.** Checksums don't catch resized or edited copies. A photo library app planned for later can find those by how they look.
- **Keep iCloud in step.** Until the Pi cluster exists, that's a monthly job by hand: download the new photos, then run the same two scripts.

## What it cost

Nothing. Every tool I used is free.

## What's next

Documents: 6,000 files from old drives, down to about 540 real ones, each named from what's inside it.
