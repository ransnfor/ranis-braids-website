# Rani's Braids — Website (v2, built to improve on ranisbraids.com)

An 8-page static website (no backend, no database, no build step) for
Rani's Braids: Home, Services & Pricing, Gallery, About, Reviews, FAQ,
Booking, and Contact. Every page is a plain `.html` file sharing one
`css/style.css` and one `js/script.js`.

This version was built by looking at your current live site
(ranisbraids.com) and fixing the gaps it had: no visible pricing, no
clear booking flow, and no light/dark toggle. It keeps your real name,
tagline, contact info, hours, and Square booking link — see below for
exactly what's still a placeholder.

---

## What changed vs. your current site

- **Pricing is now visible** on a dedicated Services & Pricing page
  (your current site's services page didn't show prices).
- **A real, working "Book Now" flow** — the Booking page leads with a
  button straight to your actual Square scheduler
  (`square.site/book/LPF2VRFQNETAF/ranisbraids`), plus a request form
  as a fallback for consultations/custom asks.
- **Light/dark theme toggle** (the sun/moon icon in the header) — the
  site defaults to your current dark look, but visitors (and you) can
  switch to a light theme. Try it live once you open the site.
- **A working mobile menu**, fast-loading pages (no heavy video hero,
  just lightweight placeholder art you'll swap for photos), and the
  same page structure as your nav (Home, Gallery, Services, About,
  Reviews, FAQ) plus a dedicated Contact and Booking page.

---

## 1. What's still placeholder and needs your input

| Placeholder | Where | What to do |
|---|---|---|
| Social handles (`instagram.com/ranisbraids`, `facebook.com/ranisbraids`, `tiktok.com/@ranisbraids`, `youtube.com/@ranisbraids`) | Every page footer, contact.html | I guessed these from your business name — confirm they're your real handles or fix them (find & replace across all files). |
| Service names & prices | `services.html`, and the dropdown in `booking.html` | I couldn't pull your real menu (your live site loads it with JavaScript my tool can't read). Replace the placeholder styles/prices with your actual Square service list. |
| Stylist bio & name | `about.html` (`[Stylist Name]`) | Replace with the real name and story. |
| Photos | Every `.photo-placeholder` block | See section 2. |
| FAQ answers | `faq.html` | The questions are realistic for a braiding studio, but the answers are placeholders — confirm or rewrite each one to match your actual policies. |
| Reviews | `reviews.html`, and the 3 on the homepage | Replace the 6 sample reviews with real ones copied from Google/Facebook/Instagram (exact wording, first name + last initial, rating). |
| Contact form endpoint (`YOUR_FORM_ID`) | `booking.html`, `contact.html` | See section 3. |
| "Leave a Google Review" link | `reviews.html` | Currently a placeholder `https://g.page/r/` — replace with your actual Google Business review link. |

Everything else (business name, tagline, phone, email, address, hours)
is already filled in with your real information from ranisbraids.com.

---

## 2. Adding your own photos

Every image right now is a dashed placeholder box
(`<div class="photo-placeholder">`) so pages work before photos are
ready.

1. Create an `images/` folder next to `index.html`, add your photos
   (export around 1600px wide, under ~500KB each, so pages stay fast).
2. Find the placeholder, e.g.:
   ```html
   <div class="hero-visual">
     <div class="photo-placeholder">...</div>
   </div>
   ```
3. Replace the inner `<div class="photo-placeholder">...</div>` with:
   ```html
   <img src="images/hero.jpg" alt="Describe the photo" style="width:100%;height:100%;object-fit:cover;border-radius:inherit;">
   ```
4. In `gallery.html`, do the same for each `.gallery-item` tile, and
   keep its `data-category` attribute (`braids`, `cornrows`, `twists`,
   `locs`) so the filter buttons keep working.

---

## 3. Connecting the request form (contact + custom booking requests)

The request form on `booking.html` and the message form on
`contact.html` currently point at a placeholder Formspree ID, so
submitting either one shows "form is not connected yet" instead of
actually sending.

1. Create a free account at formspree.io with the salon's email.
2. Create a form — you'll get a URL like `https://formspree.io/f/abcd1234`.
3. In both `booking.html` and `contact.html`, replace
   `action="https://formspree.io/f/YOUR_FORM_ID"` with your real URL.
4. Submit a test — you should get an email within a minute. Free tier
   covers 50 submissions/month.

Your main "Book Now" button already goes straight to your real Square
scheduler — you don't need to set anything up for that, it's live.
If you ever get a new Square booking link, update it in `booking.html`
(search for `square.site/book`) — that's the only place it appears.

---

## 4. Rewriting the FAQ

Open `faq.html` and find each `<details class="faq-item">` block. Each
one looks like:

```html
<details class="faq-item">
  <summary>Question here <span class="faq-icon">+</span></summary>
  <p class="faq-answer">Answer here.</p>
</details>
```

Edit the question and answer text directly — no other markup needs to
change. Add a new FAQ by copy-pasting one whole `<details>...</details>`
block and editing the text; delete one the same way.

---

## 5. Adding real reviews

In `reviews.html`, each review is a `.review-card` block:

```html
<div class="card review-card">
  <div class="stars">★★★★★</div>
  <div class="review-head"><span class="who">Name</span><span class="date">When</span></div>
  <p class="quote">"Review text."</p>
  <div class="review-source">via Google</div>
</div>
```

Replace the name, date, quote and source with real reviews (copy them
exactly — don't paraphrase). The homepage also has 3 sample
testimonials in the same format worth updating to match.

---

## 6. Adding a real map (Contact page)

In `contact.html`, find the `.map-placeholder` block and replace its
inner `<div class="photo-placeholder">` with a Google Maps embed:
search your address on Google Maps → **Share → Embed a map** → copy
the `<iframe>` code in, adding `style="width:100%;height:100%;border:0;"`.

---

## 7. Publishing to Namecheap

### Option A — cPanel File Manager (easiest)

1. Namecheap → **Hosting List** → **Go to cPanel**.
2. Open **File Manager**, navigate into `public_html` (delete any
   placeholder `index.html` Namecheap put there).
3. Upload every file and folder from this project (`index.html`
   through `reviews.html`, plus `css/`, `js/`, and your `images/`
   folder) directly into `public_html`. If the uploader only takes
   single files, zip the folder, upload the `.zip`, then right-click
   it in File Manager and choose **Extract**.
4. Visit your domain — live within a few minutes.

### Option B — FTP

Get your FTP host/username/password from cPanel → **FTP Accounts**,
connect with a client like FileZilla, and upload the same files into
`public_html`.

### After it's live

- Test the mobile menu (shrink your browser, or check on your phone)
  and the light/dark toggle.
- Click "Book Now on Square" and confirm it opens your real scheduler.
- Submit a test request form once Formspree is connected (section 3).
- In cPanel → **SSL/TLS Status** → **Run AutoSSL** if the site isn't
  already loading as `https://`.

---

## 8. How the site is built (for your coursework)

- **No framework, no build step** — 8 standalone HTML files sharing
  one stylesheet and one script via `<link>`/`<script>` tags. This is
  the simplest deployable unit, which is why it drops straight into
  shared hosting.
- **`css/style.css`** is CSS custom properties (`:root { --color-... }`)
  driving every component — buttons, cards, forms. The light/dark
  toggle works by swapping one block of variable values
  (`:root[data-theme="dark"] { ... }`) rather than duplicating any CSS;
  every component below it already reads those variables.
- **Theme persistence**: a tiny inline `<script>` in each page's
  `<head>` reads `localStorage` and applies the saved theme *before*
  the page paints, avoiding a flash of the wrong theme. The actual
  toggle logic lives in `js/script.js`.
- **`js/script.js`** is vanilla JavaScript (no dependencies): mobile
  nav, theme toggle, active-nav-link highlighting, the gallery filter/
  lightbox, and intercepting form submissions to show an inline
  success/error message. Every form still works via native HTML
  `action`/`method` even if JavaScript fails — it's progressive
  enhancement, not a requirement.
- **The FAQ accordion** uses native `<details>/<summary>` — zero
  JavaScript, works even with scripts disabled, and is accessible by
  default (keyboard + screen reader).

A natural next step for a DevOps-flavored exercise: a small CI
pipeline that lints the HTML/CSS and auto-deploys on push (e.g. an
FTP-deploy GitHub Action) — happy to help set that up once this
version is live and the content is finalized.
