# CLAUDE.md — Grupo Punta Cana Project

> This document is the single source of truth for this project.
> It is read by Claude at the start of every session and updated automatically as work progresses.
> Last updated: 2026-03-19

---

## 1. Client Profile

| Field | Details |
|---|---|
| **Client** | Grupo Punta Cana |
| **Website (reference)** | https://grupopuntacana.com.do/es/ |
| **Industry** | Luxury Caribbean hospitality & real estate |
| **Founded** | 1960s (50+ year legacy) |
| **Scale** | 44,000+ hotel rooms, 15,000+ employees |
| **Tagline** | "Imagining More" |
| **Core Mission** | Make visitor dreams reality while respecting nature |
| **Values** | Sustainability, community, family legacy, environmental stewardship |
| **Developer** | Nicolás García |

---

## 2. Target Audience

- Corporate stakeholders and investors
- Potential resort guests (luxury travelers)
- Job seekers (careers section)
- Press and media
- Community partners and NGOs
- Language: Spanish primary, English secondary (bilingual site)

---

## 3. Brand Style Guide

### Colors
```
Primary:    #1a2744  (dark navy — headers, logo areas)
Secondary:  #0891b2  (Caribbean blue — accents, links)
Accent:     #10b981  (tropical green — highlights, CTAs)
Background: #ffffff  (main) / #f8fafc (subtle sections)
Text dark:  #1e293b
Text muted: #64748b
```

### Typography
- **Display / Headings**: Playfair Display (Google Fonts) — heritage, luxury feel
- **Body**: Inter (Google Fonts) — clean, modern, readable

### Design Principles
- Luxury Caribbean hospitality tone — sophisticated yet approachable
- Narrative-driven: history and legacy are central to every page
- Bold imagery with generous whitespace
- Bilingual: all content in `es.json` and `en.json`
- No generic AI aesthetics — distinctive, intentional design choices
- Mobile-first responsive layout
- Accessibility: WCAG AA minimum (contrast ≥ 4.5:1, touch targets ≥ 44px)

### Icons
- Library: `react-icons` (primary)
- Secondary: `lucide-react` for UI icons

### Components
- UI Library: `shadcn/ui`

---

## 4. Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 16 (App Router) |
| Language | TypeScript |
| Styling | TailwindCSS v4 |
| Components | shadcn/ui |
| Icons | react-icons + lucide-react |
| i18n | next-intl (ES + EN) |
| Auth | NextAuth.js v5 |
| Database | Supabase (PostgreSQL) |
| ORM | Supabase client (direct) |
| Deployment | Vercel (planned) |

### Commands Reference
```bash
# Dev server
npm run dev

# Build
npm run build

# Lint
npm run lint

# Add shadcn component
npx shadcn@latest add <component>

# Generate design system from ui-ux-pro-max skill
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "luxury caribbean hospitality" --design-system
```

---

## 5. Project Structure

```
src/
├── app/
│   ├── [locale]/
│   │   ├── layout.tsx                # Root layout with i18n + fonts
│   │   ├── page.tsx                  # Landing page (NEW — doesn't exist on original site)
│   │   ├── historia/page.tsx
│   │   ├── sobre-nosotros/page.tsx
│   │   ├── responsabilidad-social/page.tsx
│   │   ├── noticias/page.tsx
│   │   ├── carreras/page.tsx
│   │   └── contacto/page.tsx
│   ├── admin/                        # PROTECTED — middleware enforced
│   │   └── dashboard/page.tsx
│   └── api/
│       ├── auth/[...nextauth]/route.ts
│       └── contact/route.ts
├── components/
│   ├── layout/        # Navbar, Footer
│   ├── sections/      # Page-specific section components
│   └── ui/            # shadcn/ui components
├── lib/
│   ├── supabase.ts    # Supabase client (server-only where sensitive)
│   ├── auth.ts        # NextAuth config
│   └── utils.ts       # Shared utilities
├── messages/
│   ├── es.json        # Spanish translations
│   └── en.json        # English translations
└── middleware.ts      # Auth guard + locale routing
```

---

## 6. Security Checklist

- [ ] `src/middleware.ts` blocks unauthenticated access to `/admin/*`
- [ ] No `/admin` page accessible via direct URL without session
- [ ] All sensitive env vars are server-only (no `NEXT_PUBLIC_` prefix)
- [ ] `.env.local` is in `.gitignore` — never committed
- [ ] Contact form has server-side validation and sanitization
- [ ] API routes have input validation
- [ ] Rate limiting on contact form API route
- [ ] Supabase RLS (Row Level Security) enabled on all tables
- [ ] CSP headers configured in `next.config.ts`
- [ ] No secrets hardcoded anywhere in codebase
- [ ] `SUPABASE_SERVICE_ROLE_KEY` only used in server-side code

### Required Environment Variables (`.env.local`)
```
NEXTAUTH_SECRET=
NEXTAUTH_URL=
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
```

---

## 7. Pages & Progress Tracker

> Claude updates this table when a section is completed.
> You can also mirror this in your Trello board.

| # | Page / Section | Status | Notes |
|---|---|---|---|
| 1 | Project init + config + CLAUDE.md | ✅ Done | Next.js 16 + all deps installed |
| 2 | Layout: Navbar + Footer (bilingual) | ⬜ Todo | |
| 3 | Landing page (hero + summary sections) | ⬜ Todo | New — doesn't exist on original |
| 4 | Historia page (timeline component) | ⬜ Todo | |
| 5 | Sobre Nosotros (mission/vision/values) | ⬜ Todo | |
| 6 | Responsabilidad Social | ⬜ Todo | |
| 7 | Noticias (blog/news listing + detail) | ⬜ Todo | |
| 8 | Carreras (job listings) | ⬜ Todo | |
| 9 | Contacto (form + map) | ⬜ Todo | |
| 10 | Admin dashboard (protected) | ⬜ Todo | |
| 11 | Auth (NextAuth + Supabase) | ⬜ Todo | |
| 12 | Final security audit + SEO | ⬜ Todo | |

---

## 8. Git Push Log

| # | Date | Branch | Description |
|---|---|---|---|
| 1 | 2026-03-19 | main | Project init: Next.js 16 + TypeScript + TailwindCSS v4 + shadcn/ui + next-intl + next-auth + supabase + react-icons. CLAUDE.md created. |

---

## 9. Lessons & Notes

> Claude adds entries here when something non-obvious is learned during the project.

- npm/create-next-app rejects directory names with capital letters. Workaround: scaffold in /tmp with lowercase name, then rsync into the project directory.
