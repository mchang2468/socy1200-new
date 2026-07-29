# SOCY 1200 — Course Materials Site

Static materials index for *Introduction to Using AI to Study Society* (Yale, Daniel Karell).
No build step, no dependencies. Everything renders from one data array in `index.html`.

---

## Deploy

```bash
git init
git add .
git commit -m "Course materials site"
git branch -M main
git remote add origin https://github.com/USERNAME/socy1200.git
git push -u origin main
```

Then: **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)` → Save.**

Live in about a minute at `https://USERNAME.github.io/socy1200/`.

To publish at `https://USERNAME.github.io/` instead, name the repo `USERNAME.github.io`.

---

## Do not delete `.nojekyll`

GitHub Pages runs Jekyll by default, and **Jekyll silently ignores every file and folder
whose name starts with an underscore.** xaringan decks knit to `deckname_files/` — that's
where all the CSS, JS, and remark.js live. Without `.nojekyll`, your decks deploy as
unstyled text with no keyboard navigation, and the build log reports success.

The empty `.nojekyll` file in the repo root turns Jekyll off. It has no other effect.

---

## What's actually in here right now

**Slides only** — all 13 real decks (`slides/week1_v3.html` … `week15+16_v3.html`),
rendered xaringan HTML plus the shared `libs/`, `yale.css`, and `yale-fonts.css` they
depend on. Weeks are grouped into the five real units pulled from each deck's own YAML
subtitle (Introduction; Prompting, with Application to Measurement; Synthetic People; AI
in Experiments; AI and Society), with the midterm and final review decks (weeks 8–9 and
15–16) shown as their own entries. There's no week 9 or 13 deck, so the schedule skips
them — that matches what was uploaded, not a bug.

Article PDFs are no longer hosted on the site. The `readings/` folder is kept as an empty
placeholder (just a `.gitkeep`) in case you want to reintroduce readings later — as local
files, or, better for a public repo, as links to DOIs or a library permalink instead.

## Re-adding readings later

To attach a reading to a specific week, add it to that week's `materials` array:

```js
{ n:7, dates:"Week 7", title:"Limitations and Potential Solutions", materials:[
  {type:"slides",  label:"Week 7 — Limitations and Potential Solutions",
   sub:"Unit 3: Synthetic People", ext:"HTML", url:"slides/week7_v3.html"},
  {type:"reading", label:"Argyle (2023) — Out of one, many: using language models to simulate human samples",
   sub:"Political Analysis", ext:"PDF", url:"readings/argyle_simulate_2023.pdf"},
]},
```

`type` must be `slides` or `reading` to pick up existing badge styling (or `assignment`,
`data`, `code` — the CSS for those is still in the stylesheet if you add problem sets or
datasets later). `CURRENT_WEEK` above the `UNITS` array controls the amber "This week"
highlight; set it to `0` over breaks.

**Keep every path relative.** A project page is served from `/socy1200/`, so a leading
slash (`/slides/week07.html`) resolves to `USERNAME.github.io/slides/...` and 404s.

---

## Still to fill in

- Five nav links marked `data-placeholder` (Syllabus, Canvas, Ed Discussion, and the four
  "→" links in the Logistics cards). They currently no-op on click. Add real `href`s and
  delete the `data-placeholder` attribute.
- The one remaining `url:"#"` — week 13's Salganik chapter, which links out to an external
  site rather than a file you host.
- Week topics, dates, and readings are plausible placeholders, not your actual syllabus.

---

## If you add readings back

Same caveat as before: a GitHub Pages site is public and indexed, which is a different
kind of exposure than posting a PDF behind Canvas authentication — publishers do issue
takedowns over exactly that. If you reintroduce paywalled articles, the low-friction move
is to point `reading` entries at DOIs or Yale library permalinks instead of local PDFs.
Yale's library staff can generate persistent proxied links that authenticate students
automatically.
