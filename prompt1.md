VISUAL IDENTITY BRIEF
─────────────────────
Background:   #070711 / #0B0620 / #120A2E — cool, dark violet, cinematic, near-black
Primary text: #F6F2FF — thin to medium weight, elegant, high-contrast
Muted text:   #B8A9D9 / #8E80B8 — lavender gray, used for body copy and secondary labels
Accent:       #FF3FD7 / #B45CFF / #6C7BFF — CTAs, luminous borders, highlights, glow details
Surface:      rgba(255,255,255,0.06) — glass cards, panels, navigation, soft overlays

Display font: refined geometric sans similar to Gotham / Aeonik / Satoshi / Neue Montreal — use local fonts if available, otherwise use next/font with a high-quality Google alternative
Body font:    elegant readable sans — 14px–20px, strong mobile readability
Label/mono:   optional mono or narrow label style for metadata, tags, counters, and futuristic UI details

Border radius: 20px–32px for cards, 999px for pills/buttons
Shadow system: soft violet/magenta glow, subtle depth, no harsh shadows
Spacing unit: 8px grid, generous editorial whitespace
Motion feel: smooth, cinematic, premium, restrained
Scroll type: reveal/parallax/sticky/scrub only where described in site_reference.md

Signature element:
A cinematic futuristic portfolio hero with a refined female UX/UI specialist portrait composition, luminous violet/magenta/blue atmosphere, glass UI fragments, soft halos, and premium editorial typography.

## GOAL

Set up the complete production-ready foundation for a high-fidelity futuristic premium UX/UI portfolio site in Next.js, TypeScript, and Tailwind, based on `site_reference.md` and the attached visual reference, without fully building all final sections yet.

## CONTEXT

You are working inside an existing project repository.

The final site must recreate the structure, atmosphere, visual language, interaction quality, and responsive behavior described in `site_reference.md`. This file exists inside the project and contains approximately 1,000 lines of detailed analysis covering sections, layout, typography, colors, spacing, assets, visual effects, animations, responsiveness, and behavior.

The attached reference image is an additional visual reference. Treat it as a visual north star for mood, composition, lighting, hierarchy, density, glow intensity, glassmorphism, portrait treatment, and premium futuristic atmosphere.

The target site is a personal portfolio for a UX/UI specialist. The aesthetic is futuristic editorial luxury: dark violet/blue-black background, cinematic magenta and violet halos, glass panels, refined thin typography, luminous cards, elegant spacing, and polished mobile-first composition.

Before writing or changing code, inspect:

* The full project structure.
* Existing package manager and dependencies.
* Existing Next.js setup, if any.
* Existing TypeScript configuration.
* Existing Tailwind configuration.
* Existing app/page structure.
* Existing components.
* Existing assets.
* Existing styling files.
* Existing lint/build scripts.
* `site_reference.md`.
* `skills/` folder and every relevant skill inside it.
* `CLAUDE.md`, even though it was written for Claude, because it may contain useful project rules.
* `AGENTS.md`, `.codex/`, `README.md`, or any other project instruction files if present.

Use every relevant available skill, subagent, plugin, screenshot-analysis tool, browser/visual-inspection tool, image/asset-generation tool, code-review tool, and validation tool that exists in this environment and can improve the result. Do not invent unavailable tools. If a tool is not available, proceed with the best available implementation path.

Required stack:

* Next.js 14+ with App Router.
* TypeScript.
* Tailwind CSS v3.
* CSS custom properties for design tokens.
* Reusable React components.
* Mobile-first layout.
* Modern CSS.
* GSAP 3 + ScrollTrigger prepared for complex scroll animation when needed.
* `@gsap/react` with `useGSAP()` if GSAP animations are implemented later.
* Framer Motion only for microinteractions or UI transitions when appropriate.
* Lucide React or another consistent icon system only if icons are needed.
* Deploy-ready structure.
* No TypeScript errors.
* No broken routes.
* No visible placeholders in the foundation UI.

## SPEC

1. Inspect before changing

   * Do not overwrite the project blindly.
   * First inspect all relevant files and folders.
   * Identify the current framework, package manager, styling approach, scripts, and architecture.
   * Preserve useful existing code.
   * Only replace or restructure files when it clearly improves maintainability and matches the required implementation plan.
   * If the repository is empty or incomplete, create the missing Next.js foundation cleanly.

2. Read and extract the reference

   * Read `site_reference.md` completely before implementation.
   * Extract the following into your working understanding:

     * Section order.
     * Visual identity.
     * Layout grid.
     * Desktop composition.
     * Tablet behavior.
     * Mobile behavior.
     * Typography scale.
     * Font personality.
     * Color palette.
     * Spacing rhythm.
     * Glassmorphism rules.
     * Glow/halo usage.
     * Card system.
     * Button system.
     * Navigation behavior.
     * Hero composition.
     * Asset requirements.
     * Animation requirements.
     * Interaction behavior.
     * Accessibility notes.
   * Keep consulting `site_reference.md` continuously while working, not only at the beginning.
   * If the attached image is available to inspect, analyze it for visual details and use it to refine tokens and layout direction.

3. Create or normalize the project architecture
   Adapt to the existing project, but aim for this clean structure:

   app/
   layout.tsx
   page.tsx
   globals.css

   components/
   layout/
   Container.tsx
   Section.tsx
   SiteHeader.tsx
   SiteFooter.tsx
   sections/
   ui/
   GlassCard.tsx
   GradientButton.tsx
   SectionHeading.tsx
   Eyebrow.tsx
   visual/
   GlowOrb.tsx
   DecorativeGrid.tsx
   ResponsiveImageFrame.tsx
   motion/
   MotionProvider.tsx

   data/
   portfolio.ts

   lib/
   utils.ts
   motion.ts

   public/
   assets/
   generated/
   textures/
   portraits/
   project-covers/

   gpt.md

   Keep the architecture prepared for these final sections:

   * Header/navigation.
   * Hero.
   * Featured projects/case studies.
   * Services/expertise.
   * Process/methodology.
   * Testimonials/social proof.
   * Contact/call to action.
   * Footer.
   * Background lighting system.
   * Glass cards.
   * Buttons.
   * Section wrappers.
   * Responsive grids.
   * Animation wrappers.

4. Configure design tokens
   Create a serious token system using CSS variables in `app/globals.css`.

   Required base tokens:

   :root {
   --color-bg: #070711;
   --color-bg-deep: #05040D;
   --color-bg-violet: #120A2E;
   --color-bg-blueblack: #060A18;

   --color-text: #F6F2FF;
   --color-text-muted: #B8A9D9;
   --color-text-soft: #8E80B8;

   --color-accent: #FF3FD7;
   --color-accent-violet: #B45CFF;
   --color-accent-blue: #6C7BFF;

   --color-surface: rgba(255, 255, 255, 0.06);
   --color-surface-strong: rgba(255, 255, 255, 0.11);
   --color-border: rgba(255, 255, 255, 0.16);
   --color-border-strong: rgba(255, 255, 255, 0.28);

   --radius-card: 28px;
   --radius-panel: 36px;
   --radius-pill: 999px;

   --shadow-glow: 0 0 80px rgba(255, 63, 215, 0.22);
   --shadow-violet: 0 24px 90px rgba(91, 57, 255, 0.22);
   --shadow-glass: 0 24px 80px rgba(0, 0, 0, 0.35);

   --spacing-section: clamp(72px, 12vw, 160px);
   --spacing-section-tight: clamp(56px, 8vw, 112px);
   --container-max: 1180px;
   --container-wide: 1360px;
   }

   Also define reusable gradients:

   * Dark radial page background.
   * Magenta/violet glow.
   * Blue-violet glow.
   * Subtle glass border gradient.
   * Hero halo gradient.
   * CTA gradient.
   * Section divider fade.

   Use these tokens through Tailwind utilities or CSS classes. Avoid random hardcoded colors. If a new token is needed, add it intentionally and document it in `gpt.md`.

5. Configure typography

   * Use `next/font`.
   * Prefer local premium fonts if the project already includes them.
   * If no local premium font exists, use a high-quality Google Font combination.
   * Strong recommended fallback:

     * Display: `Outfit`, `Manrope`, `Plus Jakarta Sans`, or `Inter Tight`.
     * Body: same family or compatible refined sans.
   * Use thin/regular display weights for large titles.
   * Use controlled letter spacing:

     * Large display headings: slightly negative or tight tracking.
     * Eyebrows/labels: uppercase, wider tracking.
     * Body: normal tracking for readability.
   * Define global typography behavior:

     * Font smoothing.
     * Consistent line-height.
     * Responsive heading clamps.
     * Strong mobile readability.
   * Prepare reusable typography components/classes:

     * Eyebrow label.
     * Display heading.
     * Section title.
     * Body paragraph.
     * Metadata label.

6. Configure global visual base
   In `app/globals.css`, create the global atmosphere:

   * Dark violet/blue-black body background.
   * Subtle radial gradients.
   * Safe overflow handling.
   * Selection color.
   * Focus-visible style.
   * Smooth scrolling only if appropriate and accessible.
   * Reduced motion media query.
   * Base glass utility.
   * Base glow utility.
   * Base container utility if helpful.
   * Prevent horizontal overflow globally.

   The page should already feel visually aligned with the premium futuristic direction, even before all final sections are implemented.

7. Tailwind configuration

   * Extend Tailwind with the token system where useful.
   * Add custom colors mapped to CSS variables.
   * Add custom border radius values.
   * Add custom shadows/glows.
   * Add container sizing if appropriate.
   * Keep Tailwind config maintainable.
   * Do not create an oversized theme with unused values.

8. Base components
   Create reusable components with production-level implementation quality.

   Required components:

   Container

   * Handles max width.
   * Supports default, wide, and narrow variants if useful.
   * Uses responsive horizontal padding.

   Section

   * Handles semantic section wrapper.
   * Supports spacing variants.
   * Allows optional id.
   * Prevents layout inconsistencies.

   GlassCard

   * Uses translucent surface.
   * Uses subtle border.
   * Uses backdrop blur carefully.
   * Uses glow only when requested.
   * Supports className extension.

   GradientButton

   * Supports primary and secondary variants.
   * Includes hover, active, and focus-visible states.
   * Uses accessible button/link semantics.
   * Uses pill radius.
   * Feels premium, not generic.

   SectionHeading

   * Supports eyebrow, title, description.
   * Uses refined typography scale.
   * Supports centered or left alignment.
   * Prepared for animation wrappers later.

   Eyebrow

   * Uppercase or small label style.
   * Uses subtle accent/ muted text.
   * Avoids loud neon styling.

   GlowOrb

   * Decorative absolutely positioned glow.
   * Configurable size, intensity, position, color variant.
   * Mark decorative elements as aria-hidden where appropriate.

   DecorativeGrid

   * Subtle futuristic grid/line texture.
   * Must be restrained and premium.
   * Should not reduce readability.

   ResponsiveImageFrame

   * Prepares consistent image framing.
   * Supports portrait/project visual ratios.
   * Uses border/glass/glow language.
   * Does not reference missing images.

   Motion utilities

   * Prepare a structure for future GSAP/ScrollTrigger and Framer Motion integration.
   * Include reduced-motion helpers.

9. Data model
   Create `data/portfolio.ts` with structured content for the future full implementation.

   Include:

   * Navigation items.
   * Hero copy.
   * Projects.
   * Services.
   * Process steps.
   * Testimonials.
   * Contact links.
   * Footer links.

   Use polished realistic example content for a senior UX/UI specialist. Do not use lorem ipsum. Keep content concise, premium, and appropriate to the reference.

   Example content direction:

   * UX strategy.
   * Interface design.
   * Design systems.
   * Conversion-focused product design.
   * AI/SaaS dashboards.
   * Mobile product experiences.
   * Brand-to-product systems.

10. Initial page shell
    Implement only a foundation-level page shell in `app/page.tsx`.

It may include:

* Site background.
* Header placeholder as a real component with real nav data.
* A minimal hero scaffold showing the visual direction.
* Section placeholders only if they are styled as intentional structural scaffolding and do not look unfinished.
* Prefer not to build all detailed final sections in this prompt.

Important:

* Do not leave visible text like “TODO”, “placeholder”, “coming soon”, or “lorem ipsum”.
* The foundation should be visually coherent and executable.
* The detailed full-page build belongs to Prompt 2.

11. Animation preparation

* Install or configure GSAP only if missing and clearly needed.
* Prepare for ScrollTrigger but do not overbuild the final animation system yet.
* If `@gsap/react` is installed or added, use `useGSAP()` for future React cleanup patterns.
* Add a reduced-motion strategy now.
* Create `lib/motion.ts` with reusable animation constants, durations, easings, or helper functions.
* Do not create complex scroll timelines yet unless needed for the foundation.

12. Asset preparation

* Create asset folders.
* Configure safe image handling.
* Do not reference nonexistent assets.
* Add simple CSS/SVG decorative assets if helpful for the atmosphere.
* Document the future asset strategy in `gpt.md`.
* The real portrait, project covers, and final generated visuals will be implemented in Prompt 2.

13. Documentation in `gpt.md`
    Create `gpt.md` in the project root.

Include these sections:

# GPT Implementation Notes

## Project Objective

Explain the goal: high-fidelity futuristic premium UX/UI portfolio based on `site_reference.md` and visual reference.

## Reference Summary

Summarize the extracted direction from `site_reference.md`.

## Visual Identity

Register colors, typography, surfaces, shadows, glow, spacing, and overall aesthetic.

## Architecture

Document folder structure and why it was chosen.

## Components

List created base components and their responsibilities.

## Data Structure

Explain `data/portfolio.ts`.

## Implementation Rules

Include rules for preserving fidelity, avoiding placeholders, keeping code modular, and consulting `site_reference.md`.

## Responsiveness Rules

Document mobile-first layout principles and target breakpoints.

## Animation Rules

Document GSAP/ScrollTrigger/Framer Motion usage rules, including reduced motion.

## Asset Strategy

Explain asset folders, intended generated assets, and no-broken-image policy.

## Dependencies

List dependencies used or added and why.

## Pending Items

List what Prompt 2 must implement.

## Quality Checklist

Include foundation validation status.

## Codex Decision History

Log important decisions made during this prompt.

Update `gpt.md` before finishing.

14. Quality bar
    The result of Prompt 1 must be:

* Clean.
* Executable.
* Modular.
* Visually aligned with the reference direction.
* Ready for high-fidelity implementation in Prompt 2.
* Documented.
* Free of obvious technical errors.

## CONSTRAINTS

* Do not build the full final site in this step.
* Do not skip reading `site_reference.md`.
* Do not ignore the attached reference image if available.
* Do not ignore relevant files in `skills/`, `CLAUDE.md`, `.codex/`, `AGENTS.md`, or README files.
* Do not delete useful existing project code without inspection.
* Do not create a generic SaaS landing page.
* Do not use flat white sections.
* Do not use random bright neon colors.
* Do not use heavy cyberpunk clutter.
* Do not use purple gradients without hierarchy or purpose.
* Do not use harsh shadows.
* Do not use low-quality stock-image assumptions.
* Do not leave visible placeholders.
* Do not use lorem ipsum.
* Do not leave broken images.
* Do not leave empty cards or empty sections.
* Do not create horizontal overflow.
* Do not install unnecessary libraries.
* Do not create duplicate components.
* Do not hardcode repeated visual values instead of tokens.
* Do not implement GSAP with unsafe cleanup patterns.
* Do not ignore `prefers-reduced-motion`.
* Do not make desktop the only polished viewport.
* Do not finish without updating `gpt.md`.

## VERIFY

Before finishing, complete this validation sequence:

1. Confirm `site_reference.md` was fully read.
2. Confirm relevant skills and project instruction files were inspected.
3. Confirm the project runs locally.
4. Run the available lint command.
5. Run the available typecheck command, or add/use a suitable TypeScript validation command if missing.
6. Run the production build command.
7. Fix all errors found.
8. Inspect the page at minimum at:

   * 375px mobile
   * 430px large mobile
   * 768px tablet
   * 1024px small desktop
   * 1440px desktop
9. Confirm no horizontal overflow.
10. Confirm the global visual foundation matches the dark violet futuristic premium direction.
11. Confirm the base components render correctly.
12. Confirm no visible lorem ipsum, TODO, placeholder labels, broken images, or empty blocks.
13. Confirm focus-visible styles exist for interactive elements.
14. Confirm reduced-motion strategy exists.
15. Confirm `gpt.md` exists and contains:

* Objective.
* Reference summary.
* Visual identity.
* Architecture.
* Components.
* Data structure.
* Implementation rules.
* Responsiveness rules.
* Animation rules.
* Asset strategy.
* Dependencies.
* Pending items for Prompt 2.
* Quality checklist.
* Codex decision history.

End by reporting only:

* What was created or changed.
* What validation commands were run.
* Whether each validation passed.
* What remains for Prompt 2.
