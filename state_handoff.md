# State Handoff — S4 → S5

## Receiving Agent (S5 — Profile Photo Upload + Profile Page Wiring)

## Context
S4 has created all 11 profile sub-pages under `app/student/perfil/*/page.tsx`.
All pages use `ProfilePageShell` and the `.glass-card` glassmorphism pattern.

## What S4 Built
11 pages under `app/student/perfil/`:
- `meus-dados` — editable name/class form, readonly email/matricula
- `alterar-pin` — 4-digit PIN change with validation + success state
- `alunos-vinculados` — main student card + disabled add button
- `historico-financeiro` — balance card + transaction list
- `chave-pix` — display/edit/copy for PIX key
- `extrato-completo` — filterable transaction list with period pills
- `minhas-reservas` — reservation cards with color-coded status badges
- `preferencias-cardapio` — toggles per category, persisted to localStorage
- `falar-cantina` — contact form with simulated send + success state
- `termos-de-uso` — 6-section legal text
- `politica-de-privacidade` — 7-section privacy policy

## IMPORTANT: Route Note
All sub-pages live at `/student/perfil/*` (NOT `/perfil/*`).
The existing `app/student/profile/page.tsx` currently uses `showToast` instead of navigating.
S5 must wire up the profile page rows to navigate to the correct `/student/perfil/*` routes.

## What S5 Must Implement
1. **Wire up `app/student/profile/page.tsx`** — change `onClick` on each row to navigate to the correct `/student/perfil/*` route instead of showing toast.
2. **Profile Photo Upload** — add photo upload capability to the existing profile page header area using the `ProfileAvatar` component and `cantina_profile_photo` localStorage key.

## DO NOT
- Rewrite the entire profile page — surgical diff edits only.
- Modify any of the 11 sub-pages created in S4.
- Add new npm packages.
