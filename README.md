# azharpm.com — Portfolio Website

Premium dark-theme portfolio for **Azharuddin Mohammed**, Fit-Out Project Manager.
Built as a static site — no build step, no Node.js, no React. Edit one file → projects update.

---

## Quick reference

| Want to… | Edit this file |
|---|---|
| Change name, contact, hero text, stats | `js/site-data.js` |
| Add / edit / remove a project | `js/projects-data.js` |
| Replace your CV PDF | drop into `assets/cv/azhar-cv.pdf` (overwrite) |
| Add project photos | drop into `assets/images/projects/<project-id>/` |
| Add project videos | drop into `assets/videos/`, then list in `projects-data.js` |
| Change colours / fonts | `css/styles.css` (the `:root` block at the top) |

---

## 1. Run it locally (preview on your laptop)

You **don't need to install anything**. Two options:

### Option A — Just open the file (simplest)
Double-click `index.html`. It opens in your browser.
**Caveat:** ES modules need a server. If you see a blank page or console errors, use Option B.

### Option B — Recommended: a tiny local server
**On Windows (no install):**
1. Open a terminal in this folder (Shift + right-click → "Open PowerShell here").
2. Run:
   ```
   python -m http.server 8080
   ```
3. Open http://localhost:8080 in your browser.

**Or with Node.js installed:**
```
npx serve
```

That's it. Edit files, refresh the browser, see the changes.

---

## 2. Deploy to Vercel (free, takes 3 minutes)

### Easiest method — drag & drop
1. Go to **https://vercel.com/new** and sign in (Google or GitHub).
2. Click **"deploy a static site"** → drag the `azharpm-portfolio` folder into the upload area.
3. Wait ~30 seconds. Vercel gives you a `*.vercel.app` URL — your site is live.

### Better method — GitHub-connected (auto-redeploys on changes)
1. Create a new repo on **github.com**, e.g. `azharpm-portfolio`.
2. Upload the contents of this folder to that repo (drag & drop in GitHub's UI works).
3. On **vercel.com**, click "Add New → Project" → select the repo → click Deploy.
4. From now on: every time you push a change to GitHub, Vercel rebuilds the site automatically.

`vercel.json` is already configured for clean URLs and aggressive image caching.

---

## 3. Connect your domain `azharpm.com`

You said you own the domain. Here's exactly how to point it at Vercel:

1. In Vercel, open your project → **Settings → Domains**.
2. Add `azharpm.com` and `www.azharpm.com`.
3. Vercel shows you the DNS records to add. They look like this:
   ```
   Type: A      Name: @     Value: 76.76.21.21
   Type: CNAME  Name: www   Value: cname.vercel-dns.com
   ```
4. Log in to your **domain registrar** (where you bought azharpm.com — e.g. GoDaddy, Namecheap, Hostinger) and open the **DNS settings** for the domain.
5. Delete any existing A or CNAME records pointing to a parking page.
6. Add the two records Vercel gave you. Save.
7. Wait 5–60 minutes for DNS to propagate. Vercel will show a green "Valid Configuration" tick.
8. Done. https://www.azharpm.com loads your portfolio. Vercel also issues a free SSL certificate automatically.

> If Vercel shows different DNS values than the example above, **use Vercel's values, not these**. They're the source of truth.

---

## 4. Update content — the only files you'll touch

### A. Add a new project
Open `js/projects-data.js`. Copy the last project block (everything from `{` to `}`), paste it after the comma, then update the fields. Every field is documented in the file.

```js
{
  id: "my-new-project",            // unique, lowercase, no spaces — used in the URL
  name: "Project Name",
  location: "Dubai, UAE",
  year: "2024",
  category: "Retail",              // Retail | Salon | Commercial | Renovation | Hospitality | Residential
  country: "UAE",                  // UAE | KSA | Other GCC
  status: "Completed",             // Completed | Ongoing | On hold
  client: "Client Name",
  duration: "8 weeks",
  value: "AED [amount]",
  role: "Fit-Out Project Manager (Client-Side)",
  scope: "One-line scope summary.",
  summary: "Card subtitle, one short sentence.",
  responsibilities: [
    "First responsibility…",
    "Second responsibility…"
  ],
  challenges: "Plain-text paragraph.",
  actions: "Plain-text paragraph.",
  outcome: "Plain-text paragraph.",
  images: [
    "assets/images/projects/my-new-project/img-1.jpg",
    "assets/images/projects/my-new-project/img-2.jpg"
  ],
  before: ["assets/images/projects/my-new-project/before-1.jpg"],
  after:  ["assets/images/projects/my-new-project/after-1.jpg"],
  videos: [
    { src: "assets/videos/my-walkthrough.mp4", title: "Site walkthrough" }
  ],
  authorityNotes: "DM, DCD, Civil Defence, mall NOC.",
  handoverNotes:  "Snags closed, O&M packs delivered."
}
```

Save the file. Refresh the projects page. Your new project appears.

### B. Add photos to an existing project
1. Create a folder for the project under `assets/images/projects/` if it doesn't exist (e.g. `assets/images/projects/sapori/`).
2. Drop your `.jpg` or `.png` files there. Use lowercase filenames with no spaces.
3. In `js/projects-data.js`, add the new paths to that project's `images` array.

**Tip on image size:** the site looks best with photos around 1600–2000 px wide. Bigger = slower to load. Compress them at https://squoosh.app before uploading if any are over 1 MB.

### C. Add videos
1. Drop the video file into `assets/videos/` (use `.mp4`, ideally H.264 + AAC, under 30 MB).
2. In `projects-data.js`, add `{ src: "assets/videos/your-file.mp4", title: "Walkthrough" }` to that project's `videos` array.
3. The Videos page automatically aggregates all project videos.

### D. Update your CV
Replace the file at `assets/cv/azhar-cv.pdf` with your latest CV. Keep the filename the same and the download link continues to work. (If you change the filename, update `SITE.cvFile` in `js/site-data.js`.)

### E. Update your name / contact / stats / hero text
Open `js/site-data.js`. Every field is labelled. Save and refresh.

### F. Update work history (timeline)
In `js/site-data.js`, edit the `workHistory` array. Each entry has `date`, `title`, `company`, `location`, and a `points` array of bullet points.

---

## 5. Folder structure

```
azharpm-portfolio/
├── index.html              ← Home (3D hero, featured projects, stats, expertise)
├── about.html              ← About / approach
├── projects.html           ← Filterable project archive
├── project.html            ← Project detail (loads ?id=… from URL)
├── work-history.html       ← Career timeline
├── gallery.html            ← Aggregated photo gallery + lightbox + filters
├── videos.html             ← Aggregated video library
├── cv.html                 ← CV download + skills + summary timeline
├── services.html           ← Services & expertise + sectors + authorities
├── achievements.html       ← Editable achievement cards (placeholders by default)
├── contact.html            ← Contact form + info
├── 404.html                ← Not-found page
├── sitemap.xml  robots.txt ← SEO
├── vercel.json             ← Vercel config (cache headers, clean URLs)
├── css/
│   └── styles.css          ← Full design system (edit colours in :root)
├── js/
│   ├── site-data.js        ← ★ EDIT: name, contact, stats, work history, expertise
│   ├── projects-data.js    ← ★ EDIT: every project
│   ├── components.js       ← Shared header + footer (don't touch)
│   ├── three-bg.js         ← 3D hero scene
│   └── animations.js       ← Scroll reveal
├── assets/
│   ├── images/
│   │   ├── projects/
│   │   │   ├── sapori/     ← seeded with 5 photos from your folder
│   │   │   ├── nstyle/     ← seeded with 6 photos
│   │   │   ├── omorfia/    ← empty — add photos here
│   │   │   ├── uml/        ← seeded with 3 photos
│   │   │   └── dubai-hills/ ← empty — add photos here
│   ├── videos/             ← seeded with 2 videos (BBL Citywalk, BBL Shahama)
│   └── cv/azhar-cv.pdf     ← placeholder PDF — replace with your real CV
└── README.md               ← this file
```

---

## 6. What's already loaded vs what needs you

| Page | Status |
|---|---|
| Home | Live with real layout, 3D hero, your project cards |
| About | Live, profile written from your brief — review wording |
| Projects | Live, 6 project entries seeded (Sapori, Nstyle, Omorfia ×2, UML, Dubai Hills) |
| Project detail pages | Live for every project — but `[year]`, `[client]`, `[value]` are placeholders. Replace once confirmed. |
| Gallery | Live, aggregates from project images. Already showing Sapori, Nstyle, UML photos. |
| Videos | Live, BBL Citywalk and BBL Shahama walkthroughs already playing. |
| CV | Live with placeholder PDF — replace `assets/cv/azhar-cv.pdf` |
| Services | Live |
| Achievements | Live with placeholder metrics — replace numbers in `js/site-data.js` once verified |
| Contact | Live with mailto-based form (opens user's email app pre-filled) |

### To make the site fully production-ready, do these:
1. **Drop your real CV** into `assets/cv/azhar-cv.pdf` (overwrite the placeholder).
2. **Update placeholders** in `js/site-data.js`:
   - `phone`, `linkedin`, optional `portrait` photo path
   - `workHistory` — fill in real company names, dates, locations
   - `achievements` — replace `[#]` with verified figures or delete the entry
3. **Update placeholders** in `js/projects-data.js` for each project:
   - `[Year]`, `[Client]`, `[Project value]`, `[Duration]`, the `challenges` / `actions` / `outcome` paragraphs
   - Add more photos by dropping into the project's folder under `assets/images/projects/<id>/`
4. **Add a portrait** (optional): drop `your-photo.jpg` into `assets/images/`, then set `SITE.portrait = "assets/images/your-photo.jpg"` in `site-data.js`.

---

## 7. Optional: real backend for the contact form

The current contact form opens the user's email app. To receive emails directly:

**Easiest — Formspree (free tier):**
1. Sign up at https://formspree.io, create a new form.
2. Open `contact.html`, find the `<form id="contact-form" …>` line.
3. Replace it with:
   ```html
   <form id="contact-form" class="card" style="padding:32px;"
         action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
4. Remove the `addEventListener('submit', …)` block at the bottom of the script.

Formspree forwards every submission to your email.

---

## 8. SEO checklist (already done for you)

- Per-page `<title>` and meta description
- Open Graph tags on home page
- `robots.txt` and `sitemap.xml`
- Canonical URL on home
- Semantic HTML (h1, h2, structured headings)
- Mobile-responsive
- Fast (no build step, lazy-loaded images, cached assets via vercel.json)

After deploying to azharpm.com, submit the sitemap in **Google Search Console**: add the property `https://www.azharpm.com`, verify (Vercel offers a one-click DNS verification), then submit `sitemap.xml`.

---

## 9. Common questions

**Can I host this somewhere other than Vercel?**
Yes. It's plain HTML — drop the folder on **Netlify**, **Cloudflare Pages**, **GitHub Pages**, or any static host. No build step required.

**Why not React / Next.js?**
A build step adds friction every time you want to update content. You'd need Node.js installed, npm, a deploy pipeline. Static HTML is faster, more SEO-friendly, and editable in Notepad. The site already uses modern ES modules so the code stays clean and reusable.

**The 3D background looks heavy on my phone.**
It's already disabled for users who set "reduce motion" in their OS settings. To remove it entirely, delete the `<canvas id="hero-canvas">` line in `index.html` and the `initHero3D(...)` call.

**How do I change the gold accent colour?**
Open `css/styles.css`. The very top has a `:root { --accent: #c9a961; }` line. Change that hex code and every accent on the site updates.

---

Built for [azharpm.com](https://www.azharpm.com/) · Senior Fit-Out Project Manager · UAE / GCC
