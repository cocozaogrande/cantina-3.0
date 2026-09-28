# CLAUDE.md — Cantina Saudável School Cafeteria App

## Project Overview
Cantina Saudável is a mobile-first web app designed to digitize school cafeteria operations.
It replaces the physical notebook used to track student debts, enables PIX payments,
and allows students to pre-order snacks before arriving at school.

This is a high-fidelity mockup built to impress stakeholders in a sales meeting.
Every screen must look production-ready, polished, and trustworthy.

## Target Users
- **Students / Parents**: Browse menu, view balance/debt, pay via PIX, pre-order meals
- **Cafeteria Admin**: Log new orders, manage student accounts, view debts, confirm payments

## Stack
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript (strict mode)
- **Styling**: Tailwind CSS + custom CSS variables
- **UI Components**: shadcn/ui
- **Icons**: Lucide React
- **Charts**: Recharts (admin dashboard)
- **Animations**: Framer Motion
- **Mock Data**: Static JSON files in /data/ — no backend required for mockup
- **State**: React Context + useState (no external state library needed)

## Design System

### Color Palette
```css
--color-primary: #FF6B35;        /* Warm orange — energy, food, action */
--color-primary-dark: #E85520;
--color-secondary: #2ECC71;      /* Green — PIX, payments, success */
--color-secondary-dark: #27AE60;
--color-dark: #1C1C2E;           /* Deep navy — backgrounds, text */
--color-surface: #FFFFFF;
--color-surface-alt: #F4F4F8;
--color-text-primary: #1C1C2E;
--color-text-muted: #6B7280;
--color-danger: #EF4444;
--color-warning: #F59E0B;
--color-pix: #32BCAD;            /* Official PIX brand color */
```

### Typography
- **Display**: `Sora` (Google Fonts) — headings, brand name
- **Body**: `Inter` — paragraphs, labels, data
- **Mono**: `JetBrains Mono` — codes, PIX keys, transaction IDs

### Border Radius
- Cards: `16px`
- Buttons: `12px`
- Inputs: `10px`
- Avatars: `full`

### Shadows
- Card: `0 2px 16px rgba(0,0,0,0.07)`
- Modal: `0 8px 40px rgba(0,0,0,0.15)`
- Bottom nav: `0 -2px 20px rgba(0,0,0,0.08)`

## File Structure

/app
/student — student-facing routes
/admin — cafeteria admin routes
/api — mock API routes (static data)
/components
/ui — shadcn components
/shared — reusable components (BalanceBadge, OrderCard, etc.)
/student — student-specific components
/admin — admin-specific components
/data
students.json — mock student accounts
orders.json — mock order history
menu.json — cafeteria menu items
transactions.json — payment history
/lib
mock-data.ts — data access helpers
utils.ts — formatters (currency, date, PIX)
/public
/icons — app icons


## Core Conventions
- Mobile-first (375px base), responsive up to tablet (768px)
- All monetary values in BRL, formatted as `R$ 0,00`
- PIX payment flow is SIMULATED — no real API calls
- Mock data must feel realistic: Brazilian names, real item names, plausible prices
- All UI text in Brazilian Portuguese
- Loading states on every async action (even if fake)
- Every destructive action needs a confirmation modal

## Mock Data Rules
- At least 12 student accounts in students.json
- At least 5 students with outstanding debts
- At least 3 recent orders per student
- Menu must have at least 15 items across categories: Lanches, Bebidas, Sobremesas, Combos
- Transaction history must include PIX payments, pending items, and cancelled orders

## Quality Bar
A screen is done when:
- [ ] It looks like a real, shipped product — not a wireframe
- [ ] Mobile viewport (375px) looks perfect
- [ ] Loading/empty/error states exist
- [ ] Interactions feel responsive (hover, active states)
- [ ] Typography hierarchy is clear
- [ ] No layout breaks at 320px or 768px

## Skills Location
Always check `/mnt/skills/` before writing code. Load:
- `frontend-design/SKILL.md` before any UI implementation
- `docx/SKILL.md` if generating documentation
- Read the relevant SKILL.md FIRST, then write code.
