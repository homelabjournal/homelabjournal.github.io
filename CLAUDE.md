# Home Lab Journal

The blog at https://homelabjournal.com: a dad and his teenage son build a home lab, one phase at a time, with AI doing all the coding. MkDocs Material, published to GitHub Pages by `.github/workflows/publish.yml`.

**This repo is public.** Everything in it, including this file, drafts and commit messages, can be read by anyone.

## Hard rules

- **Faceless.** No names, faces, school, employer, town, or anything that identifies the family. "I" is the dad, "we" is the two of us, and he is "my son" (a teenager; no age). Say "30-odd years of coding", never anything about the dad's career.
- **Nothing that helps anyone into the house:** no IP addresses, open ports, real network or VLAN maps, Wi-Fi names, MAC or serial numbers, hostnames or domain names of home services, provider or council names, station names, or exact device models that pin the house down. Explain how and why, not our exact config.
- **Never link this blog to the dad's other public work** (his personal GitHub account, other projects or sites) or to the private lab repo.
- **Commits** use the blog identity set in this repo's git config: `Home Lab Journal <blog@homelabjournal.com>`. No session links or personal trailers in commit messages.
- **Honest about AI, from the start.** The plan was written with Claude; the code is written **with** Claude Code (Claude writes it, driven by our spec, feature requests and brainstorming, and we may tweak it); posts are drafted by Claude from our notes and edited by us. Say "with Claude", not "by Claude", for code from now on. Never imply we wrote the bulk of it by hand. **But AI is not the focus:** mention it briefly where it matters (usually one short paragraph, no "Built with Claude" headings), and keep the post about what we built and learned.
- **Only write what happened.** Draft from the facts we give you, and ask when unsure (who did what, how long it took, what broke). Don't invent anecdotes.
- **First person, plain British English,** friendly and specific. Short paragraphs, bold lead-ins, lists where they help.

## Publishing

- **Two or three posts a week while catching up** (spaced a day or two apart), then as things happen. Never more than one a day. New posts are `draft: true` until the dad says publish. To queue one, give it a future `date` and remove `draft: true`: future-dated posts stay hidden (and out of the RSS feed), and the daily 07:00 UTC rebuild publishes them on their date.
- **Instagram goes out with the blog.** Each post gets a carousel on @homelabjournal on the same day it publishes (five hashtags at most: Instagram's limit). The carousels themselves live outside this repo.
- Every post has `date`, `authors: [lab]`, `categories`, and a one-sentence `description` (for search results and link previews), plus a `<!-- more -->` after the opening paragraph.
- Run the privacy checklist in `README.md` before publishing.
- Check the build with `mkdocs build --strict` before pushing (`pip install -r requirements.txt`).

## Series order

Posts follow the order things were actually done:

1. Why we're building a home lab (published 27 Oct 2026)
2. Pi-hole on a 2012 Raspberry Pi (published 28 Oct 2026)
3. The kitchen dashboard on an iOS 12 iPad (draft, dated Mon 2 Nov)
4. Tidying up the NAS: locking it down, accounts, health checks, space, layout and backups (draft, dated Wed 4 Nov)
5. Photos: finding and removing 50,000 duplicates, then sorting 20 years of pictures by date (draft, dated Fri 6 Nov)
6. Documents: 6,000 files from old drives down to about 540, named from their contents with OCR (planned for Mon 9 Nov)
7. The rack tidy, with before and after photos (when it's done)
8. Then the firewall, the Pi cluster and the rest of the plan, as they happen

## Site features

- RSS: `feed_rss_created.xml` (mkdocs-rss-plugin).
- Visitor stats: Cloudflare Web Analytics, via `extra.cloudflare_analytics_token` and `overrides/main.html`. No cookies.
- Google Search Console is verified and has the sitemap. Bing Webmaster Tools: not yet (import from Google when wanted).
