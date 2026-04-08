# Rocco's Rides Again — Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-page Astro brochure site for Rocco's Rides Again with a rock poster aesthetic, deployed to Vercel via GitHub — no ordering, no CMS, no contact form.

**Architecture:** One `index.astro` page composed of five Astro components (Nav, Hero, About, Menu, Contact) plus Footer. Tailwind handles layout, spacing, and responsive grid. Scoped `<style>` blocks inside components handle design-specific CSS (radial gradients, glows, text-shadows). Zero JavaScript — smooth scroll via CSS `scroll-behavior: smooth`, mobile nav via flex-wrap.

**Tech Stack:** Astro 4.x, @astrojs/tailwind, Tailwind CSS 3.x, GitHub, Vercel

---

## File Map

```
/
├── src/
│   ├── pages/
│   │   └── index.astro              # Page shell — imports all components
│   ├── components/
│   │   ├── Nav.astro                # Sticky nav, anchor links
│   │   ├── Hero.astro               # Logo, headline, CTA
│   │   ├── About.astro              # Frankie's story
│   │   ├── Menu.astro               # 6-category grid
│   │   ├── Contact.astro            # Phone, email, hours
│   │   └── Footer.astro             # Copyright line
│   └── styles/
│       └── global.css               # scroll-behavior: smooth, Tailwind directives
├── public/
│   └── logo.jpg                     # Phoenix wings logo (copied from Downloads)
├── astro.config.mjs                 # Astro + Tailwind integration
├── tailwind.config.mjs              # Custom color tokens
└── .gitignore
```

---

## Task 1: Initialize Astro Project

**Files:**
- Create: `astro.config.mjs` (generated)
- Create: `package.json` (generated)
- Create: `.gitignore` (generated)

- [ ] **Step 1: Scaffold the project**

Run in `C:/Users/loren/projects/roccos`:
```bash
npm create astro@latest . -- --template minimal --yes
```
When prompted interactively (if `--yes` doesn't suppress):
- Template: **Minimal**
- TypeScript: **No** (not needed for a brochure site)
- Install dependencies: **Yes**
- Git: **No** (we'll init manually)

- [ ] **Step 2: Add Tailwind integration**

```bash
npx astro add tailwind --yes
```

This installs `@astrojs/tailwind` and creates `tailwind.config.mjs` and updates `astro.config.mjs`.

- [ ] **Step 3: Verify build works**

```bash
npm run build
```
Expected: `dist/` folder created, no errors. Output should say something like `✓ Completed in Xs`.

- [ ] **Step 4: Initialize git and commit**

```bash
git init
git add .
git commit -m "chore: scaffold Astro project with Tailwind"
```

---

## Task 2: Tailwind Config + Global Styles

**Files:**
- Modify: `tailwind.config.mjs`
- Create: `src/styles/global.css`

- [ ] **Step 1: Set custom color tokens in Tailwind config**

Replace the contents of `tailwind.config.mjs`:
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./src/**/*.{astro,html,js,jsx,md,mdx,ts,tsx}'],
  theme: {
    extend: {
      colors: {
        fire: '#e8890a',
        teal: '#2ec4b6',
        smoke: '#555555',
        ember: '#1a0d00',
      },
      fontFamily: {
        serif: ['Georgia', 'serif'],
      },
    },
  },
  plugins: [],
};
```

- [ ] **Step 2: Create global.css**

Create `src/styles/global.css`:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

html {
  scroll-behavior: smooth;
}

body {
  background-color: #000;
  color: #fff;
}

/* Prevent flash of unstyled content on anchor scroll */
:target {
  scroll-margin-top: 72px;
}
```

- [ ] **Step 3: Verify build**

```bash
npm run build
```
Expected: builds without errors.

- [ ] **Step 4: Commit**

```bash
git add tailwind.config.mjs src/styles/global.css
git commit -m "chore: add custom Tailwind tokens and global styles"
```

---

## Task 3: Page Shell (index.astro)

**Files:**
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Replace index.astro with the page shell**

Replace the entire contents of `src/pages/index.astro`:
```astro
---
import Nav from '../components/Nav.astro';
import Hero from '../components/Hero.astro';
import About from '../components/About.astro';
import Menu from '../components/Menu.astro';
import Contact from '../components/Contact.astro';
import Footer from '../components/Footer.astro';
import '../styles/global.css';
---
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Rocco's Rides Again — Fresh Bronx Style Pizza · Los Angeles</title>
    <meta name="description" content="Bronx-style pizza catering, events, and food truck in Los Angeles. Three generations of craft." />
  </head>
  <body class="bg-black text-white">
    <Nav />
    <main>
      <Hero />
      <About />
      <Menu />
      <Contact />
    </main>
    <Footer />
  </body>
</html>
```

- [ ] **Step 2: Create stub components so the build doesn't fail**

Create `src/components/Nav.astro`:
```astro
---
---
<nav>Nav</nav>
```

Create `src/components/Hero.astro`:
```astro
---
---
<section id="hero">Hero</section>
```

Create `src/components/About.astro`:
```astro
---
---
<section id="about">About</section>
```

Create `src/components/Menu.astro`:
```astro
---
---
<section id="menu">Menu</section>
```

Create `src/components/Contact.astro`:
```astro
---
---
<section id="contact">Contact</section>
```

Create `src/components/Footer.astro`:
```astro
---
---
<footer>Footer</footer>
```

- [ ] **Step 3: Verify build**

```bash
npm run build
```
Expected: builds without errors. All six component stubs resolve.

- [ ] **Step 4: Commit**

```bash
git add src/
git commit -m "chore: add page shell and component stubs"
```

---

## Task 4: Nav Component

**Files:**
- Modify: `src/components/Nav.astro`

- [ ] **Step 1: Replace Nav stub with full implementation**

Replace `src/components/Nav.astro`:
```astro
---
---
<nav class="sticky top-0 z-50 bg-black border-b border-[#1a1a1a] flex flex-wrap justify-between items-center px-8 md:px-10 py-4 gap-4">
  <div class="font-serif font-black text-fire text-[22px] leading-tight" style="text-shadow: 0 0 20px rgba(232,137,10,0.4)">
    ROCCO'S<br />
    <span class="text-[11px] tracking-[4px] text-smoke font-normal font-sans uppercase not-italic">RIDES AGAIN</span>
  </div>
  <div class="flex gap-6 md:gap-8 items-center">
    <a href="#about" class="text-smoke text-[10px] tracking-[3px] uppercase hover:text-white transition-colors duration-200">About</a>
    <a href="#menu" class="text-smoke text-[10px] tracking-[3px] uppercase hover:text-white transition-colors duration-200">Menu</a>
    <a href="#contact" class="text-smoke text-[10px] tracking-[3px] uppercase hover:text-white transition-colors duration-200">Contact</a>
  </div>
</nav>
```

- [ ] **Step 2: Verify build**

```bash
npm run build
```
Expected: builds without errors.

- [ ] **Step 3: Spot-check in browser**

```bash
npm run dev
```
Open `http://localhost:4321`. Nav should appear at top: fire-orange "ROCCO'S / RIDES AGAIN" on the left, three muted links on the right. Resize to mobile width — links should wrap below the logo gracefully.

- [ ] **Step 4: Commit**

```bash
git add src/components/Nav.astro
git commit -m "feat: add sticky nav with anchor links"
```

---

## Task 5: Hero Section

**Files:**
- Modify: `src/components/Hero.astro`
- Create: `public/logo.jpg`

- [ ] **Step 1: Copy logo to public/**

```bash
cp "/c/Users/loren/Downloads/TruckPhoenixLogoDraft3JPEGCrownColoredLargerLOGO.jpg" "/c/Users/loren/projects/roccos/public/logo.jpg"
```

- [ ] **Step 2: Replace Hero stub with full implementation**

Replace `src/components/Hero.astro`:
```astro
---
---
<section
  id="hero"
  class="text-center px-8 py-16 md:py-24 border-b border-[#111]"
  style="background: radial-gradient(ellipse at 50% 0%, #1a0d00 0%, #000 70%)"
>
  <img
    src="/logo.jpg"
    alt="Rocco's Rides Again — phoenix wings logo"
    loading="lazy"
    class="mx-auto mb-8 w-48 md:w-64"
  />

  <div class="inline-block border border-[#333] px-4 py-1 mb-5">
    <span class="text-smoke text-[9px] tracking-[4px] uppercase">
      From the Heart of the Bronx · Los Angeles
    </span>
  </div>

  <h1 class="font-serif font-black leading-[0.95] mb-4 text-5xl md:text-7xl">
    FRESH<br />
    <em class="italic text-white" style="letter-spacing: -1px">BRONX STYLE</em><br />
    PIZZA
  </h1>

  <div class="border-t border-b border-[#1f1f1f] py-3 my-6 max-w-xs mx-auto">
    <span class="text-smoke text-[10px] tracking-[3px] uppercase">
      Catering&nbsp;///&nbsp;Events&nbsp;///&nbsp;Food Truck
    </span>
  </div>

  <a
    href="#contact"
    class="inline-block border border-fire text-fire text-[10px] tracking-[4px] uppercase px-8 py-3 hover:bg-fire hover:text-black transition-colors duration-200"
    style="box-shadow: 0 0 20px rgba(232,137,10,0.1)"
  >
    Book Your Event
  </a>

  <div class="mt-8 text-[#333] text-[10px] tracking-[2px]">↓ scroll</div>
</section>

<!-- Section gradient bleed -->
<div style="height: 2px; background: linear-gradient(90deg, transparent, #e8890a, #2ec4b6, transparent)"></div>
```

- [ ] **Step 3: Verify build and check visually**

```bash
npm run build && npm run dev
```
Expected: builds clean. In browser at `http://localhost:4321`:
- Logo renders in hero
- "FRESH / *BRONX STYLE* / PIZZA" headline is white serif, italic on BRONX STYLE
- Fire-orange CTA button present
- Gradient bleed line visible below hero
- "Book Your Event" click scrolls to `#contact` (stub, but anchor should jump)

- [ ] **Step 4: Commit**

```bash
git add src/components/Hero.astro public/logo.jpg
git commit -m "feat: add hero section with logo and headline"
```

---

## Task 6: About Section

**Files:**
- Modify: `src/components/About.astro`

- [ ] **Step 1: Replace About stub**

Replace `src/components/About.astro`:
```astro
---
---
<section id="about" class="px-8 md:px-16 py-16 bg-[#050505] border-b border-[#111]">
  <div class="text-fire text-[9px] tracking-[4px] uppercase mb-4">— About</div>

  <div class="flex flex-col md:flex-row gap-8 items-start max-w-3xl">
    <div class="flex-1">
      <h2 class="font-serif font-black text-white text-2xl md:text-3xl leading-tight mb-5">
        From the Heart<br />of the Bronx
      </h2>
      <p class="text-[#999] text-sm leading-relaxed">
        Frankie Rocco grew up working in his mother's pizzeria in the Bronx — learning the craft
        from the ground up, tossing dough the old way, using the right ingredients and nothing else.
        When he relocated to Los Angeles, he brought the whole operation with him: the same family
        recipe passed down three generations, Polly-O mozzarella, Perfect Diamond flour — by family
        request, no substitutions.
      </p>
      <p class="text-[#999] text-sm leading-relaxed mt-4">
        Over 40 years of forming dough balls and building community. Now bringing that same energy
        to catering, events, and the food truck across Los Angeles.
      </p>
    </div>

    <!-- Uncomment when a photo is available:
    <img
      src="/frankie.jpg"
      alt="Frankie Rocco"
      loading="lazy"
      class="w-32 md:w-48 object-cover flex-shrink-0"
    />
    -->
  </div>

  <!-- Stats strip -->
  <div class="flex gap-12 mt-12 pt-8 border-t border-[#111]">
    <div>
      <div class="font-serif font-black text-fire text-2xl" style="text-shadow: 0 0 10px rgba(232,137,10,0.3)">40+</div>
      <div class="text-[#3a3a3a] text-[9px] tracking-[2px] uppercase mt-1">Years of Craft</div>
    </div>
    <div>
      <div class="font-serif font-black text-[#f5c842] text-2xl" style="text-shadow: 0 0 10px rgba(245,200,66,0.2)">3</div>
      <div class="text-[#3a3a3a] text-[9px] tracking-[2px] uppercase mt-1">Generations</div>
    </div>
    <div>
      <div class="font-serif font-black text-teal text-2xl" style="text-shadow: 0 0 10px rgba(46,196,182,0.2)">1</div>
      <div class="text-[#3a3a3a] text-[9px] tracking-[2px] uppercase mt-1">Secret Recipe</div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Verify build**

```bash
npm run build
```
Expected: builds without errors.

- [ ] **Step 3: Commit**

```bash
git add src/components/About.astro
git commit -m "feat: add about section with story and stats"
```

---

## Task 7: Menu Section

**Files:**
- Modify: `src/components/Menu.astro`

- [ ] **Step 1: Replace Menu stub**

Replace `src/components/Menu.astro`:
```astro
---
const categories = [
  {
    name: 'Pizza',
    items: [
      'Plain Pie',
      'Sicilian',
      '— update with full menu items —',
    ],
  },
  {
    name: 'Entrees',
    items: [
      '— update with full menu items —',
    ],
  },
  {
    name: 'Salads',
    items: [
      '— update with full menu items —',
    ],
  },
  {
    name: 'Sandwiches',
    items: [
      '— update with full menu items —',
    ],
  },
  {
    name: 'Catering',
    items: [
      '— update with full menu items —',
    ],
  },
  {
    name: 'Add-Ons',
    items: [
      '— update with full menu items —',
    ],
  },
];
---
<section id="menu" class="px-8 md:px-16 py-16 bg-black border-b border-[#111]">
  <div class="text-fire text-[9px] tracking-[4px] uppercase mb-4">— Menu</div>
  <h2 class="font-serif font-black text-white text-2xl md:text-3xl mb-8">What We Bring</h2>

  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3">
    {categories.map((cat) => (
      <div class="border border-[#1a1a1a] p-4 hover:border-[#2a2a2a] transition-colors duration-200">
        <h3 class="text-white text-sm font-bold tracking-wide mb-3">{cat.name}</h3>
        <ul class="space-y-1">
          {cat.items.map((item) => (
            <li class="text-[#555] text-xs leading-relaxed">{item}</li>
          ))}
        </ul>
      </div>
    ))}
  </div>
</section>

<!-- Diamond divider -->
<div class="flex items-center px-8 py-0">
  <div class="flex-1 h-px" style="background: linear-gradient(90deg, transparent, #222)"></div>
  <div class="w-2 h-2 bg-fire mx-2 rotate-45"></div>
  <div class="flex-1 h-px" style="background: linear-gradient(90deg, #222, transparent)"></div>
</div>
```

- [ ] **Step 2: Verify build**

```bash
npm run build
```
Expected: builds without errors.

- [ ] **Step 3: Commit**

```bash
git add src/components/Menu.astro
git commit -m "feat: add menu section with category grid"
```

---

## Task 8: Contact Section + Footer

**Files:**
- Modify: `src/components/Contact.astro`
- Modify: `src/components/Footer.astro`

- [ ] **Step 1: Replace Contact stub**

Replace `src/components/Contact.astro`:
```astro
---
---
<section id="contact" class="px-8 md:px-16 py-16 bg-[#050505]">
  <div class="text-fire text-[9px] tracking-[4px] uppercase mb-4">— Contact</div>
  <h2 class="font-serif font-black text-white text-2xl md:text-3xl mb-8">Book an Event</h2>

  <div class="flex flex-wrap gap-10">
    <div>
      <div class="text-smoke text-[9px] tracking-[2px] uppercase mb-2">Restaurant</div>
      <a href="tel:3105733727" class="text-white text-base hover:text-fire transition-colors duration-200">
        (310) 573-3727
      </a>
    </div>
    <div>
      <div class="text-smoke text-[9px] tracking-[2px] uppercase mb-2">Catering</div>
      <a href="tel:3109951895" class="text-white text-base hover:text-fire transition-colors duration-200">
        (310) 995-1895
      </a>
    </div>
    <div>
      <div class="text-smoke text-[9px] tracking-[2px] uppercase mb-2">Email</div>
      <a
        href="mailto:kroccolevy@roccospalisades.com"
        class="text-teal text-base hover:text-white transition-colors duration-200"
      >
        kroccolevy@roccospalisades.com
      </a>
    </div>
    <div>
      <div class="text-smoke text-[9px] tracking-[2px] uppercase mb-2">Hours</div>
      <div class="text-white text-xs leading-relaxed">
        Mon–Fri: 10AM–8PM<br />
        Sat: 11AM–8PM<br />
        Sun: Closed
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Replace Footer stub**

Replace `src/components/Footer.astro`:
```astro
---
---
<footer class="bg-black border-t border-[#111] px-8 py-4 flex items-center gap-4">
  <span class="text-[#2a2a2a] text-[9px] tracking-[2px] uppercase whitespace-nowrap">
    © Rocco's Rides Again
  </span>
  <div
    class="flex-1 h-px"
    style="background: linear-gradient(90deg, transparent, #1a1a1a, transparent)"
  ></div>
  <span class="text-[#2a2a2a] text-[9px] tracking-[2px] uppercase whitespace-nowrap">
    Los Angeles
  </span>
</footer>
```

- [ ] **Step 3: Verify full build and do a complete visual pass**

```bash
npm run build && npm run dev
```
Open `http://localhost:4321` and check end-to-end:
- Sticky nav stays at top while scrolling
- Clicking "About" / "Menu" / "Contact" nav links smooth-scrolls to correct sections
- "Book Your Event" CTA scrolls to Contact section
- Phone numbers are tappable links (`tel:`)
- Email is a tappable link (`mailto:`)
- Footer copyright line renders at the bottom
- Resize to mobile (375px) — all sections stack cleanly, menu grid goes to 1 column

- [ ] **Step 4: Commit**

```bash
git add src/components/Contact.astro src/components/Footer.astro
git commit -m "feat: add contact section and footer"
```

---

## Task 9: GitHub Repo + Vercel Deploy

- [ ] **Step 1: Create GitHub repo**

Go to github.com → New repository → name it `roccos-rides-again` → private or public → **do not** initialize with README (we already have files).

- [ ] **Step 2: Push to GitHub**

```bash
git remote add origin https://github.com/<YOUR_USERNAME>/roccos-rides-again.git
git branch -M main
git push -u origin main
```

Replace `<YOUR_USERNAME>` with your GitHub username.

- [ ] **Step 3: Connect Vercel**

1. Go to vercel.com → Add New Project
2. Import `roccos-rides-again` from GitHub
3. Framework Preset: **Astro** (Vercel auto-detects)
4. Build Command: `npm run build` (auto-filled)
5. Output Directory: `dist` (auto-filled)
6. Click **Deploy**

- [ ] **Step 4: Verify live deploy**

Vercel gives you a URL like `roccos-rides-again.vercel.app`. Open it and confirm:
- Site loads over HTTPS
- Logo renders
- All sections present
- Smooth scroll works
- Phone/email links work on mobile

- [ ] **Step 5: (Optional) Add custom domain**

In Vercel project settings → Domains → add `roccospalisades.com` (or new domain). Vercel provides DNS instructions. This replaces the SiteGround FTP workflow entirely.

---

## Post-Launch: Updating Content

To update menu items or any content:
1. Edit the relevant component in `src/components/`
2. `git add` and `git commit`
3. `git push origin main`
4. Vercel auto-deploys in ~30 seconds

No FTP. No WordPress login. No Slice dashboard.
