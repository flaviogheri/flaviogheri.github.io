# Website Revamp Plan

A working document to plan the improvements to the portfolio site. The goal is to
make the site read like the work of a professional robotics engineer: clear, confident,
typo-free writing; consistent page structure; and clean, reliable presentation.

This is a Jekyll site (academicpages / Minimal Mistakes theme). Content lives in
markdown files under `projects/`, `_pages/`, etc.; presentation is controlled by
`_layouts/`, `_sass/`, `_data/`, and `assets/css/`.

---

## 1. Guiding principles

These are the standards every page should meet after the revamp.

- **Professional, not casual.** Confident and concise. Cut self-deprecation
  ("I'm probably going to make mistakes", "mad man", "why go rogue"), filler, and
  hype ("smallest, cutest", "biggg fuzzy area").
- **Lead with outcome and contribution.** Every project should answer up front:
  what was the problem, what did *I* build, what was the result, what did I learn.
- **Zero typos / grammar errors.** The current pages have many; this alone is the
  biggest hit to perceived professionalism.
- **Consistent structure across projects** (see the template in §4).
- **Honest, internally consistent data.** Tables must not contain impossible values
  (e.g. F1-scores > 1). Captions must match the images they describe.
- **Consistent, theme-driven styling.** Move repeated inline styles into CSS classes;
  remove `!important` hacks; ensure mobile responsiveness.
- **No broken links or dead/placeholder pages** in the live navigation.

---

## 2. Site-wide issues

### 2.1 Navigation (`_data/navigation.yml`)  ✅ decided
- **Keep YouTube.** Fix the broken link: it currently points to `/youtube/` (no such
  page). Point it directly at the channel URL instead, and remove the stray leading
  space in the label (`" Youtube"` → `"YouTube"`).
- **Remove Podcast and Guide** from the nav (delete the commented-out entries so they
  don't get re-enabled by accident).

### 2.2 Config (`_config.yml`)
- `title: "Flavio Gheri / Flavio Gheri"` — duplicated name.
- `description: "personal description"` — placeholder; hurts SEO and social previews.
  Write a real one-line description.
- `bio: "Welcome to Flavio's Page"` — generic; replace with a real one-line bio.
- `repository: "academicpages/academicpages.github.io"` — still points at the template,
  not Flavio's repo.
- Review social links: confirm `bluesky`, `medium`, `youtube`, `linkedin` are correct
  and that we want all of them shown.

### 2.3 Home / About page (`_pages/about.md`)
- Typos: "explenations", "drawrings" (appears site-wide), missing article/grammar slips.
- Mentions content that **does not exist** on the site: "podcasting-interviews",
  "podcast appearances", "documentaries". Either remove these claims or scope them to
  what's real.
- Large block of leftover **Academic Pages template boilerplate** is commented out at
  the bottom (lines 19–59). Delete it.
- Tone is a bit generic/cringy ("Whether you are interested... or simply a tinkerer
  like me, you'll find all you are looking for"). Tighten to a confident intro.
- Title "Building Robots. Ideas and Stories" — confirm this is the desired tagline.

### 2.4 Repo hygiene (root-level clutter)  ✅ done in Phase 1
Removed the committed scratch files: `COMPLETION_REPORT.md`, `PROJECT_UPDATE_SUMMARY.md`,
`QUICK_START_IMAGES.md`, `IMAGE_RESOURCES.md`, `notes.md`. Kept `README.md`, `LICENSE`,
`CONTRIBUTING.md`. (`blob/` is git-ignored.)

### 2.5 Stub / dead project files
- ✅ **done in Phase 1:** removed `_projects/lunarzebro.html`, `_projects/poletilt.html`,
  `_projects/README.md` (all empty).
- `projects/MAChallenge.md` — empty body, `published: false`, **wrong title**
  ("Localization of SO100 Robot Hand"). Decide: finish it or delete it.
- `projects/localization_hand.md` — `published: false`, fine to leave hidden but the
  prose has typos ("redunant", "in due process").
- `projects/this_website.md` — front matter only, no content. Decide: write it or drop.
- `_portfolio/` (portfolio-1.md, portfolio-2.html) — leftover template samples, unused.
  Remove if the Projects page has fully replaced the portfolio.

---

## 3. Styling / UI issues

### 3.1 Project cards (`assets/css/styles.css` + `_pages/projects.md`)
- CSS relies on `!important` to fight the theme; `.project-text p` (1.2em) conflicts
  with `.project-desc` (1em). Clean up the cascade so overrides aren't needed.
- `.project-image { width: 15% }` is a fixed ratio with no mobile breakpoint — cards
  likely look cramped on small screens. Add responsive behaviour (stack on mobile).
- Card titles are written in literal ALL CAPS in the HTML
  ("IMITATION LEARNING"). Use normal casing in markup + `text-transform: uppercase`
  in CSS so content stays clean and editable.
- **Reading times are hard-coded and likely inaccurate** (e.g. lunar_zebro is a long
  read marked "7 min"). Either recompute them or drop the badges.
- Card descriptions repeat the typo/tone problems of the project pages — fix together.

### 3.2 In-page image / caption styling (all project pages)
- Captions and image wrappers are done with **repeated inline styles** on nearly every
  image (`style="text-align:center; margin:2rem 0"`, `<i>` captions, border hacks).
  Introduce reusable classes (e.g. `.figure`, `.figure-caption`) or use the theme's
  `<figure>` support consistently, and apply site-wide.
- `malware_detection.md` already uses semantic `<figure>/<figcaption>` — adopt that
  pattern everywhere for consistency.

### 3.3 General
- Confirm heading hierarchy is consistent (single `#`/H1 from title, then `##`, `###`).
  Several pages jump levels or start at `## 2.` (see lunar_zebro).

---

## 4. Standard project-page template

Adopt one structure for every project page so the site feels coherent:

1. **Title** (front matter) — descriptive, consistent capitalization.
2. **One-paragraph summary** — problem, my role, headline result.
3. **Context / Motivation** — why this mattered.
4. **Approach / What I built** — methods, with *my* contribution called out.
5. **Results** — figures and tables (verified, captioned).
6. **Discussion / What I learned.**
7. **Future work** (optional).
8. **References** (if academic).

Tag each project with consistent metadata (role, tools, date, links to code/paper)
— consider a small front-matter convention rendered as a header block.

---

## 5. Per-page content fixes

### 5.1 `projects/lunar_zebro.md` (highest priority — longest, most visible)
- **Broken structure:** body starts, then jumps to `## 2. Related Work` with **no
  section 1**, and numbering is inconsistent (later `## 3`, `## 4`, then `### 4.2`).
  Reorganize to the §4 template.
- **Reads like a group academic report, not a portfolio piece.** Reframe around
  Flavio's contribution and keep the research detail as supporting depth.
- **What's actually missing / wrong (you asked):** the tables *are* present and can
  stay — the problem is the **F1-score column is mathematically impossible**. F1 ∈ [0,1],
  but the table lists values like 0.84, 1.00, 1.28, 1.36, 1.74. F1 = 2·P·R/(P+R), so
  recomputing from the existing precision/recall gives:
  - **Table 1 (model comparison):** N → 0.016, S → 0.313, M → 0.478, B → 0.249,
    L → 0.028, X → 0.405, SSD → 0.488 (already correct).
  - **Table 2 (augmentation):** no-aug → 0.478, warping → 0.174, histogram → 0.023,
    pooling → 0.423.
  - Table 3 (real data) F1 = 0.2725 is already correct.

  These are the "reasonable numbers" — they're just the correctly computed F1s, so no
  data is invented. The narrative conclusions (M is best, augmentation hurt, real-world
  performance dropped) still hold. **Also fix the prose** that quotes the old impossible
  F1s (e.g. "an F1-score of 1.28").
- **Duplicate / wrong images:** ✅ done in Phase 1 — `yolov10_warping.png` was reused as
  the confusion matrix for both warping and histogram preprocessing. Per Flavio's call,
  the duplicates were **dropped** (kept the unique pooling-trick figure). If correct
  warping/histogram confusion matrices surface later, they can be added back.
- Many typos: "oppertunity", "eneergy", "summerized", "disadventageous", "balacing",
  "rquire", "percieve", "compairison", "launches" (→ "launched"), "it's" vs "its".
- Caption "Original Image (Right), In-house Equalization (left)" contradicts the next
  caption ("Left: Dataset image. Right: ..."). Reconcile left/right labels with images.

### 5.2 `projects/MagIA.md`
- ✅ **Phase 1 done:** wrote a clean, professional **short description** as the new intro;
  linked the live startup site **[magiaworld.com](https://magiaworld.com/)**; embedded the
  **animation pipeline** video and removed the placeholder "*this website*" reference and
  the cringy intro ("mad man", "biggg fuzzy area").
- **Assets extracted** from `blob/Magia_pitch_desk 1.pptx` (confirmed accessible):
  - `images/magia/animation_pipeline.mp4` — the "nice gif" (a 14 s MP4: drawing →
    figure detection → segmentation → pose/joint placement → final animation). Now the
    page header visual.
  - `images/magia/magia_logo.png` — MagIA logo + wizard mascot (available for hero/branding).
  - The pptx also has a tiger character mascot (`image7.png`) and many product mockups if
    we want more visuals later.
- **Still TODO (later phase):** the lower "Chapter 1/2" tech-stack and scaling sections are
  still rough notes (typos: "Unfotunately", "committments", "bearocratic", "vunerabilities",
  "Liectenstein"; "twofold" then lists 4; "Main Plan: Frontend ->"). Rewrite these into a
  clean product/tech-stack/AI-pipeline overview following §4, or trim them.

### 5.3 `projects/malware_detection.md`
- **Duplicate front matter:** a second YAML block is embedded inside the body
  (lines 8–12) with a different title and permalink. This is a bug — remove it.
- Title inconsistency: front matter "CNN for Malware Detection" vs embedded
  "Malware Classification with Convolutional Neural Networks".
- **Page is cut off:** ends mid-section at "Example: Turning a File into an Image"
  with a dangling code block and no conclusion. Finish or trim.
- Otherwise the writing here is the strongest on the site — use it as the quality bar.

### 5.4 `projects/path_planning.md`  — full redesign (you provided the target)
Rebuild this page to the exact case-study layout Flavio specified. Structure:

- **"← Back to Projects"** link at the top.
- **Hero / header block:** eyebrow label **"Unknown Environment"**, large title
  **"Drone Path Planning"**, and a one-line summary:
  *"Global planner implementation using Dijkstra algorithm for a quadrotor in PyBullet
  simulation, ensuring safe maneuverability and collision avoidance."*
- **Tag chips:** `Python`, `Dijkstra`, `PyBullet`.
- A **"Drone Flight Simulation"** visual (image/gif/video placeholder).
- **Section `01. The Concept`:** built for the "Planning and Decision Making" course
  in the Robotics MSc at TU Delft (course code RO47005); objective was a robust global
  planner guiding a quadrotor safely through obstacle-ridden environments in a
  physics-based sim. Core challenge: implement **Dijkstra from scratch** and integrate
  it into PyBullet for autonomous 3D navigation.
- **Section `02. Technical Deep Dive` → "Smart Grid Generation":** voxel-based grid;
  space discretized into nodes; each node validated against bounds + obstacle positions
  to build a navigable graph. Include the `grid_filter.py` code block (the
  `filter_grid(XYZ)` snippet provided).
- **Fine vs. Coarse grid comparison:** two captioned visuals — "High Resolution Grid
  (0.1 spacing)" and "Low Resolution Grid (0.2 spacing)".

> **⚠️ Content discrepancy to confirm:** the *current* page describes a **Velocity
> Obstacles local planner** (and global planners RRT/RRT*/IB-RRT*/A*) done with 3
> teammates. The new design reframes the project around a **Dijkstra global planner**.
> Confirm whether this is a re-scope (replace old content) or whether Dijkstra should be
> presented *alongside* the existing planners. I'll treat it as a replacement unless told
> otherwise. The old "go rogue" aside is dropped regardless.

> **Note:** this richer, sectioned, chip-and-hero layout is a strong candidate to become
> the **template for all project pages** (see §6 Interactivity). That would resolve the
> "site feels static/boring" feedback and the §4 consistency goal at the same time.

### 5.5 `projects/6dpose.md`  — flesh out from the MSc thesis
This is Flavio's **TU Delft MSc thesis, done in collaboration with Hilti** (the source
is `blob/Thesis_FINAL_Draft(1).zip`, now git-ignored). It's a flagship project and
should be the most polished page on the site. Key content (from the thesis abstract):

- **Problem:** construction *stakeout* transfers design points from a digital model to
  the physical site using a robotic total station (RTS) tracking a prism on a handheld
  pole. Accuracy is limited by the operator keeping the pole perfectly vertical — any
  tilt becomes a lateral error at the tip that scales with pole length. The manual
  levelling cycle is slow (~2–3 min/point) and is ~25% of a surveyor's working time.
- **Idea:** estimate pole orientation in real time by **fusing the RTS with an IMU** so
  tilt is corrected automatically — operator just brings the tip to the target.
- **My three contributions:** (1) a **tilt-aware RTS measurement model** that corrects
  the PLT400's built-in vertical-pole assumption; (2) an **in-field calibration** of the
  IMU-to-pole-tip lever arm via sphere fitting (rotating the pole about a fixed tip
  traces a sphere); (3) a **delay-aware extension** that treats the unknown RTS↔IMU clock
  offset as an optimization variable via piecewise-linear pose interpolation.
- **Method:** the whole thing is a **factor graph** (each measurement/constraint = a cost
  term) solved with a **moving-horizon estimator (MHE)** for real-time operation. Built
  on **GTSAM** (matches the current poletilt blurb).
- **Result:** **~5.8 mm 2D RMSE** in the fine-navigation regime — meeting the
  sub-centimetre target *without* hardware sync and with a less accurate RTS than prior
  work. Levelling cycle eliminated; **<30 s per point** (vs 2–3 min); a full day's
  fine-navigation drops from ~2 h to <30 min. Dominant remaining error = calibration
  drift as the pole tip's contact point shifts (the main future-work direction).
- **Assets available** in the thesis zip: figures for the factor-graph/MHE structure,
  code structure, bias/Allan-deviation plots, error distributions, pole-tip lag
  behaviour, ball-socket pole design, robot (Jaibot) PLT example. Pull a few clean ones
  into the page (export from the zip into `images/` — don't commit the zip).
- **Cleanup:** align slug/title/card — permalink is `/projects/poletilt/` but the title
  says "6D Pose"; pick one consistent name and update the card link in `projects.md`.
- **Decided:** ❌ **Do not name Hilti** on the public page. Describe it generically (e.g.
  "an industry MSc thesis project" / "a commercial robotic total station") and avoid the
  PLT400 model name / Hilti branding in copy and image captions.

### 5.6 `projects/swarm_planning.md`  — flesh out from the reference paper
Base this on **Barnes, Fields & Valavanis, "Unmanned Ground Vehicle Swarm Formation
Control Using Potential Fields"** (15th Mediterranean Conf. on Control & Automation, 2007)
— the paper Flavio provided. Goal: a clearer, correct write-up of the method **and an
honest account that the reproduction didn't fully work.**

- **Concept:** organize a robot swarm into formations using **artificial potential
  fields** built from **normal (Gaussian) and sigmoid functions**. A bivariate normal
  "hill" defines an elliptical surface the swarm travels on; its gradient gives each
  member's velocity/heading. Members are attracted to a target ellipse band (the *R\**
  neighbourhood); sigmoid **limiting functions** confine the fields so vectors "die out"
  at the band edges; an extra perpendicular field moves members *along* the band, and an
  avoidance field controls inter-member spacing.
- **Equations to explain properly** (the current page has none): the bivariate normal
  `f(x,y)=e^{-((x-x_c)² + γ(y-y_c)²)}`; its gradient → velocity vectors; the target
  ellipse `R*² = (x-x_c)² + γ(y-y_c)²` with axis-ratio γ; and the sigmoid limiting
  functions `S_in`, `S_out`, `N⊥` that trap members in `R* − ΔR_in < r < R* + ΔR_out`.
  Walk through what each parameter (γ, ΔR_in, ΔR_out, ΔR_avoid, ε) controls — the paper's
  Tables I–III give concrete values for arc/circle/ellipse formations.
- **Honesty / my experience:** Flavio reproduced this but **could not get the exact swarm
  effect** — the sigmoid limiting functions didn't shape the field as intended. Frame
  this as a candid "what I tried, what broke, what I'd debug next" section (likely
  suspects: limiting-function tuning/α derivation, the perpendicular-field direction
  multiplier `SGN`, or gradient normalization). This kind of honest post-mortem reads as
  *more* professional, not less.
- **Tone:** drop the bare "military applications" line, or contextualize it as one
  application area alongside planetary exploration / search-and-rescue (as the paper's
  convoy-protection framing does).
- Decide whether to publish it on the Projects index (currently not linked).

### 5.7 `projects/Imitation_learning.md`
- Strongest-structured page already. Minor polish only:
  - LaTeX bug at line 88: `\text{Success Rate}` is written as `	ext{...}`
    (a literal tab + "ext") — will not render. Fix.
  - Otherwise keep as a model for the others.

### 5.8 `projects/this_website.md`, `projects/localization_hand.md`,
`projects/MAChallenge.md`
- See §2.5 — finish or remove; fix the duplicated/incorrect titles.

---

## 6. Interactivity — make the site feel less static

Flavio's feedback: *"the website needs to feel more interactive… it feels very static
and boring,"* and especially *"the main page… I would like the website to pop a little
more and feel more professional."* This is now a first-class goal, not a nice-to-have.
The path-planning case-study design (§5.4) is the visual direction; extend that feel
across the site.

**The home page (`_pages/about.md`) is the top priority here** — it's currently a plain
wall of text. Make it the showcase:
- A proper **hero**: name + one-line "Robotics engineer — perception, SLAM, computer
  vision," a portrait, and clear calls-to-action (Projects, CV, YouTube).
- **Featured-projects strip** right on the landing page (e.g. 6D Pose, Lunar Zebro,
  Imitation Learning) as interactive cards, instead of making visitors hunt via the nav.
- Subtle entrance animation / motion in the hero so the first screen feels alive.
- Tighten the copy (it still mentions podcasts/documentaries that don't exist).

**Principle:** add motion and interaction that *reveals the engineering* — it should make
the work easier to understand, not just decorate. Keep it lightweight (this is a static
Jekyll/GitHub Pages site: prefer CSS + vanilla JS, lazy-load heavy assets, respect
`prefers-reduced-motion`, and keep it fast on mobile).

Concrete ideas, cheap → richer:

- **Project-card hover polish:** the cards already scale on hover — add subtle image
  zoom, an accent underline/arrow, and smooth easing so the index feels alive.
- **Scroll-reveal:** fade/slide sections in as they enter the viewport (IntersectionObserver),
  used on the new sectioned project layout (`01. The Concept`, `02. …`).
- **Sticky section nav / progress bar** on long pages (lunar_zebro, 6dpose) so readers can
  jump between sections and see reading progress.
- **Hero motion:** looping muted video / GIF / subtle canvas animation in project headers
  (e.g. the drone sim, the MagIA animated drawings, the rover render).
- **Interactive figures where they teach something:**
  - Path planning: animate Dijkstra exploring the grid, or a fine-vs-coarse grid toggle.
  - Lunar zebro: a before/after image slider for histogram equalization / warping; tabbed
    confusion matrices instead of stacked images.
  - 6dpose: an animated factor-graph / pole-tilt diagram, or an interactive error plot.
  - Malware: there's already a `malware_scanner_interactive.html` "binary visualizer" —
    make it a model for this kind of embedded interactive widget.
- **Code blocks:** syntax highlighting + copy-to-clipboard buttons (e.g. the
  `grid_filter.py` snippet, the LeRobot CLI commands).
- **Micro-interactions:** animated tag chips, smooth anchor scrolling, a light/dark toggle
  if it fits the theme.

**Recommendation:** turn the §5.4 layout into a reusable project layout/include so every
project gets the hero + chips + numbered sections + scroll-reveal "for free," giving the
whole site a consistent, modern, interactive feel in one move.

---

## 7. Open questions for Flavio

Most earlier questions are now answered (YouTube kept, podcast/guide removed; thin
projects to be fleshed out; lunar_zebro F1s recomputed in §5.1; lunar duplicate figures
dropped; Hilti **not** named on the 6dpose page; MagIA short description written).
Remaining:

1. **Path planning re-scope:** is the project now *Dijkstra global planner* (replacing the
   old Velocity Obstacles / RRT* content), or should both be shown? (See §5.4.) I'll
   assume replacement unless told otherwise.
2. **Path-planning assets:** can you provide the fine/coarse grid images and the drone-sim
   visual referenced in the target design?
3. **6dpose display name:** 6D Pose vs Pole-Tilt Estimation vs the thesis title — which
   should the public page use?
4. **Tagline:** keep "Building Robots. Ideas and Stories" as the homepage title?
5. **Tone/voice:** first person ("I built…") throughout — confirm preferred.

---

## 8. Suggested execution order

1. ✅ **Quick wins / hygiene (DONE):** fixed `_config.yml` placeholders (title, description,
   bio, repository); fixed the YouTube nav link + removed podcast/guide; fixed the LaTeX
   tab bug in imitation_learning; removed the duplicate front matter in malware_detection;
   dropped the duplicate lunar figures; removed root clutter + empty stub files; wrote the
   MagIA short description + embedded the extracted animation pipeline. (`blob/` git-ignored.)
2. **Copy editing pass:** typos and tone across about.md, projects.md cards, and all
   published project pages.
3. **Build the reusable interactive project layout** (hero + chips + numbered sections +
   scroll-reveal), starting with **path_planning** as the reference implementation (§5.4).
4. **lunar_zebro restructure** + F1 recomputation (§5.1) + figure fixes.
5. **Flesh out 6dpose (thesis)** and **swarm_planning (paper)**; rewrite **MagIA**;
   finish/trim **malware_detection**.
6. **Roll the interactive layout out to all projects** + styling pass (card CSS cleanup +
   responsiveness, shared figure/caption classes, ALL-CAPS via CSS).
7. **Final review:** build locally, click every nav item and project link, check mobile +
   `prefers-reduced-motion`.
