# CLAUDE.md — Frontend Website Rules

## Always Do First
- **Invoke the `frontend-design` skill** before writing any frontend code, every session, no exceptions.

## Reference Images
- If a reference image is provided: match layout, spacing, typography, and color exactly. Swap in placeholder content (images via `https://placehold.co/`, generic copy). Do not improve or add to the design.
- If no reference image: design from scratch with high craft (see guardrails below).
- Screenshot your output, compare against reference, fix mismatches, re-screenshot. Do at least 2 comparison rounds. Stop only when no visible differences remain or user says so.

## Local Server
- **Always serve on localhost** — never screenshot a `file:///` URL.
- Start the dev server: `node serve.mjs` (serves the project root at `http://localhost:3000`)
- `serve.mjs` lives in the project root. Start it in the background before taking any screenshots.
- If the server is already running, do not start a second instance.

## Screenshot Workflow
- Puppeteer is installed at `C:/Users/nateh/AppData/Local/Temp/puppeteer-test/`. Chrome cache is at `C:/Users/nateh/.cache/puppeteer/`.
- **Always screenshot from localhost:** `node screenshot.mjs http://localhost:3000`
- Screenshots are saved automatically to `./temporary screenshots/screenshot-N.png` (auto-incremented, never overwritten).
- Optional label suffix: `node screenshot.mjs http://localhost:3000 label` → saves as `screenshot-N-label.png`
- `screenshot.mjs` lives in the project root. Use it as-is.
- After screenshotting, read the PNG from `temporary screenshots/` with the Read tool — Claude can see and analyze the image directly.
- When comparing, be specific: "heading is 32px but reference shows ~24px", "card gap is 16px but should be 24px"
- Check: spacing/padding, font size/weight/line-height, colors (exact hex), alignment, border-radius, shadows, image sizing

## Output Defaults
- Single `index.html` file, all styles inline, unless user says otherwise
- Tailwind CSS via CDN: `<script src="https://cdn.tailwindcss.com"></script>`
- Placeholder images: `https://placehold.co/WIDTHxHEIGHT`
- Mobile-first responsive

## Brand Assets
- Always check the `brand_assets/` folder before designing. It may contain logos, color guides, style guides, or images.
- If assets exist there, use them. Do not use placeholders where real assets are available.
- If a logo is present, use it. If a color palette is defined, use those exact values — do not invent brand colors.

## Brand Guidelines

### Theme
- **Frosted glass** — transparency, backdrop-filter blur, layered surfaces with glass morphism
- Surfaces should feel elevated and translucent, showing what's behind them

### Color Palette
- **Primary accent:** Orange `#e8832a` (warm, energetic)
- **Secondary accent:** Blue `#3b82f6` (trust, technology)
- **Hero section:** Black + white + orange only. No blue in the hero.
- **Rest of site:** Blue gradually introduced alongside orange (alternating icons, stats, subtle glows)
- **Dark surfaces:** `#0a0f1a` (deep), `#0f172a` (navy), `#1e293b` (mid)
- **Light surfaces:** `#ffffff` (light), `#f8fafc` (cream), `#f1f5f9` (cream-dark)

### Typography
- **Headings & titles:** Inter (400–700 weight). Keep sizes modest and readable — avoid oversized display text.
- **Body & subtext:** Fira Sans (300–700 weight). Line-height 1.7 for body copy.
- **Max heading sizes:** Hero ~4.2rem, Section ~2.4rem, Card titles ~1.35rem. Never exceed these.

### Button System
- **Primary CTA (dark glow):** `.btn-glow` — dark background with blurred orange gradient
- **Secondary CTA (pill):** `.btn-pill` — orange pill with sliding dark circle + arrow

## Anti-Generic Guardrails
- **Colors:** Use the brand palette (orange #e8832a, blue #3b82f6). Never use default Tailwind indigo/purple.
- **Shadows:** Never use flat `shadow-md`. Use layered, color-tinted shadows with low opacity.
- **Typography:** Inter for headings, Fira Sans for body. Keep headings small and readable — no massive display text.
- **Gradients:** Layer multiple radial gradients. Add grain/texture via SVG noise filter for depth.
- **Animations:** Only animate `transform` and `opacity`. Never `transition-all`. Use spring-style easing.
- **Interactive states:** Every clickable element needs hover, focus-visible, and active states. No exceptions.
- **Images:** Add a gradient overlay (`bg-gradient-to-t from-black/60`) and a color treatment layer with `mix-blend-multiply`.
- **Spacing:** Use intentional, consistent spacing tokens — not random Tailwind steps.
- **Depth:** Surfaces should have a layering system (base → elevated → floating), not all sit at the same z-plane.

## Deployment Workflow
- GitHub → Netlify sync is automatic. Pushing to GitHub deploys to production.
- **Test all changes on localhost** until the user explicitly says to push/commit to GitHub.
- Never run `git push` or `git commit` unless the user explicitly asks.

## Hard Rules
- Do not add sections, features, or content not in the reference
- Do not "improve" a reference design — match it
- Do not stop after one screenshot pass
- Do not use `transition-all`
- Do not use default Tailwind blue/indigo as primary color
