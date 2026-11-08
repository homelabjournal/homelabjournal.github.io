---
description: How nearly 7,000 files from old drives and laptops came down to about 540 real documents, each named from what's inside it, plus the simple habit that keeps them tidy now.
date: 2026-11-11
authors: [lab]
categories: [Foundations]
draft: true
---

# Documents: nearly 7,000 files down to 540

Our family paperwork was spread across an old desktop's hard drive, an old laptop, an old external drive, the Mac and, oddly, the photos share. Over a few days I brought it all onto the NAS, threw out what wasn't a document, and filed what was left into one share, with every file named from what's actually inside it.

<!-- more -->

This was the last big job in the NAS tidy-up, and like the photos, it was just me.

## Copy first, sort later

The order mattered more than anything else: **copy everything first, untouched, then remove duplicates, then sort.** Sorting straight off an old drive is asking for trouble. If it dies halfway through, whatever you hadn't copied yet is gone.

So each source went into its own folder in an inbox on the NAS, named after where it came from and when, and the old drives stayed as they were until the filing was done. I kept a checklist of every place old documents might be hiding: drives, laptops, USB sticks, SD cards, cloud accounts, email attachments and the filing cabinet. A source only came off the list once it was copied or I'd checked it had nothing left to give.

Five sources had something worth copying. Together that was **6,981 files, 7.1GB.**

## Most of it wasn't documents

Once it was all in one place, the real picture was clear:

- **About 6,100 files were software, not paperwork:** old code projects, a copy of an old website, data from old programs, and installers. They went to a `_junk` folder.
- **145 course videos (5.9GB)** had been sitting with the documents. They moved to the media share, where the rest of the videos live.
- **59 exact copies,** found by comparing contents rather than names.

That left **about 540 real documents.**

## Naming them from what's inside

A folder full of `Scan0042.pdf`, `Document1.docx` and `letter final FINAL.doc` isn't much use, so every document got a name in one style:

`YYYY-MM Description`, for example `2026-03 Council tax bill 2026-27.pdf`.

The month is the document's own date, the one on the letter or statement, not the day it was saved. The description says what it is and who it's from, in plain words. And **no account, policy or ID numbers ever go in a name.** They stay inside the document.

To work out the date and what each file was, the text was read from every one: straight out of PDFs and Word files, and with OCR (reading the words out of an image) for scans and photos of letters. Claude Code went through them and suggested a name and a folder for each in a plan, a spreadsheet with one row per file. I read the whole plan and corrected it before anything moved.

A few files weren't what they claimed to be. One `.doc` was really a PDF, and another turned out to be a zip of photos. Those were renamed to match what they actually were.

## Where it all lives

The share has a short list of top-level folders and no others: Family, Finance, House, Car and transport, Identity and certificates, Legal, Travel, Work, Study and Archive. A subject gets its own sub-folder once it has about five documents.

Moving the files worked the same way as the photos: a script carried out the plan I'd checked, wrote an undo log, and deleted nothing. Once I was happy, I emptied the holding folders myself and deleted the plan too, because a list of the family's document names is sensitive in itself.

## Backed up, encrypted

The documents are the most sensitive files we have, so their offsite backup is set up differently from the photos:

- **Encrypted on the NAS** before anything leaves the house, with the key kept in our password manager.
- **Daily, keeping 30 versions,** so a file that gets changed or overwritten can be got back.
- **Its own storage and its own login,** which can reach nothing else.

I tested it the same day by restoring a PDF and a scan to a separate folder and opening them.

## Keeping it tidy

The round-up was a one-off. The hard part is stopping it from turning back into a mess, so there's now one simple rule: **everything new goes into the inbox, never straight into a folder.**

- **From a phone or away from home,** it goes into an inbox folder in iCloud Drive. Every hour, while the Mac is at home and awake, a small job moves it onto the NAS.
- **Paper** gets scanned with the iPhone and then shredded, unless it's an original that matters, like a certificate or a will.
- **Email attachments** get saved as the PDF, not a screenshot.

When a few things have built up, the same script reads what's in the inbox and suggests a folder and a name for each file, and I check its suggestions before it moves anything. It also has a health check that flags anything that's drifted from the house style: loose files, odd folders, names without a date, names with long numbers in them, duplicates, and an inbox that's been sitting too long.

There's no yearly clear-out. Documents are small, so we keep everything.

## Where it's up to

Done: every source is ticked off, the inbox is empty and the backup is running. Still to come:

- **A monthly job on the Pi cluster,** once it exists, that plans the inbox and runs the health check, then posts a summary to Discord. That's earmarked as a good first coding job for my son.
- **Proper search** over all of it later, with a document app that reads every scan and lets you search for "council tax 2023".

## What it cost

Nothing to buy. The encrypted backup adds a little to the monthly offsite bill.

## What's next

The rack tidy, with before and after photos.
