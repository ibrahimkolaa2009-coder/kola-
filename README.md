# Team Apexion website

A single-page website for Team Apexion (NRL 2026, project Vortex Ion). It has a 3D intro, team pages and the Apexion Store with WhatsApp checkout.

## What's in the folder

```
apexion-website/
├── index.html        the whole website: layout, styles and code in one file
├── img/
│   ├── logo.png        full logo, dark text (used on light backgrounds and in link previews)
│   ├── logo_light.png  full logo, white text (used on the dark site)
│   ├── mark.png        mountain mark, dark
│   └── mark_light.png  mountain mark, light (also the browser tab icon)
└── README.md
```

Keep `index.html` and the `img` folder together. The page loads fonts from Google Fonts and the 3D library (three.js) from cdnjs, so it needs an internet connection to look exactly right.

## Put it online (free)

**Netlify Drop (easiest):** go to app.netlify.com/drop and drag the whole `apexion-website` folder onto the page. You get a live link in seconds. You can rename it in Site settings, for example `team-apexion.netlify.app`.

**GitHub Pages:** create a repository, upload `index.html` and the `img` folder, then turn on Settings → Pages → Deploy from branch (main, root).

**Your own domain:** both Netlify and GitHub Pages let you connect a domain like `teamapexion.in`.

To preview on your computer, double-click `index.html`. Everything works except the WhatsApp links need a phone or WhatsApp Desktop.

## Common edits (search for these in index.html)

| What to change | Search for |
|---|---|
| Number that receives store orders | `const WA_NUMBER = '918454945172';` (country code + number, no spaces or +) |
| Contact numbers on the page | `+91 97395 94993` and `+91 84549 45172` |
| Partner button WhatsApp number | `wa.me/919739594993?text=Hi%20Team%20Apexion` |
| Crew names, roles and descriptions | `const CREW = [` |
| Products, prices, colours and sizes | `const PRODUCTS = [` |
| Gallery photo slots | `const SLOTS = [` |
| Kit unboxing countdown date | `new Date('2026-10-10T00:00:00+05:30')` |
| Email (currently "Coming soon") | `Coming soon` |
| Colours | the `:root{` block at the top: `--sky` is the cyan, `--blue` is space blue, `--bg` is the black |

### Adding member photos
1. Put square photos in `img/`, named like `bassam.jpg`, `ibrahim.jpg` (the `id` of each person in `const CREW`).
2. In `index.html`, find `<div class="photo empty">` inside `renderCrew` and replace that block with:
   `<div class="photo"><span class="no">${String(n).padStart(2,'0')} / 09</span><img src="img/${m.id}.jpg" alt="${m.name}" loading="lazy"><span class="dept chip">${m.dept}</span></div>`

## How the store checkout works

1. Customer adds items, fills in name, phone, address and PIN.
2. They see a bill with a bill number (`APX-YYMMDD-XXXX`).
3. "Confirm & place order" opens WhatsApp to the order number with the full order and customer details. The customer presses Send.
4. The Order Confirmed screen appears, with buttons to send the bill to the customer's own WhatsApp, download it as an image, or email it.

A plain website can't send WhatsApp messages or emails by itself; the customer's tap on Send is what delivers them. Fully automatic bills need a paid service such as the WhatsApp Business API or an email service connected to a server.
