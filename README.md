# Waisman Lab website

Source for the Waisman Lab public website, built with [Jekyll](https://jekyllrb.com)
for native [GitHub Pages](https://pages.github.com) hosting at
`https://waismanlab.github.io`.

The site is currently a **skeleton**: every page, template, and content type
works end to end, but text and images are placeholders clearly marked with
`[PLACEHOLDER]`. Nothing here should be treated as final scientific content.

## 1. What this is

A static, editorial-style lab website (Home, Research, People, News,
Publications, Resources, About). No JavaScript framework, no build step beyond Jekyll's own
Markdown/Sass compilation — content lives in Markdown and YAML, presentation
lives in `_layouts`/`_includes`/`_sass`, so day-to-day edits never touch HTML.

## 2. Run it locally

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`. Jekyll rebuilds automatically as you edit
files (front matter changes may need a restart).

Requires Ruby + Bundler. If you don't have them, see
[GitHub Pages' Ruby setup guide](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll).

**Ruby version note:** the `github-pages` gem pins an older Jekyll/Liquid
stack that doesn't run on macOS's built-in system Ruby (too old) or on the
very latest Ruby from Homebrew (too new — some standard-library gems were
split out and old Liquid versions break on Ruby 3.2+). Ruby 3.1–3.3 is the
sweet spot. If `bundle install`/`jekyll serve` fails on your machine, install
one with Homebrew, e.g.:

```bash
brew install ruby@3.1
export PATH="/opt/homebrew/opt/ruby@3.1/bin:$PATH"   # add to your shell profile
gem install bundler
bundle install
bundle exec jekyll serve
```

## 3. How GitHub Pages deployment works

This repo is a **user/org page** (`waismanlab.github.io`), so GitHub Pages
publishes automatically from the `main` branch — no CI config needed. It
builds the site with the `github-pages` gem (the same one pinned in the
`Gemfile`), so anything that works with `bundle exec jekyll serve` locally
will work once pushed. Just push to `main` and the live site updates within
a minute or two.

## 4. Editing the homepage

- Hero text/tagline: pulled from `_config.yml` (`title`, `tagline`) plus the
  intro paragraph in [`_includes/hero.html`](_includes/hero.html).
- The two research theme cards: edit copy in [`_data/research.yml`](_data/research.yml)
  (`home_summary` for the homepage blurb, `research_summary` for the full
  `/research/` text) — the same file drives both pages.
- "Selected Research": automatically shows the first publication tagged
  `category: waisman-lab` (see §7).
- Section order/structure lives in [`_layouts/home.html`](_layouts/home.html)
  if you ever need to rearrange things.

## 5. Adding or editing a lab member

Each person is one file in [`_people/`](_people). Copy an existing file
(e.g. `_people/05-undergraduate-student.md`), rename it, and edit the front
matter:

```yaml
---
name: "Jane Doe"
role: PhD Student
order: 6
status: current      # or "alumni"
photo: /assets/images/people/jane-doe.jpg
bio: >-
  One or two sentence bio / project description.
email: "jane@example.com"
orcid: "https://orcid.org/0000-0000-0000-0000"
scholar: "https://scholar.google.com/..."
linkedin: "https://linkedin.com/in/..."
github: "https://github.com/..."
---
```

**Only include the optional fields you actually have** (`email`, `orcid`,
`scholar`, `linkedin`, `github`, `photo`, `bio`) — leaving a field out
entirely hides it from the card. Setting it to an empty string still shows
a broken link, so delete unused lines rather than blanking them.

`order` controls display order. Set `status: alumni` to move someone into
the Alumni section on `/people/` (it only appears once someone has that
status).

**Giving someone a detailed profile page** (currently used for the PI's
CV): add `profile_url: /people/pi/` (or any path you choose) to that
person's front matter — their name on `/people/` automatically becomes a
link, and a "Full CV →" link appears in their card. The page itself is a
normal top-level Markdown file (see [`pi.md`](pi.md)) using `layout: page`,
so its body is just Markdown headings/paragraphs. To add a similar page for
someone else, copy `pi.md` to a new file with its own `permalink:`, then
point that person's `profile_url` at it.

**Team photos**: below the individual cards, `/people/` also shows a small
grid of group photos, driven by [`_data/team_photos.yml`](_data/team_photos.yml).
Add or remove `{ image, caption }` entries there — no HTML editing needed.
The section disappears automatically if the list is empty.

## 6. Adding a news item

Each news item is one file in [`_news/`](_news). Copy an existing file and
edit the front matter:

```yaml
---
date: 2027-03-10
title: "Interview on regional radio about stem cell research"
category: Interview        # optional, e.g. Award, Interview, Talk, Media
description: >-
  Optional one or two sentence description.
link: "https://..."        # optional
link_label: "Read the interview →"   # optional, defaults to "Read more →"
---
```

Items are sorted newest-first automatically by `date` — no need to keep
files in order yourself. Only include `link`/`link_label` if you have
somewhere to point to.

## 7. Adding a publication

Each publication is one file in [`_publications/`](_publications). Copy an
existing file and edit the front matter:

```yaml
---
category: waisman-lab        # or "previous-research"
research_area: maturation    # optional: "maturation" or "regeneration" —
                              # links it under that section on /research/
order: 2
title: "Paper title"
authors: "Doe J, Roe R, et al."
journal: "Journal Name"
year: 2027
description: >-
  Optional one-sentence description.
doi: "https://doi.org/..."
pubmed: "https://pubmed.ncbi.nlm.nih.gov/..."
preprint: "https://..."
code: "https://github.com/..."
data: "https://..."
image: /assets/images/publications/paper-slug.jpg
---
```

Again, only include the fields you have — an empty string still renders an
(empty) link, so omit rather than blank a field. `category` decides which
section of `/publications/` the entry appears under; `waisman-lab` entries
also become eligible for the homepage "Selected Research" spot.

## 8. Replacing images

All images live under `assets/images/`, organized by section. Every current
file is a labeled SVG placeholder — open one in a browser to see exactly
what it's standing in for.

| Replace this file | With |
|---|---|
| `assets/images/hero/hero-lab.svg` | Homepage hero image |
| `assets/images/research/research-maturation.svg` | Maturation theme image |
| `assets/images/research/research-regeneration.svg` | Regeneration theme image |
| `assets/images/people/person-placeholder.svg` | Default portrait (or add a per-person photo and set `photo:` in that person's file) |
| `assets/images/institutions/fleni-logo-placeholder.svg` | FLENI logo |
| `assets/images/institutions/ineu-logo-placeholder.svg` | INEU logo |
| `assets/images/institutions/conicet-logo-placeholder.svg` | CONICET logo |
| `assets/images/publications/publication-placeholder.svg` | Reusable publication thumbnail |

Easiest approach: add your real `.jpg`/`.png` file into the same folder,
then update the relevant path in `_data/research.yml`, `_data/institutions.yml`,
or the person's/publication's front matter (`photo:` / `image:`) to point at
the new file. You don't have to reuse the old filename.

**Format**: JPEG for photos/microscopy images (hero, research, people,
publications); PNG (transparent background) for institution logos, unless
you have a true vector logo file, in which case SVG.

**Size and resolution**: every image slot on the site is a fixed-size box
that uses CSS `object-fit: cover`, which center-crops whatever you give it
to fill the box — the source file's exact dimensions/aspect ratio don't
need to match, they just get cropped. So two things matter more than exact
pixel dimensions: providing enough resolution to stay sharp, and keeping
your subject centered (since cropping always happens from the center, an
off-center subject can get clipped differently on desktop vs. mobile).

| Image | Box shape | Minimum recommended size |
|---|---|---|
| Hero (`hero.html`) | full width × up to 640px tall | ~2400px wide, landscape |
| Research theme images | 4:3 | ~1600×1200px |
| People portraits | square (1:1) | ~800×800px, subject centered |
| Publication thumbnails | small square | ~400×400px |
| Institution logos | small, uncropped | ~200–400px, transparent background |

Keep exported file sizes reasonable for page speed — JPEG quality ~75–85%,
aiming for under ~400–500KB per photo.

## 9. Editing navigation

Top nav links live in [`_data/navigation.yml`](_data/navigation.yml) — add,
remove, or reorder entries there. No HTML editing required.

## 10. Institutional / contact information

- Institution names + logos: [`_data/institutions.yml`](_data/institutions.yml)
  (used in the homepage footer and the About page).
- PI name, contact email, location, GitHub org link, Google Scholar link:
  top of [`_config.yml`](_config.yml).

## Architecture at a glance

```
_config.yml           Site metadata + contact info
_data/                navigation.yml, research.yml, institutions.yml, team_photos.yml
_people/              One file per lab member (collection, output: false)
_publications/        One file per publication (collection, output: false)
_news/                One file per news item (collection, output: false)
pi.md                  Standalone detailed profile page (PI's CV, linked from /people/)
_layouts/              Page templates (default, home, page, research, people, publications, news)
_includes/              Reusable components (header, footer, hero, cards, news-entry, team-photos)
_sass/, assets/css/    Styling (Sass partials compiled by Jekyll)
assets/js/main.js       Mobile nav toggle (the only JS on the site)
assets/images/           Placeholder images, organized by section
```
