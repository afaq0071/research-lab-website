# NEXA Research Lab — Website Restructure Report

**Date:** 08 Aug 2026
**Scope:** Session covering the restructure of `D:\research-lab` to mirror the RARL lab site structure and replace placeholder artwork with real photos.

---

## 1. Objective

1. Restructure the existing 9-page NEXA Research Lab website so its **page layout mirrors https://rarl-lab.com/** while keeping original NEXA branding and content (no copying of RARL text/branding — structure only).
2. Replace the generated SVG placeholder images with **real photo images stored locally** in the project.

## 2. What was done

### 2.1 Real photo downloads (51 images)
- Downloading via `Invoke-WebRequest` and `curl.exe` was **blocked in this environment** (empty `0-byte` files / `spawn EPERM`).
- Downloads succeeded via **Python `urllib`**.
- **51 real JPEG photos** were downloaded into `images/real/`:
  - Keyword-matched from LoremFlickr (robot, laboratory, technology, portrait, award, meeting, conference, poster, community, building, etc.), with deterministic `?lock=` seeds and Picsum fallback.
  - Coverage: home hero, about cards, news thumbnails, achievements, 9 team portraits + group shot, awards (6), collaborations (6), lab posters (6), gallery (6), membership (2), campus (1).
- Unused test files (`test.jpg`, `test2.jpg`) and one unused photo (`news6.jpg`) were removed.

### 2.2 Navigation & footer (js/main.js)
- **Nav updated to the RARL page set:**
  Home · Team · News · Awards · Collaborations · Lab Posters · Gallery · Contact · Membership.
- Footer rebuilt: Navigate / Engage / Membership / Contact columns.
- Brand subtitle changed to **"Robotics & Automation Research"**.
- Fixed a real JS syntax error (mismatched closing quote in a footer string, caught by esprima).

### 2.3 Home page (index.html) — rebuilt to RARL layout
1. Announcement bar (gradient, membership CTA)
2. Hero (lab name + mission, real robot photo, floating stat chips)
3. Welcome / about preview (intro + 3 photo cards: Publications, Mentorship, Innovation)
4. Stats band (120+ publications, 40+ researchers, 12+ patents, 8 books)
5. Recent achievements (4-photo grid)
6. Latest news (3 photo cards)
7. Featured publications (3 entries + "View all")
8. Get in Touch (Location / Phone / Email / Hours cards) + membership CTA band

### 2.4 Pages (pages/)
- **Team** — real portraits (team-1 … team-9), group photo hero, alumni badges, membership CTA.
- **News** — featured story + 6 recent updates, all with real thumbnails.
- **Awards** *(new)* — hero photo + 6 award cards + CTA.
- **Collaborations** *(new)* — partnership models + 6 partner-programme cards + CTA.
- **Lab Posters** *(new)* — 6 poster cards (portrait ratio) with download buttons + CTA.
- **Gallery** *(new)* — 6 photo cards with captions + visit CTA.
- **Membership** *(new)* — benefits, 3 membership types, 4-step apply process, FAQ accordion.
- **Contact** — real hero/hero map photos, info rows + demo contact form.

### 2.5 Housekeeping
- **Archived superseded pages** (`about.html`, `research.html`, `careers.html`, `resources.html`) to `_legacy\new-pages\`.
- Fixed the last stale link to the removed pages (publications → resources link repointed).
- Added small CSS additions: announcement bar styles and `thumb-poster` / `thumb-portrait` aspect utilities.

## 3. Verification (all passed)
- **124 local links** resolve (HTML + CSS + JS + images).
- **Tag balance** clean on all 10 HTML pages.
- **JS syntax** validated with esprima (parses OK).
- **Smoke test:** local server (`127.0.0.1:8901`) returned **200 for all 67 URLs** (10 pages, CSS, JS, brand SVG, 51 real images) — zero failures, no empty assets.
- **No unused image files** remain in `images/real/`.

## 4. Current structure

```
D:\research-lab\
├── index.html              (home — RARL-style layout)
├── css\style.css           (design system, light/dark, responsive)
├── js\main.js              (shared header/footer, theme, animations, filters)
├── images\
│   ├── brand.svg
│   ├── *.svg               (legacy placeholders, no longer referenced by pages)
│   └── real\               (51 real photos used across the site)
├── pages\
│   ├── team.html  news.html  awards.html  collaborations.html
│   ├── lab-posters.html  gallery.html  membership.html
│   ├── contact.html  publications.html
└── _legacy\                (archived old Bootstrap site + superseded new pages)
```

## 5. Notes / next steps
- Team portraits are **real Flickr photos used as placeholders** — replace with the actual team's headshots before launch.
- The contact form is a **demo** (no backend).
- Social links and "PDF / Load More" buttons are placeholders (`#`).
- Preview: `python -m http.server 8901` from `D:\research-lab`.
