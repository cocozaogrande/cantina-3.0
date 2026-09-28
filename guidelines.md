# UI Guidelines — Cantina App Extension

## Design System Authority
Before writing any component, read:
- The primary globals.css or equivalent token file
- Any existing card/button/input component files
These are the single source of truth. guidelines.md documents what exists, not what to invent.

## Typography
- Labels: uppercase, text-[11px], tracking-widest, text-white/50
- Headings: font-semibold, text-white
- Body: text-white/70
- Price/highlight: text-[#FFB800] (amber)
- Error: text-red-400
- No emojis anywhere

## Components Catalog (to be filled by S1 Audit)
- [ ] GradientButton: [path TBD]
- [ ] Avatar: [path TBD]
- [ ] Card/Glassmorphism: [pattern TBD]
- [ ] Input: [pattern TBD]
- [ ] Toggle: [pattern TBD]
- [ ] Modal: [path TBD or ABSENT → create in S2]

## Spacing Scale
- Section padding: px-4 py-6 (mobile-first)
- Card padding: p-4 sm:p-6
- Form field gap: space-y-4
- Grid gap: gap-4

## Input Pattern
```tsx
<input
  className="
    w-full bg-white/5 border border-white/10 rounded-lg px-4 py-3
    text-white placeholder:text-white/30
    focus:outline-none focus:border-[#FF6B35] focus:ring-1 focus:ring-[#FF6B35]/30
    transition-colors duration-200
  "
/>
```

## Error Pattern
```tsx
{error && (
  <span className="text-red-400 text-xs mt-1 block">{error}</span>
)}
```

## Toggle Pattern (orange, existing — read from project before writing)
Use the existing toggle component. Do not invent a new one.

## Back Header Pattern (all profile sub-pages)
```tsx
<header className="flex items-center gap-3 px-4 py-4 border-b border-white/10">
  <button onClick={() => router.back()} aria-label="Voltar">
    <ChevronLeft className="w-5 h-5 text-white" />
  </button>
  <h1 className="text-base font-semibold text-white">{title}</h1>
</header>
```

## No-No List
- No box-shadow
- No border-radius > rounded-xl (except pill buttons)
- No gradients on text (except via existing GradientButton)
- No inline styles (use Tailwind only)
- No emoji in JSX
- No hardcoded hex in className (use CSS variables or Tailwind config values)
