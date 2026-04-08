# Rocco's Rides Again — Website Redesign

**Date:** 2026-04-07  
**Status:** Approved

---

## Overview

Rebuild the existing WordPress site for Rocco's Rides Again (formerly Rocco's Cucina) as a modern static site. The business is a Bronx-style pizza catering/food truck operation based in Los Angeles. The site is a pure brochure — no ordering, no CMS, no contact form. The owner (Loren) handles all content updates.

---

## Tech Stack

| Concern | Choice | Reason |
|---|---|---|
| Framework | Astro (static export) | Purpose-built for content/brochure sites, zero JS output by default |
| Styling | Tailwind CSS | Utility-first, no runtime overhead |
| Hosting | Vercel | GitHub push → auto deploy, free tier, no more FTP |
| Source control | GitHub | Triggers Vercel deploys |

---

## Design Language

**Aesthetic:** Rock poster / tattoo art / grungy. Inspired directly by the phoenix wings logo.

**Colors:**
- Background: `#000000` (pure black)
- Primary accent: `#e8890a` (fire orange — from logo wings)
- Secondary accent: `#2ec4b6` (iridescent teal — from logo wing tips)
- Body text: `#ffffff`
- Muted text / labels: `#555555`
- Subtle borders: `#1a1a1a`

**Typography:**
- Headlines: Georgia serif, heavy weight (`font-weight: 900`)
- Accent/italic: Georgia italic for the "BRONX STYLE" treatment — white, no color, pure attitude
- Labels/nav: sans-serif, small caps, wide letter-spacing (`letter-spacing: 3-4px`)

**Motifs:**
- Diamond bullet dividers (`◆` rotated 45°)
- Gradient bleeds (orange → teal) at section transitions
- Radial dark glow (`#1a0d00`) behind hero section
- `///` separators in metadata strips
- Glowing text-shadow on orange accent elements

**Logo:** `TruckPhoenixLogoDraft3JPEGCrownColoredLargerLOGO.jpg` — centered in hero, lazy loaded.

---

## Page Structure

Single-page application. One `index.astro` file. Sticky nav with smooth-scroll anchor links. No routing.

### Sections (top to bottom)

#### 1. Sticky Nav
- Left: `ROCCO'S` in fire orange + `RIDES AGAIN` in small muted caps below
- Right: anchor links → `About`, `Menu`, `Contact`
- Background: `#000`, bottom border `#1a1a1a`
- Always sticky: `position: sticky; top: 0`

#### 2. Hero (`#hero`)
- Full-width, radial dark glow background
- Logo image (lazy loaded, centered)
- Tagline: `From the Heart of the Bronx · Los Angeles` — muted, small caps
- Headline:
  ```
  FRESH
  BRONX STYLE   ← Georgia italic, white
  PIZZA
  ```
- Metadata strip: `Catering /// Events /// Food Truck`
- CTA button: `Book Your Event` → smooth scrolls to `#contact`
- Subtle `↓ scroll` hint at bottom

#### 3. About (`#about`)
- Section label: `— About` in fire orange small caps
- Heading: `From the Heart of the Bronx`
- Body: Frankie Rocco's story — worked in his mother's Bronx pizzeria, relocated to LA, three-generation recipe, Polly-O mozzarella, Perfect Diamond flour, 40+ years of craft
- Optional: one photo (lazy loaded)

#### 4. Menu (`#menu`)
- Section label: `— Menu` in fire orange small caps
- Heading: `What We Bring`
- 3-column grid of category cards, each with name + items listed
- Categories: Pizza, Entrees, Salads, Sandwiches, Catering, Add-Ons
- Cards: dark border `#1a1a1a`, no fill, minimal

#### 5. Contact (`#contact`)
- Section label: `— Contact` in fire orange small caps
- Heading: `Book an Event`
- Display-only (no form): two phone numbers, email, hours of operation
- Restaurant: (310) 573-3727
- Catering: (310) 995-1895
- Email: kroccolevy@roccospalisades.com
- Hours: Mon–Fri 10AM–8PM · Sat 11AM–8PM · Sun Closed

#### 6. Footer
- `© ROCCO'S RIDES AGAIN` left, `LOS ANGELES` right
- Gradient line divider between them
- Color: `#2a2a2a` (very dark, barely visible)

---

## Implementation Notes

- **Lazy loading:** All images use `loading="lazy"` attribute
- **Smooth scroll:** CSS `scroll-behavior: smooth` on `html`, anchor `href="#section-id"` on nav links
- **No JavaScript framework:** Astro ships zero JS for this use case. Smooth scroll handled entirely in CSS.
- **No contact form:** Spam risk, maintenance burden. Phone/email displayed directly.
- **No CMS:** Content lives in the `.astro` file. Owner updates via git.
- **No online ordering:** Slice integration removed entirely.
- **Fonts:** System font stack for body. Georgia (web-safe serif) for headlines — no font loading overhead.
- **Responsive:** Mobile-first. Nav collapses to hamburger or stacked links on small screens. Menu grid: 3-col on desktop, 2-col on tablet, 1-col on mobile. Hero text scales down. All tap targets minimum 44px.

---

## Content to Migrate from Old Site

All content extracted from roccospalisades.com:

- Business name: Rocco's Rides Again
- Tagline: "From the Heart of the Bronx"
- About story: Frankie Rocco, mother's Bronx pizzeria, LA relocation, 3-generation recipe
- Ingredients callout: Polly-O Mozzarella, Perfect Diamond flour
- Phone (restaurant): (310) 573-3727
- Phone (catering): (310) 995-1895
- Email: kroccolevy@roccospalisades.com
- Hours: Mon–Fri 10AM–8PM, Sat 11AM–8PM, Sun Closed
- Menu categories: Pizza, Entrees, Salads, Sandwiches, Lunch Specials, Add-Ons, Catering

> **Note:** Full menu item details (names, descriptions, prices) are not on the current site — will need to be provided by the client before launch.

---

## Out of Scope

- Online ordering
- Contact form
- CMS / admin panel
- Blog
- Multiple pages / routing
- Analytics (can be added later via Vercel)
