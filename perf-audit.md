# Performance Audit

## Stack Fingerprint
- Framework: [detect from package.json]
- Bundler: [Vite / Webpack / Turbopack / etc]
- Renderer: [Next.js App Router / Pages / Remix / Astro / etc]
- Animation libraries: [GSAP / Framer Motion / CSS only / etc]
- Scroll library: [Lenis / Locomotive / native / etc]
- Image handling: [next/image / manual / Cloudinary / etc]
- Font loading: [next/font / @font-face / Google Fonts CDN / etc]

## Current Lighthouse Scores (run on production or `next build && next start`)
- Performance: __
- LCP: __
- CLS: __
- INP: __
- TTFB: __
- TBT: __

## Bundle Analysis (run: npx @next/bundle-analyzer or npx vite-bundle-analyzer)
- Total initial JS (gzipped): __ KB
- Largest chunks: [list top 5 with sizes]
- Unused JS on home route: __ KB
- Third-party scripts total: __ KB

## Bottleneck Priority List (fill before writing a single diff)
| # | Bottleneck | Metric Impact | Root Cause | Files Involved |
|---|------------|--------------|-----------|----------------|

## Confirmed Visual Snapshot
Before any changes: [describe the visual behavior of the site in one paragraph so we can verify nothing changed after optimization]
