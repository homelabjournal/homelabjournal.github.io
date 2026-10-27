# Home Lab Journal

The blog about our home lab, at https://homelabjournal.com. Posts are Markdown files in `docs/posts/`, built with MkDocs Material and published to GitHub Pages by `.github/workflows/publish.yml` on every push to `main`.

## Writing a post

Write in the first person: "I" is me (dad), "we" is the two of us, and he is "my son".

1. Copy an existing file in `docs/posts/` and change the front matter: `date`, `categories`, and keep `draft: true` until it's ready.
2. Put a `<!-- more -->` line after the first paragraph: everything above it is the summary on the front page.
3. Preview: `pip install -r requirements.txt`, then `mkdocs serve` and open http://127.0.0.1:8000 (drafts show when previewing).
4. When it's ready, remove `draft: true`, run through the checklist below, and push.

Images go in `docs/posts/images/` (JPEG or PNG, under about 500KB each).

## Before publishing: the checklist

The repo is public, so drafts are visible to anyone who looks. Nothing here should ever help someone find or get into the house.

- [ ] No names, faces, school, location or anything that identifies the family. "Dad" and "my son" only.
- [ ] No IP addresses, port numbers that are open to the internet, network or VLAN maps of the real house, Wi-Fi names, MAC addresses, serial numbers, or domain names of home services.
- [ ] Screenshots checked and cropped: browser address bars, terminal prompts (user and host names), router and NAS pages, and photo EXIF location data (strip it).
- [ ] No passwords, keys, tokens or config files, even "redacted" ones.
- [ ] Explain how and why, not our exact configuration.
- [ ] Both of us are happy with it.

## Staying faceless on GitHub

The repo is public, so nothing in it may point back to us:
- It lives under its own GitHub **organisation** (`homelabjournal`), not a personal account, with members hidden.
- Commits use the blog's own name and address, set in this repo only: `git config user.name "Home Lab Journal"` and `git config user.email "blog@homelabjournal.com"`. Check with `git log --format='%an <%ae>'` before the first push.

## Publishing set-up (done once)

1. GitHub: create a free organisation called `homelabjournal`, set your membership to private (Organisation → People), and create a **public** repo `homelabjournal.github.io` in it. Push this repo there.
2. In the repo: Settings → Pages → Source: **GitHub Actions**. Custom domain: `homelabjournal.com`.
3. In Cloudflare, DNS for `homelabjournal.com`, all set to **DNS only** (grey cloud), so GitHub can issue the certificate:
    - `A` records for `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
    - `AAAA` records for `@`: `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`
    - `CNAME` `www` → `homelabjournal.github.io`
4. Back in Settings → Pages, once the DNS check passes, tick **Enforce HTTPS**.
5. Organisation → Settings → Pages → **Add a domain** to verify `homelabjournal.com` (a TXT record in Cloudflare), so no one else can claim it on GitHub.
