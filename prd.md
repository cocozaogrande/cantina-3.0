# PRD — Cantina App: Briefing 1 Feature Set

## Scope
Three feature groups added to existing Cantina App:
1. Admin Menu Product Management (/admin/menu, /admin/menu/novo, /admin/menu/[id]/editar)
2. Profile Sub-Pages (11 routes under /perfil/*)
3. Profile Photo Upload (enhancement to existing /perfil page)

## Exact Stack
- Framework: Next.js 14 App Router (src/app directory)
- Language: TypeScript strict (no `any`, no `!` assertions without comment)
- Styling: Tailwind CSS utility-first — no inline styles
- Forms: React controlled components + custom validation (no react-hook-form unless already present)
- Image upload: <input type="file"> + FileReader API for base64 + localStorage persistence
- No new dependencies to be installed unless GradientButton or Avatar component is ABSENT

## Design Tokens (source of truth — read from existing CSS before accepting these)
- Background: #0D0907
- Primary: #FF6B35
- Amber: #FFB800
- Glassmorphism card: bg-white/5 backdrop-blur-md border border-white/10
- Input focus ring: border-[#FF6B35]
- Error color: text-red-400 border-red-400
- Label style: uppercase text-[11px] tracking-widest text-white/50
- Font: (read from existing project — do not assume)

## Route Schema
### New Routes (Admin)
- /admin/menu — product grid management
- /admin/menu/novo — create product form
- /admin/menu/[id]/editar — edit product form (id = local mock id)

### New Routes (Profile)
- /perfil/meus-dados
- /perfil/alterar-pin
- /perfil/alunos-vinculados
- /perfil/historico-financeiro
- /perfil/chave-pix
- /perfil/extrato-completo
- /perfil/minhas-reservas
- /perfil/preferencias-cardapio
- /perfil/falar-cantina
- /perfil/termos-de-uso
- /perfil/politica-de-privacidade

## TypeScript Interfaces

```typescript
// types/product.ts
export interface Product {
  id: string
  name: string
  description?: string
  category: ProductCategory
  priceInCents: number
  dailyLimit?: number
  isActive: boolean
  imageUrl?: string    // object URL (local demo)
  imageBase64?: string // fallback for persistence
}

export type ProductCategory =
  | 'Lanches'
  | 'Bebidas'
  | 'Sobremesas'
  | 'Combos'
  | 'Barrinhas'

// types/transaction.ts
export interface Transaction {
  id: string
  date: string         // ISO 8601
  description: string
  amountInCents: number
  type: 'credit' | 'debit'
}

// types/reservation.ts
export interface Reservation {
  id: string
  date: string
  time: string
  item: string
  status: 'Confirmada' | 'Pendente' | 'Cancelada'
}
```

## State Architecture
- useProductStore: useState in /admin/menu/page.tsx (no Zustand needed for demo)
- useProfilePhotoStore: localStorage key `cantina_profile_photo` — base64 string
- All profile sub-pages: local state only, no server interaction for demo

## Constraints
- Do NOT modify: existing routes, saldo logic, pedidos logic, reservas logic, bottom navigation
- No emojis in any component
- No Three.js, no Framer Motion (unless already present in project)
- No new npm packages unless strictly unavailable natively
