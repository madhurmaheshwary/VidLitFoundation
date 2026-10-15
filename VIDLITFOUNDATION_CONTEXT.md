# VidLitFoundation Website — Project Context

> Paste this at the start of any new Claude conversation about the Vidarbha Literary
> Foundation website (vidlitfoundation.org) to give full context without re-explaining.
> Update it as the site evolves. (This is the website context — separate from the
> MetroBookX app, which has its own context file.)

---

## What This Is

The public website for the **Vidarbha Literary Foundation (VLF)** — a registered
Section 8 (non-profit) company in Nagpur running reading-outreach programmes and a
free community book exchange across Nagpur and the Vidarbha region.

- **Live at vidlitfoundation.org.**
- It is a **marketing/landing site** — information about VLF, its programmes, and
  (new) event registration. It is NOT the book-exchange app (that's MetroBookX, a
  separate Next.js project at metrobookx.com).
- Programmes featured on the site: **MetroBookX** (book exchange), **Project LitSpark**
  (school outreach), **Project Rekindle** (college outreach), and the **Vidarbha
  Literature Festival** (vidlitfest.com).

---

## Tech Stack (simple on purpose — keep it that way)

- **Plain HTML, CSS, and a little vanilla JavaScript.** No framework, no build step,
  no dependencies. This is deliberate — it keeps the site trivial to host and edit.
- **Hosting:** Vercel. **Framework preset = "Other"** (no build command, no output
  directory — it's a static site).
- **Domain:** vidlitfoundation.org — purchased through **Hostinger**, site **hosted on
  Vercel**. (Email for the domain, info@vidlitfoundation.org, is also on Hostinger.)
- **Deploy:** git only — `git push` → Vercel auto-deploys in ~2 min. No npm / no local build.
- **GitHub repo:** _(TO CONFIRM — fill in the repo name; it's the VLF site repo that
  Vercel deploys from.)_

**Local project folder (Windows):**
`C:\Users\madhu\OneDrive\Balmitra Foundation\SCHOOL OUTREACH With VLF\VidLitFoundation`

**Deploy workflow (run from inside the folder above):**
```
cd "C:\Users\madhu\OneDrive\Balmitra Foundation\SCHOOL OUTREACH With VLF\VidLitFoundation"
git add .
git commit -m "..."
git push
```

---

## File Structure

```
index.html      -- home page (hero, mission, programmes, get-involved)
litspark.html   -- Project LitSpark school-programme page (links to the two book pages)
wonder.html     -- book page: Wonder (R.J. Palacio)
theboy.html     -- book page: The Boy Who Harnessed the Wind
events.html     -- NEW: event info + registration page (see Events System below)
styles.css      -- the ONE stylesheet for the whole site (tokens at top)
assets/         -- book covers (wonder.avif, the-boy.avif, litspark.avif) + posters
assets/events/  -- NEW: event posters, one per event (lowercase folder)
```

- All page copy lives directly in each `.html` file.
- **One stylesheet** (`styles.css`) powers every page. Its sections, top to bottom:
  (1) design tokens (`:root`), (2) base/home styles, (3) sub-page styles (LitSpark +
  book pages), (4) **Events page styles**, (5) **mobile menu (hamburger) styles**.
  Sections 4 and 5 were added in Oct 2026 — see History.

---

## Design System (in `styles.css` `:root`)

- **Colours:** `--paper #F6F1E7`, `--paper-warm #EFE6D3`, `--ink #232017`,
  `--ink-soft #514A3A`, `--marigold #C9742B`, `--marigold-deep #9B5420`,
  `--moss #46563E`, `--rule rgba(35,32,23,0.12)`. `--radius 4px`.
- **Fonts (Google Fonts):** `Fraunces` (display/headings), `Inter` (body),
  `Tiro Devanagari Marathi` (Marathi/Devanagari text).
- Change values in `:root` to re-theme the whole site.

---

## Navigation

- **Navbar items (every page):** Mission · Programs · **Events** · Get Involved.
  - On the **home page**, Mission/Programs/Get Involved are in-page anchors
    (`#mission`, `#programs`, `#involve`); Events → `events.html`.
  - On **other pages**, those three point to `index.html#...`; Events → `events.html`.
- **Mobile menu (added Oct 2026):** on screens ≤860px the horizontal menu is replaced
  by a **hamburger (☰) button** (`.nav-toggle`) that opens a dropdown. Implemented with
  a small vanilla-JS toggle in each page's `<script>` block (adds `.open` to `.nav`) +
  CSS in the mobile section of `styles.css`. Present on all 5 pages.

---

## Events / Registration System (built Oct 2026)

The site can advertise an event and collect RSVPs. Current model = **one reusable
`events.html`**, re-edited for each new event.

**How registration works (important):**
- A static site **cannot save form submissions itself** — it has nowhere to store data.
  So registrations are collected by a **Google Form**, which drops every response into a
  linked **Google Sheet** (download as Excel anytime: File → Download → Microsoft Excel).
- `events.html` shows the **poster** (left) + **event details** (right: Date/Time/Venue)
  and a **"Register to attend" button**. The button **opens the Google Form in a new tab**
  — it is deliberately NOT embedded. (An embedded form left a confusing white gap after
  submit because a page can't auto-scroll a cross-origin iframe to its confirmation; the
  new-tab approach gives Google's own clear "response recorded" screen.)

**The Google Form:**
- Lives in a **Google account on `info@vidlitfoundation.org`** (see Google Account below).
- Name: **"VLF Event Registration"**. Questions: **Your name** (short, required),
  **Mobile number** (short, required; response validation = regex `^[6-9]\d{9}$` for a
  10-digit Indian mobile), **Email (optional)** (short, not required). A form description
  shows the event Date/Time/Venue at the top.
- Settings: **Collect email addresses = Do not collect** and **Limit to 1 response = Off**
  — so NO Google sign-in is required; anyone with the link can submit.
- **Short link:** https://forms.gle/V7DaiuLiSs2oufFU7
- **Embed/long URL:** https://docs.google.com/forms/d/e/1FAIpQLSd7gTxNficNeRsNKLKUkjPs3oEwN9eR02-To2cbUEwvg_stHw/viewform

**QR code:**
- `vlf-events-qr.png` (900×900, dark ink on white) encodes **https://vidlitfoundation.org/events.html**.
- It is a **print asset** (posters/flyers), NOT a website file — keep it with print
  materials; it doesn't need to be in the repo. Regenerate if the events URL changes.

**Current live event (example):** "In conversation with author **Jerry Pinto** — *A Good
Life: The Power of Palliative Care*", Sat **17 October 2026, 5:00 pm**, Institution of
Engineers, North Ambazari Road, Nagpur. Poster: `assets/events/jerry-pinto-event.jpeg`.

---

## Google Account & Chrome Setup (for running VLF's Google Form/Sheet)

- **A Google account was created ON `info@vidlitfoundation.org`** (NOT a new @gmail).
  Done via accounts.google.com/signup → **"Use my current email address instead"** →
  verification code sent to the Hostinger inbox. This account **owns the Form and the
  responses Sheet**, so the data belongs to the Foundation. (The actual email still
  arrives in Hostinger as before — the Google account just rides on top of the address.)
  Note: the Google account's display name shows as "Vidarbha Literature Foundation".
- **A dedicated Chrome profile** ("Vidarbha Literature Foundation") was set up so VLF
  Google work doesn't clash with the personal Google account. **Always do VLF Google
  work in that Chrome profile** — then `forms.new`, Drive, Sheets etc. default to the VLF
  account (no `/u/1/` juggling). Confirm the "V" profile icon (top-right) before creating
  anything.

---

## Gotchas / Lessons Learned (read before editing — these all bit us once)

1. **Image file extension must match the HTML exactly.** `events.html` references
   `jerry-pinto-event.jpeg` — the file MUST be `.jpeg`, not `.jpg` (a browser treats them
   as different filenames → broken image). Windows **hides extensions by default**: turn
   on File Explorer → View → **File name extensions** to see the real ending before
   saving/renaming.
2. **Vercel is case-sensitive** for files and folders. Use **lowercase** (`assets/events/`,
   not `assets/Events/`), or the site 404s the file even though it works locally on Windows.
3. **`styles.css` is one shared file — always edit the LATEST copy.** It now holds the base
   site + sub-page + events + mobile-menu styles. Once (Oct 2026) an edit was built on a
   stale copy that lacked the event styles, and saving it wiped the events-page layout.
   **Before Claude edits `styles.css` (or any hand-edited file, including this context
   doc), upload the current version first** so Claude builds on what's actually live.
4. **A static web page can't write to a local Excel file.** Form data needs an online
   "collection box" (Google Form/Sheet). You then download the Sheet as Excel when needed.
5. **A Google account is not the same as an email address** — you can make a Google
   account that logs in with a non-Gmail address (that's what we did for info@).

---

## How to Add a NEW Event (future)

Current setup reuses the single `events.html`. To run the next event:

1. **Poster:** save it into `assets/events/` with a lowercase, no-spaces name
   (e.g. `author-name-event.jpeg`). Confirm the real extension and match it in the HTML.
2. **Form:** either reuse the existing "VLF Event Registration" form (clear old responses
   in the Sheet first if you want a clean list) OR make a new form in the VLF Google
   account. Note its short link.
3. **Edit `events.html`:** update the poster `<img src>` + `alt`; the Date/Time/Venue in
   the `.event-facts` list; the **Register button `href`** (if the form changed); and the
   `<title>`/`description` meta.
4. **QR:** if the events URL is unchanged, the existing QR still works. If you move to a
   per-event page, regenerate the QR for the new URL.
5. **Deploy:** `git add . && git commit -m "..." && git push`. Wait ~2 min, then test the
   live page + the Register button + a dummy submission landing in the Sheet.

**Possible future upgrade:** move from one overwritten `events.html` to **per-event pages**
(`event-<slug>.html`) plus an events-listing page, so past events stay live as an archive.

---

## How to Work With This Project (notes for Claude)

- **Static site, git deploy only** — give git commands (`add`/`commit`/`push`) at the end
  of any change, to run from the project folder. No npm/build steps.
- **Deliver all edited files together at the end**, with a save table: download name →
  save-as name → destination folder. Call out the exact path for anything in `assets/`.
- **Always build on the latest file.** Ask the user to upload the current version before
  editing (especially `styles.css` and this context doc) — don't assume an older copy is
  current. (This is how the Oct 2026 styles.css regression happened.)
- **Keep instructions simple and step-by-step.**
- Keep responses focused — this is a real public site for a community non-profit.
