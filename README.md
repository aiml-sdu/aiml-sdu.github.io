# aiml-sdu.github.io

Website of the **Applied and Interpretable Machine Learning Research Group**, Centre for Industrial Software, Mærsk Mc-Kinney Møller Institute, University of Southern Denmark.

Live at **https://aiml-sdu.github.io**

Plain HTML and CSS. No framework and no build step. To change a page, edit its HTML file.

## Where things are

| What | File |
| --- | --- |
| Home statement, photo, latest news, the two research areas | `index.html` |
| Research overview: areas and projects | `research/index.html` |
| One research area: description, themes, people, papers | `research/<area>/index.html` |
| Publication list | `publications/index.html` |
| News | `news/index.html` (the latest four are repeated on `index.html`) |
| People | `people/index.html` |
| Positions and contact | `join/index.html` |
| All styling | `assets/css/site.css` |

The header and footer are repeated on every page. If you change one, change them on every page.

## Recipes

### A person

Copy an existing `<div class="person">` block in `people/index.html`. Leave out any line you do not have. The `id` is the surname and is what citations link to.

```html
<div class="person" id="lovelace">
  <div class="portrait"><img src="/assets/img/ada.jpeg" alt="" width="800" height="800" loading="lazy"></div>
  <p class="name">Ada Lovelace</p>
  <p class="role">PhD Fellow</p>
  <p class="line">One sentence on what you work on.</p>
  <div class="links"><a href="https://example.org">Personal Website</a></div>
</div>
```

A person's line comes from them or from a public source. If there is neither, leave it out.

### A news item

Add it to `news/index.html` under the right year, newest first. Copy it to the top of the news list on `index.html` with the year after the month (`Oct 2026`) and remove the bottom item there, so the home page keeps four.

```html
<div class="news-item">
  <div class="news-date">Oct<span class="tag">paper</span></div>
  <p class="news-text"><a href="CANONICAL RECORD">Title as the record prints it</a> accepted at Venue 2026.</p>
</div>
```

The kind label is one word: `paper`, `talk`, `joined`, `visit`, `grant`, `project`, `event`. Link member names to their card (`/people/#surname`).

### A publication

Copy the nearest `<div class="pub">` in `publications/index.html`, newest first within its section.

```html
<div class="pub">
  <div class="pub-year">2026</div>
  <div>
    <p class="pub-title"><a href="CANONICAL RECORD">Title as the record prints it</a></p>
    <p class="pub-authors">Outside Author, <a href="/people/#surname">Group Member</a></p>
    <p class="pub-meta"><span class="venue">Venue</span> volume, pages</p>
  </div>
</div>
```

Sections:

- **Peer-reviewed**: journals, conferences and named workshops.
- **Preprints**: the venue is the arXiv identifier, e.g. `arXiv:2605.10601`.
- **Earlier work**: papers written before the authors joined the group, such as Toygar Tanyel's clinical and language papers and Serkan Ayvaz's work from before he came to SDU in August 2023. A paper done in the group goes in the sections above, whoever wrote it.

Citation rules:

- Every author, in the record's order, with full first names. No `et al.`
- Group members (anyone with a card on the people page) are links. Nobody is bold.
- The title links to one record: DOI first, then arXiv, then OpenReview. No record, no link.
- `.tag` marks a distinction only, such as `oral`.
- No citation counts or other metrics.

If the paper belongs to a research area, also add it to the Papers list on that area's page (`research/interpretability/` or `research/structured-data/`) and update the paper count on `research/index.html`. The copies are not checked against each other, so when a paper's status changes, edit all of them.

### A research area or project

Each area has its own page under `research/`, with the same four parts: a short description, themes, people and papers. To add an area, copy an area directory, change its text, and add a block for it on `research/index.html`. Describe an area by its field and questions, not by single papers. Projects are listed on `research/index.html` with their years.

### A photograph

Crop it before adding it (portraits square), keep it under 1.5 MB, put it in `assets/img/`, and give the `<img>` its real `width` and `height`. A photograph that is not ours carries its credit and licence in the caption, as the one on the home page does.

## Before you open a pull request

```bash
python3 -m http.server 8000      # then open http://localhost:8000
python3 .github/scripts/check_site.py
```

Use the server, not Finder: every path starts from the site root. The check catches unclosed tags, links and `#fragments` that do not resolve, missing images, oversized images and paths without a leading slash. The same check runs on every pull request.

## How a change reaches the site

`main` is what is published, so nothing is pushed to it directly.

1. Branch: `git switch -c people-add-ada`
2. Commit and push
3. Open a pull request
4. The check runs and one other person reads it
5. Merge. The site updates in about a minute.

## Rules

- **Paths start from the site root**: `/assets/img/x.jpg`, never `assets/img/x.jpg` or `../`.
- **Pages are directories**: `/research/` is `research/index.html`.
- **Colours clear WCAG AA.** The ratios are at the top of `site.css`; re-check if you change a colour.
- **No placeholders on the live site.** `class="todo"` marks unfinished text and should not be merged.
- **The favicon is cached hard.** If you change it, change its filename too, in every page's `<link>` and in `assets/js/theme.js`.
- **`work/`** holds redirect stubs for old study addresses. The check verifies their targets.
- **Research areas have no numbers.** They are named, not ranked.

## Design

Two typefaces: Newsreader for reading, IBM Plex Mono for navigation, labels and dates. Warm paper and ink with no accent colour, light and dark themes, one centred reading column. The mark in `assets/img/mark.svg` is applied as a CSS mask, so it takes the text colour of either theme.
