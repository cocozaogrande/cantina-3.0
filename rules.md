# Execution Rules — Antigravity Agent

## TypeScript
- strict: true enforced — no `any`, no non-null assertions without // REASON comment
- All props interfaces must be explicitly typed
- All event handlers must be typed (e.g., React.ChangeEvent<HTMLInputElement>)
- All async functions must handle errors in try/catch with semantic log

## Tailwind
- Utility-first only — no @apply except in globals.css
- No dynamic string concatenation for class names (use cn() or clsx() if available)
- Responsive: mobile-first (no desktop-only defaults)

## File Operations
- Existing files: Git DIFF format only (unified diff, -3 context lines)
- New files: full content permitted
- Never rewrite a file entirely if it already exists
- Read before write — always run a targeted grep/cat before modifying

## Component Rules
- All components that use hooks: must be 'use client'
- All components using GSAP or browser APIs: must be dynamic import with ssr: false
- No client components at the page level if avoidable — prefer leaf-level client boundary

## Form Validation
- Validate on submit, show inline errors below each field
- Required fields: show error if empty on submit
- Price > 0 rule enforced numerically
- No HTML5 `required` attribute alone — validate in JS

## Image Upload
- Use FileReader.readAsDataURL() for base64 conversion
- Persist to localStorage only as base64 for demo
- Show real-time preview via object URL (URL.createObjectURL)
- Revoke object URL on component unmount (return () => URL.revokeObjectURL(objectUrl))
- Accept: image/jpeg, image/png, image/webp only — validate MIME type on selection

## Accessibility
- All interactive elements: aria-label
- All images: alt attribute
- Focus trap in modals
- Color contrast: minimum AA on all text

## Error Handling
```typescript
try {
  // operation
} catch (error) {
  console.error('[ComponentName][operationName]', error)
  // show user-facing toast or inline error
}
```

## Performance
- No unnecessary re-renders — memoize callbacks with useCallback where applicable
- No useEffect with missing dependencies — satisfy exhaustive-deps
- Lazy load images with next/image or native loading="lazy"
