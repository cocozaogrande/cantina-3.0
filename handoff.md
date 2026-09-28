# Handoff Document — Cantina App Briefing 1

## Atualização — pipoca e correção de produtos reais no cardápio — 2026-09-18

- Cardápio do aluno: o item que aparecia como `Fruta da estação` com foto de pizza foi corrigido para `Mini pizza individual`, com descrição, preço, categoria e imagem coerentes.
- Produto `Pipoca salgada` adicionado ao cardápio em `Lanches`, usando a imagem real `public/images/products/pipoca.png`, com preço e descrição em português.
- Cardápio Admin: os produtos mockados deixaram de apontar para imagens `.webp` inexistentes e agora usam fotos reais `.png` já presentes em `public/images/products`, incluindo a pipoca.
- Verificação local: `menu.json` válido, imagens `pipoca.png` e `fruta-1.png` respondendo `200` no servidor local, sem referências `.webp` quebradas nos arquivos do app.
- QA aprovado: `npx tsc --noEmit`, `npx eslint` e `npm run build` (27 rotas) concluídos sem erros.
- Vercel Production READY: `https://cantina-app-seven.vercel.app` · deployment `https://cantina-kvulsghcd-cocozaograndes-projects.vercel.app` · inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/5xo12tfdtyHRVDToys779Yh8uFDz`.

## Cadastro de conta do aluno — 2026-09-13

- O login do aluno (`/student/login`) agora exibe **Não tem uma conta? → Criar uma conta**.
- Fluxo frontend em três etapas: dados da conta (nome completo, e-mail, telefone e senha), aviso de envio do código e confirmação.
- No modo demonstração, qualquer código não vazio é aceito; após confirmar, o e-mail e a senha ficam preenchidos no login e uma confirmação é exibida.
- A implementação é exclusiva do fluxo do aluno; o login administrativo não foi alterado.
- A confirmação de e-mail é simulada e deverá ser conectada ao backend quando ele existir.
- Validação visual concluída no viewport de 375px; `npm run lint`, TypeScript e build Vercel aprovados.
- Vercel Production READY: `https://cantina-app-seven.vercel.app`
- Deployment: `https://cantina-iyrvtn5h8-cocozaograndes-projects.vercel.app`
- Inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/Fgqdj9ep6L5eEpCrWfQnn6HNC823`

## Auditoria e Otimização de Performance — 2026-09-13

Ciclo completo de auditoria e otimização de performance, com restrição absoluta de **zero mudança visual**. Todas as alterações são invisíveis ao usuário final.

**Imagens:**
- 12 PNGs de produtos (`public/images/products/`, 1.8–2.3MB cada, 23.3MB total) convertidos para WebP via `sharp` (qualidade 82) — redução de 92–96% por arquivo, 1.43MB total. PNGs originais mantidos como fonte (não deletados).
- Script reutilizável criado em `scripts/optimize-images.js`; rodar com `npm run optimize-images` sempre que novas imagens forem adicionadas em `/public`.
- Referências `.png` → `.webp` atualizadas em `data/menu.json` (12 itens) e `app/admin/menu/page.tsx` (6 produtos mock).
- `MenuItemImage.tsx` já estava otimizado de sessão anterior (blur placeholder, priority loading, sizes) — nenhuma mudança necessária.
- 3 tags `<img>` nativas identificadas (`AvatarUpload`, `ProductImageUpload`, `student/home`) — mantidas como estão: são pré-visualizações client-side de data URLs recém-capturadas (upload/crop), incompatíveis com `next/image` e sem imagem estática a otimizar.

**JavaScript bundle:**
- `'use client'` removido de 7 componentes puramente apresentacionais sem hooks/handlers: `BalanceBadge`, `LoadingSpinner`, `MoneyDisplay`, `OrderStatusBadge`, `PaymentMethodBadge`, `PixBadge`, `StudentAvatar`.
- `NewOrderDrawer` (admin) e `OrderDetailModal` (student) convertidos para `dynamic(..., { ssr: false })` nos 4 pontos de uso (`admin/orders`, `admin/dashboard`, `student/orders`, `student/home`) — code-split de modais/drawers não visíveis no carregamento inicial.
- Todos os imports de `lucide-react` já eram nomeados (nenhum wildcard encontrado).

**Fontes:**
- Migrado de `@import` do Google Fonts (bloqueante, no `globals.css`) para `next/font/google` em `app/layout.tsx` — Sora, Inter, JetBrains Mono com `display: 'swap'`, `preload: true` nas fontes principais, apenas os pesos realmente usados (400/500/600/700).
- Variáveis CSS em `globals.css` atualizadas para referenciar as fontes auto-hospedadas via CSS vars (`--font-sora`, `--font-inter`, `--font-jbmono`), preservando exatamente a mesma família/peso/fallback visual.

**Config:**
- `next.config.ts`: adicionado `compress: true`, `images.formats: ['avif', 'webp']`, `deviceSizes`/`imageSizes` ajustados ao breakpoint do projeto, e `headers()` com cache imutável para `/_next/static` e `/images`.
- `vercel.json` criado (não existia): headers de segurança (`X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy`) + cache imutável para assets estáticos.
- `eslint.config.mjs`: `scripts/**` adicionado aos ignores (script Node standalone usa CommonJS `require`, não é código do app).
- `sharp` promovido de dependência transitiva do Next.js para devDependency explícita (usado pelo script de otimização).

**Itens avaliados e descartados (sem risco/benefício):**
- Tailwind `content` paths: N/A — projeto usa Tailwind v4 com detecção automática, sem `tailwind.config.*`.
- `will-change`: nenhuma classe ativa anima `transform`/`opacity` continuamente (`.float-card` existe no CSS mas não é usada em nenhum componente — CSS morto, não removido pois está fora do escopo de otimização visual); shimmer de imagem anima `background-position`, não se beneficia de `will-change`.
- `useCallback`/`useMemo`: não aplicados especulativamente — nenhum componente memoizado (`React.memo`) que justificasse a otimização foi identificado nesta passada.

**Validação:** `npm run lint`, `npx tsc --noEmit` e `npm run build` (27 rotas) aprovados sem erros após cada fase.
**Deploy:** `https://cantina-app-seven.vercel.app` · deployment `https://cantina-7nsviglk6-cocozaograndes-projects.vercel.app` · inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/E4GBtfDVjaVLBQEQFQi3RaC6pyrR`

---

## Atualização — 2026-09-12: experiência desktop e conta do aluno

- A home pública (`/`) agora é responsiva para PC, com hero em duas colunas, resumo visual da experiência e CTAs claros para aluno e cantina; permanece fluida em 375px sem overflow horizontal.
- A área autenticada do aluno ganhou sidebar no desktop, cabeçalho de contexto e conteúdo amplo; a navegação inferior original continua exclusivamente em telas móveis.
- A home do aluno foi reorganizada como dashboard desktop com saldo, próxima retirada, ações rápidas, destaques e pedidos recentes. A versão móvel permanece focada e navegável.
- Perfil simplificado: removidos Alterar PIN, Alunos vinculados, Histórico financeiro, Chave PIX cadastrada, Termos de uso e Política de privacidade.
- `Meus dados` concentra foto, telefone, e-mail, informações acadêmicas e alteração simulada de senha; foto e telefone usam armazenamento local no modo demo.
- `Extrato de pagamentos` separa lanches, bebidas, sobremesas e recargas por categoria. `Minhas reservas` apresenta uma agenda semanal com troca de dia. `Falar com a cantina` possui assunto, mensagem, loading e confirmação simulada.
- Notificações agora são: Lanches do dia, Débito pendente e Promoções. O banner inicial também passou a divulgar lanches e destaques do dia.
- Verificado visualmente em 375px e desktop: home, dashboard, perfil, dados, extrato, reservas com troca de dia e suporte.
- `npm run lint`, `npx tsc --noEmit`, `npm run build` e `git diff --check`: aprovados.
- Produção Vercel READY: `https://cantina-app-seven.vercel.app`
- Deployment desta entrega: `https://cantina-ak1iszm5n-cocozaograndes-projects.vercel.app`
- Inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/DVbZSVcf5NH1qQUD3hPLpsZgARjK`

## Generated: 2026-09-12T11:15:00-03:00
## Pipeline: S0 → S6 complete

---

## Build Status
- TypeScript errors: **0**
- `npm run build`: **PASS**
- Routes generated: **33**
- Tested viewport: mobile 375px

---

## Routes Created

| Route | File | Status |
|-------|------|--------|
| `/admin/menu` | `app/admin/menu/page.tsx` | ✅ MODIFIED |
| `/admin/menu/novo` | `app/admin/menu/novo/page.tsx` | ✅ NEW |
| `/admin/menu/[id]/editar` | `app/admin/menu/[id]/editar/page.tsx` | ✅ NEW |
| `/student/perfil/meus-dados` | `app/student/perfil/meus-dados/page.tsx` | ✅ NEW |
| `/student/perfil/alterar-pin` | `app/student/perfil/alterar-pin/page.tsx` | ✅ NEW |
| `/student/perfil/alunos-vinculados` | `app/student/perfil/alunos-vinculados/page.tsx` | ✅ NEW |
| `/student/perfil/historico-financeiro` | `app/student/perfil/historico-financeiro/page.tsx` | ✅ NEW |
| `/student/perfil/chave-pix` | `app/student/perfil/chave-pix/page.tsx` | ✅ NEW |
| `/student/perfil/extrato-completo` | `app/student/perfil/extrato-completo/page.tsx` | ✅ NEW |
| `/student/perfil/minhas-reservas` | `app/student/perfil/minhas-reservas/page.tsx` | ✅ NEW |
| `/student/perfil/preferencias-cardapio` | `app/student/perfil/preferencias-cardapio/page.tsx` | ✅ NEW |
| `/student/perfil/falar-cantina` | `app/student/perfil/falar-cantina/page.tsx` | ✅ NEW |
| `/student/perfil/termos-de-uso` | `app/student/perfil/termos-de-uso/page.tsx` | ✅ NEW |
| `/student/perfil/politica-de-privacidade` | `app/student/perfil/politica-de-privacidade/page.tsx` | ✅ NEW |

---

## Components Created

| Component | Path | Used By |
|-----------|------|---------|
| `ProfilePageShell` | `components/profile/ProfilePageShell.tsx` | All 11 perfil sub-pages |
| `AvatarUpload` | `components/profile/AvatarUpload.tsx` | `app/student/profile/page.tsx` |
| `ProductImageUpload` | `components/admin/ProductImageUpload.tsx` | `ProductForm` |
| `PriceInput` | `components/admin/PriceInput.tsx` | `ProductForm` |
| `ProductForm` | `components/admin/ProductForm.tsx` | `/admin/menu/novo`, `/admin/menu/[id]/editar` |

---

## Files Modified (Surgical Diffs Only)

| File | Changes |
|------|---------|
| `app/student/profile/page.tsx` | Added `AvatarUpload` import; replaced `ProfileAvatar` JSX; wired all 11 rows to `/student/perfil/*` routes |
| `app/admin/menu/page.tsx` | Full rewrite — new `Product` type, product grid, search, category filter, toggle, delete dialog, sessionStorage read on mount |

---

## Key Architecture Decisions

- **Admin product state**: `useState(MOCK_PRODUCTS)` in `app/admin/menu/page.tsx`. Cross-page communication via `sessionStorage` keys: `cantina_new_product`, `cantina_updated_product`, `cantina_edit_product`.
- **Profile photo**: `localStorage` key `cantina_profile_photo` (base64). `ProfileAvatar` reads it automatically; `AvatarUpload` adds the camera-badge click-to-upload layer on top.
- **Route prefix**: Sub-pages are at `/student/perfil/*` (not `/perfil/*`) to stay inside the student layout's auth guard and bottom navigation.
- **`glass-card` pattern**: All new components use the `.glass-card` CSS utility class from `globals.css`, NOT inline Tailwind glassmorphism chains.
- **No new npm packages**: All features built with existing stack (Lucide React, Framer Motion, base-ui, clsx, tailwind-merge).

---

## Known Limitations (Demo Mode)

- Product data resets on page refresh — no persistent DB, `useState(MOCK_PRODUCTS)` only
- sessionStorage clears on tab close — edit/create flow requires the tab to stay open
- Profile photo: persists via localStorage base64 (~5MB browser limit; large photos may fail silently on some browsers)
- Alterar PIN: validates format only — no backend check against real PIN
- Falar com a Cantina: simulated 800ms send — no email or webhook fired
- Alunos Vinculados: "Adicionar aluno" button is permanently disabled (feature not implemented)
- Preferências do Cardápio: persisted locally — does not affect actual menu filtering in `/student/menu`

---

## Files NOT Modified (Protected)

- `app/student/home/page.tsx`
- `app/student/menu/page.tsx`
- `app/student/orders/page.tsx`
- `app/student/payment/**`
- `app/student/reservations/page.tsx`
- `app/student/layout.tsx` (bottom nav intact)
- `app/admin/dashboard/page.tsx`
- `app/admin/orders/page.tsx`
- `app/admin/reports/page.tsx`
- `app/admin/students/**`
- `lib/mock-data.ts`
- `types/index.ts`
- All saldo/balance logic

---

## S6 QA Results

| Check | Result |
|-------|--------|
| `window.confirm` / `window.alert` in new files | ✅ None |
| `style={{}}` inline styles in new files | ✅ None (1 pre-existing hit in `KpiCard.tsx` — untouched) |
| `: any` / `as any` types in new files | ✅ None |
| Camera icon uses lucide-react `Camera` (not emoji) | ✅ Confirmed |
| No emoji in any JSX | ✅ Confirmed |
| All 14 route files exist on disk | ✅ Confirmed |
| `npm run build` | ✅ PASS — 0 errors |

---

## Placeholder Tasks (Reserved for Future Sessions)

- [ ] Connect `/admin/menu` CRUD to Supabase product table
- [ ] Implement real PIN change API endpoint
- [ ] Wire `/student/perfil/falar-cantina` to email or webhook (e.g., Resend, SendGrid)
- [ ] Replace base64 avatar with Supabase Storage URL (lift the 5MB localStorage limit)
- [ ] Enforce product daily limits in the student order flow
- [ ] Make menu category preferences actually filter `/student/menu` display
- [ ] Implement "Adicionar aluno vinculado" flow with account linking
- [ ] Add real PIX key validation (CPF/CNPJ/email/phone format check)

---

## Next Session Seed

**Recommended**: Connect admin product CRUD to Supabase.

```bash
# Prerequisite: Supabase MCP configured in Antigravity
# Table needed: products (id, name, description, category, price_in_cents, daily_limit, is_active, image_url)
```

## Atualização — 2026-09-12

- Canvas desktop ocupa 100% da largura, sem bordas laterais ao reduzir o zoom; overflow horizontal bloqueado.
- `/admin/menu` exibe imagens locais em todos os produtos e oferece ação visível **Editar imagem**.
- O editor preserva a imagem existente e exige imagem ao cadastrar produto novo.
- `npm run lint`, `npx tsc --noEmit` e `npm run build`: aprovados.
- Deploy READY: `https://cantina-app-seven.vercel.app` (inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/5J3GfDbLezVvTrTYRLDRYn7zyBQX`).

## Atualização — 2026-09-12 (menu mobile)

- Menu lateral mobile do Admin recebeu painel escuro translúcido com `backdrop-blur`, brilho âmbar sutil, borda laranja e sombra profunda, mantendo contraste e identidade Cantina Saudável.
- Lint, TypeScript e build Vercel aprovados.
- Deploy READY: `https://cantina-app-seven.vercel.app` · inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/HdzPWxsXW1LGZ9hbjZkcVowhjGru`.

## Atualização — 2026-09-13 (imagens, recorte e menu)

- Fotos do cardápio Admin agora usam `object-contain`, com moldura escura e espaço interno para não cortar o produto.
- Upload de produto mantém prévia completa; novos produtos continuam com imagem obrigatória.
- Foto de perfil ganhou editor de recorte com zoom e posicionamento horizontal/vertical, salvando a composição final no modo demo.
- Aviso/banner e sinos de notificações foram removidos temporariamente para preparar a futura versão app.
- Menu Admin mobile ocupa toda a lateral direita com vidro escuro, blur, brilho âmbar e sombra.
- Lint e TypeScript aprovados; Vercel READY: `https://cantina-app-seven.vercel.app` · inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/J2CpfjFgdzt3YtUVAG31VbUnkEEW`.

## Scroll Reveal — 2026-09-13

- `GsapReveal` evoluído para animações acionadas pela entrada no viewport via IntersectionObserver.
- Variantes alternadas `left`, `right`, `up`, `scale` e `soft` evitam movimento uniforme e preservam a hierarquia visual.
- Home pública recebeu reveals distintos no cabeçalho, hero, cartão de experiência e rodapé.
- Shells Admin e Aluno aplicam reveal alternado às páginas estáticas sem alterar layout; `prefers-reduced-motion` é respeitado.
- Deploy READY: `https://cantina-app-seven.vercel.app` · inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/5Z3uuGFJHENFSKvLppgSQ4vkZzns`.

## Menu fullscreen e toasts — 2026-09-13

- Menu mobile Admin abre em tela inteira pela direita, com blur, animação e um único X de fechamento.
- Cards Admin seguem o padrão amplo do cardápio do aluno, com fotos grandes e `object-cover`.
- Toasts receberam fundo em gradiente, borda âmbar, contraste branco e sombra.
- Deploy READY: `https://cantina-app-seven.vercel.app` · inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/GDcvw7odyi35VUQGtPq5mmyyumWW`.

## Correção de saída e blur do menu — 2026-09-13

- Overlay do Sheet/Modal não desfoca mais o conteúdo inteiro; agora apenas escurece o fundo, mantendo o blur restrito ao painel.
- Menu Admin mantém abertura fullscreen pela direita e um único X.
- Botões de saída Admin/Aluno ganharam card contrastante, ícone, descrição e ação claramente visível.
- Dialog de confirmação recebeu superfície escura, borda âmbar e sombra consistente.
- Deploy READY: `https://cantina-app-seven.vercel.app` · inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/4Gs2QsMvT3m3vk6CkMHga3wN3viB`.

## Correção final do menu e logout — 2026-09-13

- Removido definitivamente qualquer blur do overlay global; o conteúdo atrás das três barras permanece nítido.
- Menu lateral mantém blur apenas no próprio painel e fundo laranja/preto consistente.
- Botão Cancelar do logout agora tem fundo visível, borda clara e contraste alto.
- Sair da conta usa gradiente laranja/preto e ação visual destacada.
- Deploy READY: `https://cantina-app-seven.vercel.app` · inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/K95DL7AzoWEwg71qk6tsxmd39uPX`.

## Menu Admin — correção definitiva — 2026-09-13

- Substituído o Sheet compartilhado por painel controlado diretamente no layout Admin; elimina estado preso que mostrava apenas blur.
- Três barras agora abrem sempre um painel fullscreen nítido; overlay separado fecha ao tocar fora e X fecha de forma determinística.
- Animação de entrada pela direita e acabamento laranja/preto preservados.
- Deploy READY: `https://cantina-app-seven.vercel.app` · inspect: `https://vercel.com/cocozaograndes-projects/cantina-app/8MuvMYYy8vBtmEisiedy3BPXZcd4`.
