---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8]
status: 'complete'
completedAt: '2026-01-28'
inputDocuments:
  - '_bmad-output/planning-artifacts/product-brief-portfolio-2026-01-23.md'
  - '_bmad-output/planning-artifacts/prd.md'
  - '_bmad-output/planning-artifacts/ux-design-specification.md'
  - '_bmad-output/planning-artifacts/research/domain-developer-portfolios-research-2026-01-23.md'
  - '_bmad-output/project-context.md'
workflowType: 'architecture'
project_name: 'bmad'
user_name: 'Sasa'
date: '2026-01-24'
---

# Architecture Decision Document

_This document builds collaboratively through step-by-step discovery. Sections are appended as we work through each architectural decision together._

---

## Project Context Analysis

### Requirements Overview

**Functional Requirements:**

The portfolio application is organized into **8 primary functional domains**:

1. **Persona & Content Personalization** - Landing page persona selector enabling three distinct content hierarchies (Recruiter/Client/Developer) with instant layout transformation, preference persistence, and context-aware navigation
2. **Project Showcase & Interactive Demonstrations** - 3-5 polished projects with live demos, embedded CodeSandbox/StackBlitz playgrounds, video walkthroughs, performance metrics visualization, and interactive architecture diagrams
3. **Real-Time Skill Verification** - GitHub API integration for commit activity and contribution graphs, LeetCode/HackerRank API for problem-solving stats, auto-updating "Last Active" indicators with polling every 5 minutes
4. **Content Management (Admin)** - Authenticated admin panel with CRUD operations for projects, image upload with automatic optimization, multi-persona preview, and instant publishing workflow
5. **Visitor Engagement & Conversion** - Context-aware contact forms with different fields per persona, ROI calculators for client view, consultation booking system, collaboration opportunity indicators
6. **Analytics & Measurement** - Vercel Analytics + Plausible integration, persona selection tracking, interaction heatmaps, engagement metrics, conversion funnel analysis
7. **SEO & Discoverability** - Server-side rendering for search engines, structured data (JSON-LD), XML sitemap generation, Open Graph tags, semantic HTML5
8. **System & Performance** - Core Web Vitals optimization, image optimization (AVIF/WebP), lazy loading, code splitting, CDN distribution via Vercel Edge Network

**Non-Functional Requirements:**

Critical NFRs that will drive architectural decisions:

- **Performance (NON-NEGOTIABLE)**: LCP <2.5s, INP <200ms, CLS <0.1, Lighthouse score 90+ across all categories
- **SEO**: Server-side rendering required for organic discoverability, metadata API for all pages, structured data schemas
- **Accessibility**: WCAG 2.1 AA compliance minimum - keyboard navigation, screen reader support, 4.5:1 color contrast
- **Security**: API keys server-side only (GitHub, LeetCode tokens), input validation, sanitization of user-generated content
- **Browser Compatibility**: Latest 2 versions of Chrome, Firefox, Safari, Edge with progressive enhancement
- **Mobile Responsiveness**: Mobile-first design with 50%+ expected mobile traffic, touch-optimized interactions (44x44px minimum touch targets)
- **Reliability**: 99.9% uptime via Vercel hosting, graceful degradation when external APIs fail, error boundaries for client-side errors
- **Scalability**: Architecture designed for continuous enhancement, admin panel enables content updates without code changes

**Scale & Complexity:**

- **Primary domain**: Full-Stack Web Application (Next.js 14+ App Router with React Server Components)
- **Complexity level**: **Medium-High** - Innovative tri-persona system, multiple real-time API integrations, strict performance constraints, rich interactive features
- **Estimated architectural components**: 
  - 15-20 page components (landing, projects, about, admin dashboard, etc.)
  - 30-40 reusable UI components (PersonaSelector, ProjectCard, CodePlayground, SkillMatrix, etc.)
  - 5-8 API routes (GitHub proxy, LeetCode proxy, contact form, admin CRUD)
  - 3-5 custom React hooks (usePersonaContext, useGitHubStats, useRealTimePolling)
  - Database schema with 3-5 tables (projects, users, analytics, testimonials)

### Technical Constraints & Dependencies

**Mandated Technology Stack** (from project-context.md):
- Next.js 14+ with App Router (NOT Pages Router)
- TypeScript strict mode (no `any` types)
- Tailwind CSS + shadcn/ui component library
- PostgreSQL + Prisma ORM for admin panel
- Vercel hosting with automatic HTTPS/SSL

**External API Dependencies:**
- GitHub API (60 req/hour unauthenticated, 5,000/hour authenticated) - requires rate limiting and caching
- LeetCode/HackerRank API - less frequently updated, 1-hour cache acceptable
- Both APIs require graceful degradation when unavailable

**Performance Constraints:**
- Core Web Vitals targets are **non-negotiable** - architecture must prioritize performance
- Mobile-first approach required (50%+ traffic from mobile devices)
- No `'use client'` directive unless absolutely necessary (increases bundle size)
- All images must use Next.js `<Image>` component (never `<img>` tag)
- Heavy libraries (Three.js, CodeSandbox) must use `next/dynamic` with `ssr: false`

**Security Constraints:**
- API keys NEVER exposed client-side - all external API calls proxied through Next.js API routes
- User input validation and sanitization required
- NextAuth.js for admin authentication

### Cross-Cutting Concerns Identified

**1. Performance Optimization** (affects all components)
- Server vs Client Component decisions critical for bundle size
- Lazy loading strategy for heavy interactive features
- Image optimization and responsive images with srcset
- Code splitting and tree shaking
- Caching strategy for API responses (24h GitHub, 1h real-time data)

**2. Persona-Based Content Delivery** (affects all pages)
- State management for persona selection (React Context or URL params)
- Conditional rendering based on persona
- Smooth CSS transitions (<300ms) for layout transformations
- Content prioritization logic per persona
- Context-aware form fields

**3. Error Handling & Resilience** (affects all API integrations)
- Graceful degradation when GitHub/LeetCode APIs fail
- Error boundaries for client-side errors
- Loading states that don't cause layout shift (skeleton screens)
- Rate limiting handling with exponential backoff
- Fallback to cached data with timestamps

**4. Accessibility** (affects all UI components)
- Keyboard navigation for all interactive elements
- ARIA labels and semantic HTML5
- Color contrast compliance (4.5:1 minimum)
- Screen reader compatibility
- Focus indicators visible and clear

**5. SEO & Metadata** (affects all pages)
- Metadata API for title, description, Open Graph tags
- Structured data (JSON-LD for Person, WebSite schemas)
- Semantic HTML5 (header, nav, main, article, footer)
- Single H1 per page with logical heading hierarchy
- XML sitemap auto-generation

**6. Real-Time Data Synchronization** (affects skill verification features)
- Polling intervals (5 min GitHub, 1 hour LeetCode)
- Client-side SWR (stale-while-revalidate) pattern
- Cache invalidation strategy
- Loading states and optimistic updates

---

## Starter Template Evaluation

### Primary Technology Domain

**Full-Stack Web Application** using Next.js 14+ App Router with React Server Components

### Technical Preferences from Project Context

The project-context.md file contains comprehensive technical rules that define the exact technology stack:

**Mandated Technologies:**
- **Framework**: Next.js 14+ with App Router (NOT Pages Router)
- **Language**: TypeScript strict mode (no `any` types)
- **Styling**: Tailwind CSS + shadcn/ui component library
- **Database**: PostgreSQL + Prisma ORM
- **Authentication**: NextAuth.js
- **Hosting**: Vercel with automatic HTTPS/SSL
- **Testing**: Playwright (E2E), Jest (unit tests)

### Starter Options Considered

**1. Official Next.js SaaS Starter (shadcn.io)**
- Stack: Next.js 14+, PostgreSQL, Drizzle ORM, Tailwind CSS, shadcn/ui
- Features: Authentication, Stripe integration, subscription management, RBAC
- **Rejected**: Uses Drizzle ORM instead of required Prisma

**2. Next.js 15 Starter Shadcn**
- Stack: Next.js 15, React 19, TypeScript 5, Tailwind CSS 4, shadcn/ui
- Features: App Directory, dark mode, Bundle Analyzer, Docker support
- **Rejected**: No database/ORM included, would need extensive manual setup

**3. Standard create-next-app + Manual Configuration**
- Official Next.js CLI with TypeScript + Tailwind options
- Clean slate approach - add shadcn/ui, Prisma, and other tools manually
- **Selected**: Full control, no unwanted dependencies, exact specification match

### Selected Starter: create-next-app + Manual Configuration

**Rationale for Selection:**

Given the **strict technical requirements** defined in project-context.md and the fact that no pre-built starter exactly matches the required stack (Next.js 14+ App Router + TypeScript + Tailwind + shadcn/ui + **Prisma** + Vercel), the recommended approach is:

1. Initialize with official `create-next-app` for clean Next.js 14+ App Router foundation
2. Manually add shadcn/ui, Prisma, NextAuth.js, and testing infrastructure
3. Configure according to project-context.md rules

**Advantages:**
- ✅ Exact Next.js 14+ App Router setup with no compromises
- ✅ Zero unwanted dependencies or architectural patterns
- ✅ Follows project-context.md rules precisely
- ✅ Clean foundation for tri-persona architecture
- ✅ Aligns with "boring technology for stability" principle

**Initialization Command:**

```bash
npx create-next-app@latest portfolio --typescript --tailwind --app --no-src-dir --import-alias "@/*"
```

**Command Options Explained:**
- `--typescript`: Enables TypeScript with strict mode configuration
- `--tailwind`: Configures Tailwind CSS with PostCSS
- `--app`: Uses App Router architecture (NOT Pages Router)
- `--no-src-dir`: Places `app/` directory at project root (cleaner structure)
- `--import-alias "@/*"`: Sets up path aliases for clean imports (`@/components`, `@/lib`, etc.)

**Post-Initialization Setup (Implementation Stories):**

After creating the base Next.js app, the following tools must be added:

1. **shadcn/ui Component Library**
   ```bash
   npx shadcn@latest init
   ```
   - Configures Radix UI primitives with Tailwind styling
   - Adds `components/ui/` directory for shadcn components
   - Sets up component installation workflow

2. **Prisma ORM + PostgreSQL**
   ```bash
   npm install prisma @prisma/client
   npx prisma init
   ```
   - Creates `prisma/schema.prisma` for database schema
   - Configures PostgreSQL connection
   - Sets up migration workflow

3. **NextAuth.js Authentication**
   ```bash
   npm install next-auth
   ```
   - Admin panel authentication
   - Session management
   - API route protection

4. **Testing Infrastructure**
   ```bash
   npm install -D @playwright/test jest @testing-library/react @testing-library/jest-dom
   ```
   - Playwright for E2E cross-browser testing
   - Jest for unit testing
   - React Testing Library for component testing

5. **Additional Dependencies**
   - `swr`: Client-side data fetching with stale-while-revalidate
   - `framer-motion`: Animations for persona transitions
   - `zod`: Runtime validation for API responses
   - `@vercel/analytics`: Analytics integration

### Architectural Decisions Provided by Starter

**Language & Runtime:**
- TypeScript 5+ with strict mode enabled (`noImplicitAny`, `strictNullChecks`, `strictFunctionTypes`)
- React 18+ with Server Components and Client Components support
- Node.js runtime via Next.js server

**Styling Solution:**
- Tailwind CSS 3+ configured with JIT (Just-In-Time) compiler
- PostCSS for CSS processing and optimization
- CSS Modules support built-in for scoped styles
- Custom Tailwind config for brand colors (to be configured)
- Dark mode support via Tailwind's `dark:` variant

**Build Tooling:**
- Turbopack (Next.js 14+ default dev server) for fast hot module replacement
- Automatic code splitting per route and component
- Tree shaking to eliminate unused code
- Image optimization via Next.js `<Image>` component (AVIF/WebP)
- Bundle analysis available via `@next/bundle-analyzer`

**Testing Framework:**
- **Not included by default** - requires manual setup:
  - Playwright for E2E testing (cross-browser: Chrome, Firefox, Safari, Edge)
  - Jest for unit testing with React Testing Library
  - Test organization: `tests/e2e/` and co-located `*.test.tsx` files

**Code Organization:**
- **App Router structure**:
  - `app/` - Pages, layouts, loading states, error boundaries
  - `app/api/` - API routes for GitHub/LeetCode proxying, contact form, admin CRUD
  - `components/` - Reusable React components (organized by feature)
  - `lib/` - Utility functions, helpers, API clients
  - `hooks/` - Custom React hooks (`usePersonaContext`, `useGitHubStats`)
  - `types/` - TypeScript type definitions and interfaces
  - `public/` - Static assets (images, fonts, favicon)
  - `prisma/` - Database schema and migrations

**Development Experience:**
- Hot module replacement with Turbopack (instant updates)
- TypeScript IntelliSense and compile-time type checking
- ESLint with Next.js recommended rules (`eslint-config-next`)
- Prettier for consistent code formatting (to be configured)
- Git integration ready with `.gitignore` configured

**Deployment:**
- Vercel-optimized build configuration
- Automatic HTTPS/SSL via Vercel
- Edge Network CDN for global distribution
- Zero-config deployment via Git integration
- Environment variables managed in Vercel dashboard

**Note:** Project initialization using `create-next-app` should be the **first implementation story**. Subsequent stories will add Prisma schema, shadcn/ui components, authentication, testing infrastructure, and configure the tri-persona architecture.

---

## Core Architectural Decisions

### Decision Priority Analysis

**Critical Decisions (Block Implementation):**
1. State management for persona system (React Context + localStorage)
2. API caching strategy for real-time integrations (SWR)
3. Database schema design (Prisma models)
4. Error handling and resilience patterns
5. Deployment and environment configuration

**Important Decisions (Shape Architecture):**
- All critical decisions above directly shape the implementation
- These decisions were made collaboratively based on project requirements and constraints

**Deferred Decisions (Post-MVP):**
- Advanced analytics dashboards (basic analytics included in MVP)
- Content versioning system (can add later if needed)
- Multi-language internationalization (English-only for MVP)
- Advanced 3D project galleries (basic interactive demos in MVP)

---

### Decision 1: State Management for Persona System

**Decision:** React Context + localStorage

**Rationale:**
The tri-persona system (Recruiter/Client/Developer) is a core UX personalization feature that requires client-side state management with persistence across sessions.

**Selected Approach:**
- **Technology**: React Context API + localStorage
- **Implementation**: `PersonaContext` wrapping the app, storing selection in localStorage
- **State Management**: Client-side only (acceptable for UX personalization, not SEO-critical)

**Why This Choice:**
- ✅ **Performance**: Meets <300ms transition requirement with instant client-side state updates
- ✅ **Simplicity**: Built-in React pattern, no external dependencies, aligns with "boring technology" principle
- ✅ **Persistence**: localStorage ensures users return to their preferred persona view
- ✅ **UX**: Smooth CSS transitions without URL clutter or cookie complexity
- ✅ **SEO**: Search engines see default view (acceptable - persona is user preference, not content variation)

**Implementation Pattern:**
```typescript
// contexts/PersonaContext.tsx
'use client'
import { createContext, useContext, useState, useEffect } from 'react'

type Persona = 'recruiter' | 'client' | 'developer' | null

const PersonaContext = createContext<{
  persona: Persona
  setPersona: (persona: Persona) => void
}>({ persona: null, setPersona: () => {} })

export function PersonaProvider({ children }: { children: React.ReactNode }) {
  const [persona, setPersonaState] = useState<Persona>(null)
  
  useEffect(() => {
    const saved = localStorage.getItem('persona') as Persona
    if (saved) setPersonaState(saved)
  }, [])
  
  const setPersona = (newPersona: Persona) => {
    setPersonaState(newPersona)
    if (newPersona) localStorage.setItem('persona', newPersona)
  }
  
  return (
    <PersonaContext.Provider value={{ persona, setPersona }}>
      {children}
    </PersonaContext.Provider>
  )
}

export const usePersona = () => useContext(PersonaContext)
```

**Affects:** All pages, PersonaSelector component, content prioritization logic, context-aware forms

---

### Decision 2: API Caching & Real-Time Data Strategy

**Decision:** SWR (stale-while-revalidate) with custom polling intervals

**Rationale:**
Real-time skill verification requires efficient API polling for GitHub (5-minute intervals) and LeetCode (1-hour intervals) with graceful degradation when APIs fail.

**Selected Approach:**
- **Technology**: Vercel's `swr` library (5KB bundle)
- **Polling**: `refreshInterval` configured per API (5 min GitHub, 1 hour LeetCode)
- **Caching**: Stale-while-revalidate pattern with automatic revalidation
- **Error Handling**: Shows stale data with timestamp when API unavailable

**Why This Choice:**
- ✅ **Next.js Optimized**: Built by Vercel specifically for Next.js applications
- ✅ **Performance**: Tiny 5KB bundle size (critical for LCP <2.5s target)
- ✅ **Built-in Features**: Automatic revalidation, deduplication, focus revalidation, retry logic
- ✅ **Graceful Degradation**: Shows stale data instead of error screens
- ✅ **Developer Experience**: Clean hooks-based API, minimal code

**Implementation Pattern:**
```typescript
// hooks/useGitHubStats.ts
import useSWR from 'swr'

const fetcher = (url: string) => fetch(url).then(r => r.json())

export function useGitHubStats() {
  const { data, error } = useSWR(
    '/api/github/stats',
    fetcher,
    {
      refreshInterval: 5 * 60 * 1000, // 5 minutes
      revalidateOnFocus: false,
      dedupingInterval: 60 * 1000, // 1 minute deduplication
    }
  )
  
  return {
    stats: data?.data,
    timestamp: data?.timestamp,
    isStale: data?.status === 'stale',
    isLoading: !error && !data,
    isError: error
  }
}

// API Route: app/api/github/stats/route.ts
export async function GET() {
  try {
    const stats = await fetchGitHubStats()
    return Response.json({ 
      data: stats, 
      timestamp: new Date().toISOString(),
      status: 'success' 
    }, {
      headers: {
        'Cache-Control': 'public, s-maxage=300, stale-while-revalidate=3600'
      }
    })
  } catch (error) {
    console.error('GitHub API error:', error)
    const cachedStats = await getCachedStats()
    return Response.json({ 
      data: cachedStats,
      timestamp: cachedStats?.timestamp || null,
      status: 'stale'
    }, { status: 200 })
  }
}
```

**Affects:** SkillVerification component, GitHub API integration, LeetCode API integration, real-time data display

---

### Decision 3: Database Schema Design

**Decision:** Comprehensive Prisma schema with User, Project, Testimonial, and Analytics models

**Rationale:**
Admin panel requires structured data for projects, testimonials, and analytics tracking to enable data-driven optimization from day 1.

**Selected Schema:**

```prisma
// prisma/schema.prisma

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id            String    @id @default(cuid())
  email         String    @unique
  name          String
  passwordHash  String
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
}

model Project {
  id                String    @id @default(cuid())
  title             String
  slug              String    @unique
  description       String
  longDescription   String    @db.Text
  techStack         String[]
  githubUrl         String?
  liveDemoUrl       String?
  codePlaygroundUrl String?
  thumbnailUrl      String
  videoWalkthroughUrl String?
  screenshotUrls    String[]
  performanceLCP    Float?
  performanceINP    Float?
  performanceCLS    Float?
  recruiterHighlight String?  @db.Text
  clientHighlight    String?  @db.Text
  developerHighlight String?  @db.Text
  roiMetrics        Json?
  featured          Boolean   @default(false)
  order             Int       @default(0)
  published         Boolean   @default(false)
  createdAt         DateTime  @default(now())
  updatedAt         DateTime  @updatedAt
  testimonials      Testimonial[]
  analytics         ProjectAnalytics[]
}

model Testimonial {
  id          String    @id @default(cuid())
  projectId   String
  project     Project   @relation(fields: [projectId], references: [id], onDelete: Cascade)
  clientName  String
  clientRole  String
  company     String
  quote       String    @db.Text
  rating      Int       @default(5)
  order       Int       @default(0)
  published   Boolean   @default(true)
  createdAt   DateTime  @default(now())
}

model ProjectAnalytics {
  id          String    @id @default(cuid())
  projectId   String
  project     Project   @relation(fields: [projectId], references: [id], onDelete: Cascade)
  persona     String?
  viewedDemo  Boolean   @default(false)
  viewedCode  Boolean   @default(false)
  timeSpent   Int
  timestamp   DateTime  @default(now())
  userAgent   String?
  referrer    String?
}

model PersonaSelection {
  id          String    @id @default(cuid())
  persona     String
  timestamp   DateTime  @default(now())
  userAgent   String?
  referrer    String?
}
```

**Why This Choice:**
- ✅ **Comprehensive**: Supports all PRD requirements (projects, testimonials, analytics)
- ✅ **Persona-Specific**: Fields for recruiter/client/developer highlights enable tri-persona architecture
- ✅ **Performance Metrics**: Stores Lighthouse scores for "proof over claims" principle
- ✅ **Analytics**: ProjectAnalytics and PersonaSelection enable data-driven optimization from launch
- ✅ **Flexible**: JSON fields (roiMetrics) allow evolving requirements
- ✅ **PostgreSQL Arrays**: Native array support for techStack and screenshotUrls

**Affects:** Admin panel CRUD operations, project showcase pages, testimonial display, analytics dashboard

---

### Decision 4: Error Handling & Resilience Patterns

**Decision:** Graceful degradation with stale data fallback and comprehensive error boundaries

**Rationale:**
Project-context.md mandates graceful degradation when external APIs fail. Users should never see broken experiences.

**Error Handling Strategy:**

**1. API Route Error Handling:**
- Try-catch blocks around external API calls
- Return cached data with "stale" status on failure
- Server-side logging for debugging
- User-friendly error messages

**2. Client-Side Error Boundaries:**
- `app/error.tsx` for Server Component errors
- Custom ErrorBoundary for Client Components
- Reset functionality to retry failed operations

**3. Loading States (No Layout Shift):**
- Skeleton screens reserve space during loading
- Prevents Cumulative Layout Shift (CLS <0.1 requirement)
- Smooth transitions between loading/loaded states

**4. Form Validation:**
- Zod runtime validation for type safety
- Specific, actionable error messages
- Client-side validation before submission

**Implementation Patterns:**
```typescript
// API Error Handling
export async function GET() {
  try {
    const data = await fetchExternalAPI()
    return Response.json({ data, status: 'success', timestamp: new Date() })
  } catch (error) {
    console.error('API error:', error)
    const cached = await getCached()
    return Response.json({ 
      data: cached, 
      status: 'stale', 
      timestamp: cached?.timestamp 
    }, { status: 200 })
  }
}

// Error Boundary
// app/error.tsx
'use client'
export default function Error({ error, reset }: { error: Error, reset: () => void }) {
  return (
    <div className="error-container">
      <h2>Something went wrong</h2>
      <button onClick={reset}>Try again</button>
    </div>
  )
}

// Loading State
// app/loading.tsx
export default function Loading() {
  return <SkeletonScreen /> // Prevents layout shift
}

// Component with Error Handling
const { stats, isLoading, isError, isStale, timestamp } = useGitHubStats()

if (isLoading) return <SkeletonStats />
if (isError) return <ErrorMessage />
if (isStale) return (
  <div>
    <Stats data={stats} />
    <StaleIndicator>Last updated: {formatTimestamp(timestamp)}</StaleIndicator>
  </div>
)
```

**Why This Choice:**
- ✅ **User Experience**: No broken screens, always show something useful
- ✅ **Performance**: Skeleton screens prevent CLS violations
- ✅ **Transparency**: Stale data indicators build trust
- ✅ **Resilience**: Automatic retries via SWR exponential backoff
- ✅ **Debugging**: Server-side logging without exposing errors to users

**Affects:** All API integrations, all page components, form submissions, loading states

---

### Decision 5: Deployment & Environment Configuration

**Decision:** Vercel hosting with Git-based deployments and environment variable management

**Rationale:**
Vercel provides zero-config Next.js deployment with automatic HTTPS, CDN, and seamless Prisma integration.

**Environment Variables:**

```bash
# Database
DATABASE_URL="postgresql://user:password@host:5432/database"

# Authentication (NextAuth.js)
NEXTAUTH_SECRET="..." # Generate: openssl rand -base64 32
NEXTAUTH_URL="https://your-domain.com"

# GitHub API (5,000 req/hour with token)
GITHUB_TOKEN="ghp_..."
GITHUB_USERNAME="your-username"

# LeetCode API
LEETCODE_USERNAME="your-username"

# Analytics
NEXT_PUBLIC_VERCEL_ANALYTICS_ID="..." # Auto-set by Vercel
PLAUSIBLE_DOMAIN="your-domain.com"

# Email (Contact Form)
SMTP_HOST="smtp.gmail.com"
SMTP_PORT="587"
SMTP_USER="your-email@gmail.com"
SMTP_PASSWORD="app-specific-password"
```

**Deployment Workflow:**
- **Main Branch**: Automatic production deployment
- **Pull Requests**: Automatic preview deployments
- **Rollback**: Instant rollback to previous deployment if issues detected
- **Zero Downtime**: Seamless deployments with no service interruption

**Build Configuration:**
```json
{
  "buildCommand": "prisma generate && next build",
  "installCommand": "npm install",
  "framework": "nextjs",
  "regions": ["iad1"]
}
```

**Why This Choice:**
- ✅ **Zero Config**: Vercel automatically optimizes Next.js builds
- ✅ **Performance**: Edge Network CDN for global distribution
- ✅ **Developer Experience**: Git push triggers deployment
- ✅ **Reliability**: 99.9% uptime SLA, automatic HTTPS
- ✅ **Prisma Integration**: Seamless database migrations via Vercel CLI

**Affects:** All deployment processes, environment configuration, CI/CD pipeline

---

### Decision Impact Analysis

**Implementation Sequence:**

1. **Project Initialization** (create-next-app + TypeScript + Tailwind)
2. **Database Setup** (Prisma schema + PostgreSQL connection)
3. **Authentication** (NextAuth.js + User model)
4. **Persona System** (PersonaContext + localStorage)
5. **API Integration** (SWR + GitHub/LeetCode proxies)
6. **Error Handling** (Error boundaries + graceful degradation)
7. **Deployment** (Vercel + environment variables)

**Cross-Component Dependencies:**

- **Persona System** affects all pages and components (content prioritization)
- **SWR** depends on API routes being implemented first
- **Database Schema** must be deployed before admin panel can function
- **Error Boundaries** wrap all interactive features
- **Environment Variables** required for API integrations and authentication

**Technology Stack Summary:**

| Category | Technology | Version | Rationale |
|----------|-----------|---------|-----------|
| Framework | Next.js | 14+ | App Router, React Server Components, performance |
| Language | TypeScript | 5+ | Type safety, strict mode |
| Styling | Tailwind CSS | 3+ | Utility-first, rapid development |
| UI Components | shadcn/ui | Latest | Accessible, customizable, Radix UI primitives |
| Database | PostgreSQL | Latest | Relational data, Prisma compatibility |
| ORM | Prisma | Latest | Type-safe queries, migrations |
| Auth | NextAuth.js | Latest | Session management, API protection |
| Data Fetching | SWR | Latest | Stale-while-revalidate, polling |
| Validation | Zod | Latest | Runtime type validation |
| Testing | Playwright + Jest | Latest | E2E + unit testing |
| Hosting | Vercel | N/A | Zero-config Next.js deployment |
| Analytics | Vercel Analytics + Plausible | Latest | Privacy-friendly tracking |

---

## Implementation Patterns & Consistency Rules

### Overview

This section defines architecture-level patterns that ensure AI agents write compatible, consistent code. **Detailed implementation rules are documented in [`project-context.md`](file:///d:/Repositories/portfolio/bmad/_bmad-output/project-context.md)** (311 lines, 7 rule sections).

**Critical Conflict Points Addressed:** 12 areas where AI agents could make different choices without explicit patterns.

---

### Reference to Existing Rules

**Comprehensive implementation rules already defined in `project-context.md`:**

1. **Technology Stack & Versions** - Next.js 14+, TypeScript strict mode, Tailwind CSS, shadcn/ui
2. **Language-Specific Rules** - TypeScript configuration, import patterns, Server vs Client Components
3. **Framework-Specific Rules** - App Router architecture, data fetching, performance optimization
4. **Testing Rules** - Playwright E2E, Jest unit tests, accessibility testing
5. **Code Quality & Style** - ESLint, Prettier, file structure conventions
6. **Workflow Rules** - Git branching, commit messages, PR process
7. **Critical Rules** - Performance targets, security constraints, accessibility requirements

**AI agents MUST read and follow all rules in `project-context.md` before implementing any code.**

---

### Architecture-Level Consistency Patterns

The following patterns complement `project-context.md` with architecture-level decisions that prevent agent conflicts:

---

### 1. API Response Format Patterns

**Standard API Response Wrapper:**

All API routes MUST use this consistent response format:

```typescript
// Success Response
{
  data: T,              // Actual response data (typed)
  status: 'success',    // 'success' | 'stale' | 'error'
  timestamp: string,    // ISO 8601 format
  metadata?: {          // Optional metadata
    cached: boolean,
    source: string
  }
}

// Error Response
{
  data: null,
  status: 'error',
  timestamp: string,
  error: {
    code: string,       // 'API_ERROR' | 'VALIDATION_ERROR' | 'AUTH_ERROR'
    message: string,    // User-friendly message
    details?: unknown   // Optional technical details (dev only)
  }
}

// Stale Data Response (Graceful Degradation)
{
  data: T,              // Cached data
  status: 'stale',
  timestamp: string,    // When data was originally fetched
  error: {
    code: 'API_UNAVAILABLE',
    message: 'Using cached data'
  }
}
```

**Example Implementation:**

```typescript
// app/api/github/stats/route.ts
export async function GET() {
  try {
    const stats = await fetchGitHubStats()
    return Response.json({
      data: stats,
      status: 'success',
      timestamp: new Date().toISOString()
    })
  } catch (error) {
    const cached = await getCachedStats()
    return Response.json({
      data: cached,
      status: 'stale',
      timestamp: cached?.timestamp || new Date().toISOString(),
      error: {
        code: 'API_UNAVAILABLE',
        message: 'GitHub API temporarily unavailable'
      }
    }, { status: 200 }) // Still 200 to avoid SWR error state
  }
}
```

**Rationale:** Consistent response format enables predictable error handling across all API integrations.

---

### 2. Database Naming Conventions

**Prisma Schema Naming Rules:**

```prisma
// Table Names: PascalCase singular
model User { }
model Project { }
model ProjectAnalytics { }

// Column Names: camelCase
model Project {
  id                String
  createdAt         DateTime
  longDescription   String
  performanceLCP    Float?
}

// Relation Fields: camelCase, descriptive
model Testimonial {
  projectId   String
  project     Project   @relation(fields: [projectId], references: [id])
}

// Enum Values: SCREAMING_SNAKE_CASE
enum PersonaType {
  RECRUITER
  CLIENT
  DEVELOPER
}

// Index Naming: idx_tablename_columnname
@@index([slug], name: "idx_project_slug")
@@index([published, order], name: "idx_project_published_order")
```

**TypeScript Interface Naming (matching Prisma):**

```typescript
// Generated Prisma types (use as-is)
import { Project, User, Testimonial } from '@prisma/client'

// Custom types: PascalCase with descriptive suffix
type ProjectWithTestimonials = Project & {
  testimonials: Testimonial[]
}

interface CreateProjectInput {
  title: string
  slug: string
  techStack: string[]
}
```

**Rationale:** Consistent naming prevents schema conflicts when multiple agents modify database models.

---

### 3. Component & File Naming Patterns

**Component Files:**

```
components/
├── PersonaSelector.tsx          # PascalCase for component files
├── ProjectCard.tsx
├── SkillVerification.tsx
└── ui/                          # shadcn/ui components
    ├── button.tsx               # lowercase for shadcn (convention)
    ├── card.tsx
    └── skeleton.tsx
```

**Non-Component Files:**

```
lib/
├── github-api.ts                # kebab-case for utilities
├── cache-manager.ts
└── validation-schemas.ts

hooks/
├── usePersona.ts                # camelCase with 'use' prefix
├── useGitHubStats.ts
└── useRealTimePolling.ts

types/
├── api.ts                       # lowercase for type definition files
├── persona.ts
└── project.ts
```

**Rationale:** Clear naming conventions prevent file conflicts and improve discoverability.

---

### 4. Event & State Patterns

**Persona Context Event Naming:**

```typescript
// Event names: domain.action format
'persona.selected'
'persona.changed'
'project.viewed'
'demo.launched'
'code.viewed'

// Event payload structure
interface PersonaEvent {
  type: 'persona.selected' | 'persona.changed'
  payload: {
    persona: 'recruiter' | 'client' | 'developer'
    timestamp: string
    previousPersona?: string
  }
}
```

**State Update Patterns:**

```typescript
// Immutable state updates (React Context)
const setPersona = (newPersona: Persona) => {
  setPersonaState(prev => ({
    ...prev,
    current: newPersona,
    history: [...prev.history, newPersona]
  }))
}

// NOT: Direct mutation
// setPersonaState.current = newPersona // ❌ NEVER
```

**Rationale:** Consistent event naming and immutable updates prevent state synchronization bugs.

---

### 5. Error Handling Patterns

**Client Component Error Handling:**

```typescript
// Pattern: Loading → Error → Stale → Success
const { data, error, isLoading } = useGitHubStats()

if (isLoading) {
  return <SkeletonStats /> // Prevents CLS
}

if (error && !data) {
  return <ErrorMessage retry={() => mutate()} />
}

if (data?.status === 'stale') {
  return (
    <>
      <Stats data={data.data} />
      <StaleIndicator timestamp={data.timestamp} />
    </>
  )
}

return <Stats data={data.data} />
```

**API Route Error Handling:**

```typescript
// Pattern: Try → Catch → Cache Fallback → Log
export async function GET() {
  try {
    const result = await externalAPI()
    return successResponse(result)
  } catch (error) {
    console.error('[API Error]', error) // Server-side logging
    const cached = await getCache()
    return staleResponse(cached)
  }
}
```

**Rationale:** Consistent error handling ensures graceful degradation across all features.

---

### 6. Loading State Patterns

**Skeleton Screen Pattern (Prevents CLS):**

```typescript
// app/loading.tsx - Route-level loading
export default function Loading() {
  return <PageSkeleton />
}

// Component-level loading
function ProjectCard({ projectId }: { projectId: string }) {
  const { project, isLoading } = useProject(projectId)
  
  if (isLoading) {
    return (
      <div className="h-[400px] w-full"> {/* Reserve exact space */}
        <Skeleton className="h-full w-full" />
      </div>
    )
  }
  
  return <ProjectCardContent project={project} />
}
```

**Rationale:** Skeleton screens with reserved space prevent Cumulative Layout Shift (CLS <0.1 requirement).

---

### 7. Persona-Specific Content Patterns

**Conditional Rendering Pattern:**

```typescript
// Pattern: Single component, persona-aware props
interface ProjectCardProps {
  project: Project
  persona: Persona
}

function ProjectCard({ project, persona }: ProjectCardProps) {
  const highlight = {
    recruiter: project.recruiterHighlight,
    client: project.clientHighlight,
    developer: project.developerHighlight
  }[persona]
  
  const metrics = persona === 'client' 
    ? project.roiMetrics 
    : persona === 'developer'
    ? { lcp: project.performanceLCP, inp: project.performanceINP }
    : null
  
  return (
    <Card>
      <CardHeader>{project.title}</CardHeader>
      <CardContent>
        <p>{highlight}</p>
        {metrics && <MetricsDisplay metrics={metrics} />}
      </CardContent>
    </Card>
  )
}
```

**Rationale:** Single component with persona-aware logic prevents code duplication and ensures consistent behavior.

---

### 8. Performance Optimization Patterns

**Image Optimization Pattern:**

```typescript
// ALWAYS use Next.js Image component
import Image from 'next/image'

// ✅ Correct
<Image
  src="/projects/thumbnail.jpg"
  alt="Project thumbnail"
  width={800}
  height={600}
  priority={isFeatured} // LCP optimization for above-fold
  placeholder="blur"
  blurDataURL={blurDataURL}
/>

// ❌ NEVER use <img> tag
<img src="/projects/thumbnail.jpg" /> // Forbidden
```

**Dynamic Import Pattern (Code Splitting):**

```typescript
// Heavy components: Use next/dynamic with ssr: false
import dynamic from 'next/dynamic'

const CodePlayground = dynamic(
  () => import('@/components/CodePlayground'),
  { 
    ssr: false, // Client-side only
    loading: () => <SkeletonPlayground />
  }
)

const ThreeJSGallery = dynamic(
  () => import('@/components/ThreeJSGallery'),
  { ssr: false }
)
```

**Rationale:** Consistent optimization patterns ensure Core Web Vitals targets are met.

---

### Enforcement Guidelines

**All AI Agents MUST:**

1. **Read `project-context.md` first** before implementing any code
2. **Use the exact API response format** defined in Pattern 1
3. **Follow Prisma naming conventions** defined in Pattern 2
4. **Use skeleton screens** for all loading states (Pattern 6)
5. **Never use `<img>` tags** - always use Next.js `<Image>` (Pattern 8)
6. **Implement graceful degradation** for all API calls (Pattern 5)
7. **Use immutable state updates** in React Context (Pattern 4)

**Pattern Verification:**

- ESLint rules enforce TypeScript strict mode and React best practices
- Prettier enforces consistent code formatting
- Lighthouse CI enforces Core Web Vitals targets (LCP <2.5s, INP <200ms, CLS <0.1)
- Playwright tests verify persona switching and error handling patterns

**Pattern Updates:**

- Patterns are documented in this architecture document
- Implementation details are in `project-context.md`
- Updates require approval via architecture review process
- All agents must be notified of pattern changes

---

### Pattern Examples

**✅ Good Example: API Route with Consistent Response Format**

```typescript
// app/api/leetcode/stats/route.ts
export async function GET() {
  try {
    const stats = await fetchLeetCodeStats()
    return Response.json({
      data: stats,
      status: 'success',
      timestamp: new Date().toISOString(),
      metadata: { cached: false, source: 'leetcode-api' }
    })
  } catch (error) {
    console.error('[LeetCode API Error]', error)
    const cached = await getCachedLeetCodeStats()
    return Response.json({
      data: cached,
      status: 'stale',
      timestamp: cached?.timestamp || new Date().toISOString(),
      error: {
        code: 'API_UNAVAILABLE',
        message: 'LeetCode API temporarily unavailable'
      }
    }, { status: 200 })
  }
}
```

**❌ Anti-Pattern: Inconsistent Response Format**

```typescript
// ❌ DON'T DO THIS
export async function GET() {
  try {
    const stats = await fetchLeetCodeStats()
    return Response.json(stats) // Missing wrapper, status, timestamp
  } catch (error) {
    return Response.json({ error: error.message }, { status: 500 }) // Different format
  }
}
```

**✅ Good Example: Component with Skeleton Loading**

```typescript
function SkillVerification() {
  const { stats, isLoading, isStale, timestamp } = useGitHubStats()
  
  if (isLoading) {
    return (
      <div className="h-[200px] w-full"> {/* Reserve space */}
        <Skeleton className="h-full w-full" />
      </div>
    )
  }
  
  return (
    <div className="h-[200px] w-full">
      <StatsDisplay stats={stats} />
      {isStale && <StaleIndicator timestamp={timestamp} />}
    </div>
  )
}
```

**❌ Anti-Pattern: Loading Without Reserved Space**

```typescript
// ❌ DON'T DO THIS - Causes layout shift (CLS violation)
function SkillVerification() {
  const { stats, isLoading } = useGitHubStats()
  
  if (isLoading) return <p>Loading...</p> // No reserved space
  
  return <div className="h-[200px]"><StatsDisplay stats={stats} /></div>
}
```

---

### Summary

**Implementation consistency is achieved through:**

1. **Comprehensive rules in `project-context.md`** (311 lines, 7 sections)
2. **Architecture-level patterns in this document** (8 critical patterns)
3. **Automated enforcement** (ESLint, Prettier, Lighthouse CI, Playwright)
4. **Clear examples** (good patterns vs anti-patterns)

**AI agents implementing this architecture must:**
- Read both `project-context.md` AND this architecture document
- Follow all naming conventions, response formats, and error handling patterns
- Use skeleton screens for loading states
- Implement graceful degradation for all external APIs
- Optimize for Core Web Vitals targets (LCP <2.5s, INP <200ms, CLS <0.1)

---

## Project Structure & Boundaries

### Complete Project Directory Structure

```
portfolio/
├── README.md
├── package.json
├── package-lock.json
├── next.config.js
├── tailwind.config.ts
├── tsconfig.json
├── postcss.config.js
├── .env.local
├── .env.example
├── .gitignore
├── .eslintrc.json
├── .prettierrc
├── playwright.config.ts
├── .github/
│   └── workflows/
│       ├── ci.yml
│       ├── lighthouse.yml
│       └── deploy.yml
├── prisma/
│   ├── schema.prisma
│   ├── seed.ts
│   └── migrations/
│       └── [timestamp]_init/
├── public/
│   ├── robots.txt
│   ├── sitemap.xml
│   ├── favicon.ico
│   ├── og-image.png
│   ├── resume.pdf
│   └── assets/
│       ├── projects/
│       ├── videos/
│       └── icons/
├── src/
│   ├── app/
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── globals.css
│   │   ├── error.tsx
│   │   ├── global-error.tsx
│   │   ├── not-found.tsx
│   │   ├── sitemap.ts
│   │   ├── robots.ts
│   │   ├── manifest.ts
│   │   ├── (public)/
│   │   │   ├── layout.tsx
│   │   │   ├── about/
│   │   │   │   └── page.tsx
│   │   │   ├── projects/
│   │   │   │   ├── page.tsx
│   │   │   │   └── [slug]/
│   │   │   │       └── page.tsx
│   │   │   ├── skills/
│   │   │   │   └── page.tsx
│   │   │   ├── contact/
│   │   │   │   └── page.tsx
│   │   │   └── resume/
│   │   │       └── page.tsx
│   │   ├── (admin)/
│   │   │   ├── layout.tsx
│   │   │   ├── admin/
│   │   │   │   ├── page.tsx
│   │   │   │   ├── projects/
│   │   │   │   │   ├── page.tsx
│   │   │   │   │   ├── new/
│   │   │   │   │   │   └── page.tsx
│   │   │   │   │   └── [id]/
│   │   │   │   │       ├── page.tsx
│   │   │   │   │       └── edit/
│   │   │   │   │           └── page.tsx
│   │   │   │   ├── settings/
│   │   │   │   │   └── page.tsx
│   │   │   │   └── analytics/
│   │   │   │       └── page.tsx
│   │   │   └── login/
│   │   │       └── page.tsx
│   │   └── api/
│   │       ├── auth/
│   │       │   └── [...nextauth]/
│   │       │       └── route.ts
│   │       ├── github/
│   │       │   ├── stats/
│   │       │   │   └── route.ts
│   │       │   └── activity/
│   │       │       └── route.ts
│   │       ├── leetcode/
│   │       │   └── stats/
│   │       │       └── route.ts
│   │       ├── projects/
│   │       │   ├── route.ts
│   │       │   └── [id]/
│   │       │       └── route.ts
│   │       ├── contact/
│   │       │   └── route.ts
│   │       ├── analytics/
│   │       │   └── route.ts
│   │       └── upload/
│   │           └── route.ts
│   ├── components/
│   │   ├── ui/
│   │   │   ├── button.tsx
│   │   │   ├── card.tsx
│   │   │   ├── dialog.tsx
│   │   │   ├── dropdown-menu.tsx
│   │   │   ├── form.tsx
│   │   │   ├── input.tsx
│   │   │   ├── label.tsx
│   │   │   ├── select.tsx
│   │   │   ├── skeleton.tsx
│   │   │   ├── tabs.tsx
│   │   │   ├── toast.tsx
│   │   │   └── toaster.tsx
│   │   ├── layout/
│   │   │   ├── header.tsx
│   │   │   ├── footer.tsx
│   │   │   ├── navigation.tsx
│   │   │   └── sidebar.tsx
│   │   ├── features/
│   │   │   ├── persona-selector/
│   │   │   │   ├── persona-selector.tsx
│   │   │   │   ├── persona-badge.tsx
│   │   │   │   └── persona-indicator.tsx
│   │   │   ├── projects/
│   │   │   │   ├── project-card.tsx
│   │   │   │   ├── project-grid.tsx
│   │   │   │   ├── project-detail.tsx
│   │   │   │   ├── code-playground.tsx
│   │   │   │   ├── video-walkthrough.tsx
│   │   │   │   ├── performance-metrics.tsx
│   │   │   │   └── architecture-diagram.tsx
│   │   │   ├── skills/
│   │   │   │   ├── skills-matrix.tsx
│   │   │   │   ├── skill-badge.tsx
│   │   │   │   └── proficiency-indicator.tsx
│   │   │   ├── verification/
│   │   │   │   ├── github-stats.tsx
│   │   │   │   ├── leetcode-stats.tsx
│   │   │   │   ├── contribution-graph.tsx
│   │   │   │   ├── activity-indicator.tsx
│   │   │   │   └── last-active.tsx
│   │   │   ├── contact-form/
│   │   │   │   ├── contact-form.tsx
│   │   │   │   ├── persona-specific-fields.tsx
│   │   │   │   └── roi-calculator.tsx
│   │   │   └── analytics/
│   │   │       ├── analytics-dashboard.tsx
│   │   │       ├── engagement-chart.tsx
│   │   │       └── conversion-funnel.tsx
│   │   ├── admin/
│   │   │   ├── project-form.tsx
│   │   │   ├── image-upload.tsx
│   │   │   ├── persona-preview.tsx
│   │   │   ├── publish-controls.tsx
│   │   │   └── analytics-overview.tsx
│   │   └── shared/
│   │       ├── loading-skeleton.tsx
│   │       ├── error-boundary.tsx
│   │       ├── seo-head.tsx
│   │       └── theme-provider.tsx
│   ├── contexts/
│   │   ├── PersonaContext.tsx
│   │   └── ThemeContext.tsx
│   ├── hooks/
│   │   ├── usePersona.ts
│   │   ├── useGitHubStats.ts
│   │   ├── useLeetCodeStats.ts
│   │   ├── useRealTimePolling.ts
│   │   ├── useAnalytics.ts
│   │   └── useMediaQuery.ts
│   ├── lib/
│   │   ├── db.ts
│   │   ├── auth.ts
│   │   ├── cache.ts
│   │   ├── analytics.ts
│   │   ├── metadata.ts
│   │   ├── errors.ts
│   │   ├── validation.ts
│   │   ├── api-client.ts
│   │   ├── projects.ts
│   │   └── utils.ts
│   ├── types/
│   │   ├── persona.ts
│   │   ├── project.ts
│   │   ├── github.ts
│   │   ├── leetcode.ts
│   │   ├── analytics.ts
│   │   └── api.ts
│   ├── config/
│   │   ├── site.ts
│   │   ├── navigation.ts
│   │   └── personas.ts
│   └── middleware.ts
├── __tests__/
│   ├── components/
│   │   ├── persona-selector.test.tsx
│   │   ├── project-card.test.tsx
│   │   └── contact-form.test.tsx
│   ├── hooks/
│   │   ├── usePersona.test.ts
│   │   └── useGitHubStats.test.ts
│   ├── lib/
│   │   ├── cache.test.ts
│   │   ├── validation.test.ts
│   │   └── utils.test.ts
│   └── api/
│       ├── github.test.ts
│       └── contact.test.ts
├── e2e/
│   ├── persona-selection.spec.ts
│   ├── project-showcase.spec.ts
│   ├── contact-form.spec.ts
│   ├── admin-panel.spec.ts
│   └── performance.spec.ts
└── docs/
    ├── architecture.md
    ├── deployment.md
    └── api-reference.md
```

### Architectural Boundaries

**API Boundaries:**

- **External API Endpoints** (Public-facing):
  - `/api/github/stats` - GitHub contribution statistics (cached 24h)
  - `/api/github/activity` - Recent commit activity (cached 1h)
  - `/api/leetcode/stats` - LeetCode problem-solving stats (cached 24h)
  - `/api/contact` - Contact form submission (rate-limited: 5 req/hour per IP)
  - `/api/projects` - Public project listing (cached, ISR every 1h)

- **Internal API Endpoints** (Admin-only, NextAuth protected):
  - `/api/projects` (POST/PUT/DELETE) - CRUD operations
  - `/api/upload` - Image upload with optimization
  - `/api/analytics` - Analytics data retrieval

- **Authentication Boundary**:
  - `/api/auth/[...nextauth]` - NextAuth.js authentication
  - All `/admin/*` routes protected by middleware
  - Session-based authentication with HTTP-only cookies

**Component Boundaries:**

- **Server Components** (Default, no `'use client'`):
  - All page components in `src/app/(public)/`
  - Layout components (`header.tsx`, `footer.tsx`)
  - Static content components (SEO, metadata)
  - **Why**: Reduces bundle size, improves LCP, enables server-side data fetching

- **Client Components** (Explicit `'use client'` directive):
  - `PersonaSelector` - Interactive state management
  - `CodePlayground` - Dynamic CodeSandbox/StackBlitz embedding
  - `ContactForm` - Form validation and submission
  - `ArchitectureDiagram` - Interactive SVG/Canvas elements
  - All components in `src/components/ui/` (shadcn/ui)
  - **Why**: Requires browser APIs, event handlers, or React hooks (useState, useEffect)

- **Hybrid Components** (Server wrapper + Client children):
  - `ProjectDetail` (Server) wraps `CodePlayground` (Client)
  - `SkillsPage` (Server) wraps `SkillsMatrix` (Client with animations)
  - **Pattern**: Server component fetches data, passes to Client component as props

**Service Boundaries:**

- **Database Layer** (`src/lib/db.ts`):
  - Prisma Client singleton
  - Connection pooling for serverless
  - All database access goes through this layer
  - **Boundary**: Only API routes and Server Components can import

- **Cache Layer** (`src/lib/cache.ts`):
  - Redis or in-memory cache (Vercel KV)
  - Caching strategy: GitHub (24h), LeetCode (24h), real-time activity (1h)
  - **Boundary**: Only API routes can write to cache; components read through API

- **External API Integration** (`src/lib/api-client.ts`):
  - Centralized HTTP client with retry logic
  - Rate limiting and error handling
  - **Boundary**: Only server-side code (API routes) can call external APIs

**Data Boundaries:**

- **Database Schema** (Prisma):
  - `Project` table - Project showcase data
  - `User` table - Admin authentication
  - `Analytics` table - Engagement metrics
  - `ContactSubmission` table - Contact form entries
  - **Boundary**: No direct database access from client; all through API routes

- **Data Access Patterns**:
  - **Read**: Server Components → Prisma → Database
  - **Write**: Client Component → API Route → Prisma → Database
  - **Cache**: API Route → Cache Layer → External API

- **Caching Boundaries**:
  - **Next.js Cache**: `fetch()` with `revalidate` option (ISR)
  - **API Cache**: Redis/Vercel KV for external API responses
  - **CDN Cache**: Vercel Edge Network for static assets
  - **Boundary**: Cache invalidation only from admin panel or scheduled jobs

### Requirements to Structure Mapping

**Feature/Epic Mapping:**

**Epic: Persona & Content Personalization (FR1-FR7)**
- **Context**: `src/contexts/PersonaContext.tsx`
- **Components**: `src/components/features/persona-selector/`
- **Hooks**: `src/hooks/usePersona.ts`
- **Types**: `src/types/persona.ts`
- **Config**: `src/config/personas.ts`
- **Pages**: All pages in `src/app/(public)/` consume persona context
- **Tests**: `__tests__/components/persona-selector.test.tsx`, `e2e/persona-selection.spec.ts`

**Epic: Project Showcase & Interactive Demonstrations (FR8-FR17)**
- **Pages**: `src/app/(public)/projects/page.tsx`, `src/app/(public)/projects/[slug]/page.tsx`
- **Components**: `src/components/features/projects/`
- **API Routes**: `src/app/api/projects/route.ts`
- **Database**: `prisma/schema.prisma` (Project model)
- **Services**: `src/lib/projects.ts`
- **Types**: `src/types/project.ts`
- **Tests**: `__tests__/components/project-card.test.tsx`, `e2e/project-showcase.spec.ts`

**Epic: Real-Time Skill Verification (FR18-FR24)**
- **API Routes**: `src/app/api/github/`, `src/app/api/leetcode/`
- **Components**: `src/components/features/verification/`
- **Hooks**: `src/hooks/useGitHubStats.ts`, `src/hooks/useLeetCodeStats.ts`, `src/hooks/useRealTimePolling.ts`
- **Services**: `src/lib/cache.ts`, `src/lib/api-client.ts`
- **Types**: `src/types/github.ts`, `src/types/leetcode.ts`
- **Tests**: `__tests__/hooks/useGitHubStats.test.ts`, `__tests__/api/github.test.ts`

**Epic: Content Management (Admin) (FR25-FR34)**
- **Pages**: `src/app/(admin)/admin/`
- **Components**: `src/components/admin/`
- **API Routes**: `src/app/api/projects/` (POST/PUT/DELETE), `src/app/api/upload/`
- **Auth**: `src/lib/auth.ts`, `src/app/api/auth/[...nextauth]/`
- **Middleware**: `src/middleware.ts` (route protection)
- **Database**: `prisma/schema.prisma` (User model)
- **Tests**: `e2e/admin-panel.spec.ts`

**Epic: Visitor Engagement & Conversion (FR35-FR42)**
- **Pages**: `src/app/(public)/contact/page.tsx`, `src/app/(public)/resume/page.tsx`
- **Components**: `src/components/features/contact-form/`
- **API Routes**: `src/app/api/contact/route.ts`
- **Services**: `src/lib/validation.ts`
- **Database**: `prisma/schema.prisma` (ContactSubmission model)
- **Tests**: `__tests__/components/contact-form.test.tsx`, `e2e/contact-form.spec.ts`

**Epic: Analytics & Measurement (FR43-FR48)**
- **Components**: `src/components/features/analytics/`, `src/components/admin/analytics-overview.tsx`
- **API Routes**: `src/app/api/analytics/route.ts`
- **Services**: `src/lib/analytics.ts`
- **Hooks**: `src/hooks/useAnalytics.ts`
- **Database**: `prisma/schema.prisma` (Analytics model)
- **Types**: `src/types/analytics.ts`
- **Integration**: Vercel Analytics, Plausible Analytics

**Epic: SEO & Discoverability (FR49-FR56)**
- **Files**: `src/app/layout.tsx`, `src/app/sitemap.ts`, `src/app/robots.ts`, `src/app/manifest.ts`
- **Services**: `src/lib/metadata.ts`
- **Components**: `src/components/shared/seo-head.tsx`
- **Static**: `public/robots.txt`, `public/sitemap.xml`
- **Tests**: E2E tests verify meta tags, structured data

**Cross-Cutting Concerns:**

**Authentication System**
- **Middleware**: `src/middleware.ts` (route protection)
- **Services**: `src/lib/auth.ts`
- **API Routes**: `src/app/api/auth/[...nextauth]/route.ts`
- **Config**: NextAuth.js configuration
- **Database**: `prisma/schema.prisma` (User, Session, Account models)
- **Tests**: E2E tests for login flow

**Error Handling & Resilience**
- **Components**: `src/app/error.tsx`, `src/app/global-error.tsx`, `src/components/shared/error-boundary.tsx`
- **Services**: `src/lib/errors.ts` (custom error classes)
- **Pattern**: All API routes use standardized error response format
- **Tests**: Unit tests for error handling logic

**Performance Optimization**
- **Config**: `next.config.js` (image optimization, bundle analysis)
- **Components**: `src/components/shared/loading-skeleton.tsx`
- **Middleware**: `src/middleware.ts` (caching headers)
- **Tests**: `e2e/performance.spec.ts` (Lighthouse CI)

**Validation & Security**
- **Services**: `src/lib/validation.ts` (Zod schemas)
- **Middleware**: `src/middleware.ts` (rate limiting, CSP headers)
- **API Routes**: All routes validate input before processing
- **Tests**: Unit tests for validation logic

### Integration Points

**Internal Communication:**

- **Context-Based State Management**:
  - `PersonaContext` provides persona state to all components
  - `ThemeContext` provides theme state (if dark mode implemented)
  - **Pattern**: Context Provider in root layout, `useContext` hook in components

- **Component Communication**:
  - **Parent → Child**: Props (Server Components pass data to Client Components)
  - **Child → Parent**: Callbacks (Client Components emit events to parent)
  - **Sibling → Sibling**: Shared context or URL state (persona selection)

- **Server ↔ Client Communication**:
  - **Server → Client**: Initial props from Server Components
  - **Client → Server**: API routes via `fetch()` or form actions
  - **Pattern**: Server Components fetch data, Client Components handle interactivity

**External Integrations:**

- **GitHub API**:
  - **Endpoint**: `https://api.github.com/users/{username}/events`
  - **Authentication**: Personal Access Token (server-side only)
  - **Rate Limit**: 5,000 req/hour (authenticated)
  - **Caching**: 24 hours for stats, 1 hour for activity
  - **Fallback**: Cached data if API unavailable
  - **Integration Point**: `src/app/api/github/stats/route.ts`

- **LeetCode API** (Unofficial):
  - **Endpoint**: `https://leetcode.com/graphql` or third-party proxy
  - **Rate Limit**: Unknown (conservative caching)
  - **Caching**: 24 hours
  - **Fallback**: Manual override in admin panel
  - **Integration Point**: `src/app/api/leetcode/stats/route.ts`

- **Vercel Analytics**:
  - **Integration**: `@vercel/analytics` package
  - **Tracking**: Core Web Vitals, page views, custom events
  - **Privacy**: GDPR compliant, no cookies
  - **Integration Point**: `src/app/layout.tsx`

- **Plausible Analytics** (Optional):
  - **Integration**: Script tag in layout
  - **Tracking**: Page views, custom events (persona selection, project interactions)
  - **Privacy**: Privacy-friendly, GDPR compliant
  - **Integration Point**: `src/app/layout.tsx`

**Data Flow:**

1. **User Visits Landing Page**:
   - Next.js Server → Renders `page.tsx` (Server Component)
   - Hydrates `PersonaSelector` (Client Component)
   - User selects persona → Updates `PersonaContext`
   - All components re-render with persona-specific content

2. **User Views Project Detail**:
   - Next.js Server → Fetches project from database (Prisma)
   - Renders `ProjectDetail` (Server Component) with data
   - Hydrates `CodePlayground` (Client Component) with project code
   - User interacts with playground → Client-side only (no server round-trip)

3. **User Submits Contact Form**:
   - Client Component → Validates input (Zod)
   - Client → `POST /api/contact` (API Route)
   - API Route → Validates again, saves to database (Prisma)
   - API Route → Sends email notification (optional)
   - API Route → Returns success response
   - Client → Shows success toast

4. **Admin Adds New Project**:
   - Admin → Fills project form (Client Component)
   - Admin → Uploads images → `POST /api/upload` (optimizes, stores)
   - Admin → Submits form → `POST /api/projects` (API Route)
   - API Route → Validates, saves to database (Prisma)
   - API Route → Invalidates cache (ISR revalidation)
   - Admin → Sees success message, redirected to project list

5. **Real-Time Stats Update**:
   - Client Component → Mounts, calls `useGitHubStats()` hook
   - Hook → `fetch('/api/github/stats')` (API Route)
   - API Route → Checks cache (Redis/Vercel KV)
   - If cached → Returns cached data
   - If stale → Fetches from GitHub API, updates cache, returns fresh data
   - Hook → Polls every 5 minutes (configurable)
   - Component → Displays stats with "Last updated" timestamp

### File Organization Patterns

**Configuration Files:**

- **Root Level**: `package.json`, `next.config.js`, `tailwind.config.ts`, `tsconfig.json`, `.env.local`
- **Prisma**: `prisma/schema.prisma` (database schema)
- **Testing**: `playwright.config.ts` (E2E tests), `jest.config.js` (unit tests, if added)
- **CI/CD**: `.github/workflows/` (GitHub Actions)
- **Pattern**: All config files at root for tool discoverability

**Source Organization:**

- **App Router Structure** (`src/app/`):
  - Route groups: `(public)` for public pages, `(admin)` for admin pages
  - **Why**: Separate layouts, middleware, and error handling per group
  - **Pattern**: Each route has `page.tsx` (page component) and optional `layout.tsx` (layout)

- **Component Organization** (`src/components/`):
  - `ui/` - shadcn/ui primitives (button, card, dialog, etc.)
  - `layout/` - Layout components (header, footer, navigation)
  - `features/` - Feature-specific components (persona-selector, projects, verification)
  - `admin/` - Admin-only components (project-form, image-upload)
  - `shared/` - Shared utilities (loading-skeleton, error-boundary)
  - **Pattern**: Feature-based organization, not technical organization

- **Library Organization** (`src/lib/`):
  - Single-responsibility modules (db.ts, auth.ts, cache.ts, etc.)
  - **Pattern**: Each file exports related functions, no default exports

- **Type Organization** (`src/types/`):
  - Domain-specific types (persona.ts, project.ts, github.ts, etc.)
  - **Pattern**: Types mirror data models and API responses

**Test Organization:**

- **Unit Tests** (`__tests__/`):
  - Mirror source structure: `__tests__/components/`, `__tests__/hooks/`, `__tests__/lib/`
  - **Naming**: `[filename].test.tsx` or `[filename].test.ts`
  - **Pattern**: Co-located with source (alternative: `__tests__/` at root)

- **E2E Tests** (`e2e/`):
  - User journey-based: `persona-selection.spec.ts`, `project-showcase.spec.ts`
  - **Naming**: `[feature].spec.ts`
  - **Pattern**: Playwright tests, run in CI/CD pipeline

- **Test Utilities** (`__tests__/__mocks__/`, `e2e/fixtures/`):
  - Mock data, test fixtures, helper functions
  - **Pattern**: Shared across tests, reusable

**Asset Organization:**

- **Static Assets** (`public/`):
  - `robots.txt`, `sitemap.xml`, `favicon.ico` at root
  - `assets/projects/` - Project images
  - `assets/videos/` - Video walkthroughs
  - `assets/icons/` - Custom icons
  - **Pattern**: Organized by type, served via CDN

- **Dynamic Assets** (Database):
  - Project images uploaded via admin panel
  - Stored in Vercel Blob Storage or similar
  - **Pattern**: URLs stored in database, files in blob storage

### Development Workflow Integration

**Development Server Structure:**

- **Command**: `npm run dev` (Next.js dev server on port 3000)
- **Hot Reload**: Fast Refresh for instant updates
- **Environment**: `.env.local` for local development
- **Database**: Local PostgreSQL or Docker container
- **Pattern**: All developers use same structure, no custom setup

**Build Process Structure:**

- **Command**: `npm run build` (Next.js production build)
- **Output**: `.next/` directory (optimized bundles)
- **Static Generation**: Pre-renders all public pages (ISR)
- **Bundle Analysis**: `@next/bundle-analyzer` to monitor bundle size
- **Pattern**: CI/CD runs build, fails if bundle size exceeds threshold

**Deployment Structure:**

- **Platform**: Vercel (automatic deployments from Git)
- **Environment Variables**: Set in Vercel dashboard
- **Database**: PostgreSQL (Vercel Postgres or external)
- **CDN**: Vercel Edge Network (automatic)
- **Pattern**: Push to `main` → Auto-deploy to production, push to `dev` → Auto-deploy to preview

---

## Architecture Validation Results

### Coherence Validation ✅

**Decision Compatibility:**

All architectural decisions work together harmoniously. The Next.js 14+ App Router + TypeScript + Prisma + PostgreSQL + Vercel stack is industry-standard and fully compatible. shadcn/ui (Tailwind CSS) integrates perfectly with Next.js. NextAuth.js + Prisma is a proven authentication pattern. Vercel Analytics + Plausible are complementary analytics solutions with no conflicts. All technology versions are specified (Next.js 14+, TypeScript strict mode, Prisma ORM).

**Pattern Consistency:**

Implementation patterns align perfectly with technology choices. Server Components by default with Client Components only when needed follows Next.js 14+ best practices. API routes proxy external APIs for consistent security. Standardized error response format ensures consistency across all API routes. Skeleton screens for loading states provide consistent UX. Naming conventions (kebab-case files, PascalCase components, camelCase functions) are consistent across all examples.

**Structure Alignment:**

Project structure fully supports all architectural decisions. Route groups `(public)` and `(admin)` enable separate layouts and middleware. Feature-based component organization supports the persona-based architecture. API route structure mirrors functional requirements (github/, leetcode/, projects/, contact/). Test structure mirrors source structure for discoverability.

### Requirements Coverage Validation ✅

**Epic/Feature Coverage:**

All 56 functional requirements (FR1-FR56) across 8 epic categories are fully supported:

- **FR1-FR7 (Persona & Content Personalization)**: PersonaContext, persona-selector components, usePersona hook, persona.ts types, personas.ts config
- **FR8-FR17 (Project Showcase & Interactive Demonstrations)**: Project pages, project components, API routes, database schema, projects.ts service
- **FR18-FR24 (Real-Time Skill Verification)**: GitHub/LeetCode API routes, verification components, caching layer, useGitHubStats/useLeetCodeStats hooks
- **FR25-FR34 (Content Management - Admin)**: Admin pages, CRUD API routes, NextAuth authentication, middleware protection
- **FR35-FR42 (Visitor Engagement & Conversion)**: Contact form, resume download, persona-specific fields, ROI calculator
- **FR43-FR48 (Analytics & Measurement)**: Vercel Analytics integration, Plausible Analytics, analytics API routes, analytics components
- **FR49-FR56 (SEO & Discoverability)**: sitemap.ts, robots.ts, manifest.ts, metadata.ts, structured data, Open Graph tags

**Functional Requirements Coverage:**

Every functional requirement has explicit architectural support mapped to specific files and directories. No gaps in FR coverage. Cross-cutting FRs (performance, security, accessibility) are addressed through architectural patterns and technology choices.

**Non-Functional Requirements Coverage:**

- **Performance (LCP <2.5s, INP <200ms, CLS <0.1)**: Server Components by default, ISR caching, lazy loading with `next/dynamic`, image optimization with Next.js `<Image>`, skeleton screens with reserved space
- **SEO**: Server-side rendering for all public pages, metadata API, structured data (JSON-LD), XML sitemap, robots.txt, Open Graph tags
- **Accessibility (WCAG 2.1 AA)**: Semantic HTML5, keyboard navigation, screen reader support, 4.5:1 color contrast (mentioned in NFRs)
- **Security**: API keys server-side only, NextAuth.js authentication, input validation (Zod), sanitization, rate limiting, CSP headers
- **Browser Compatibility**: Playwright cross-browser testing, progressive enhancement, graceful degradation
- **Mobile Responsiveness**: Mobile-first design, touch-optimized interactions (44x44px touch targets), responsive images
- **Reliability (99.9% uptime)**: Vercel hosting, graceful degradation for external APIs, error boundaries, cached fallbacks
- **Scalability**: Admin panel for content updates without code changes, ISR for caching, CDN distribution

### Implementation Readiness Validation ✅

**Decision Completeness:**

All critical architectural decisions are documented with specific versions and rationale:
- Decision 1: Technology Stack (Next.js 14+, TypeScript, Tailwind CSS, shadcn/ui)
- Decision 2: Starter Template (create-next-app with manual configuration)
- Decision 3: Database Schema & ORM (Prisma + PostgreSQL with complete schema)
- Decision 4: Rendering Strategy (Hybrid SSR/SSG with ISR)
- Decision 5: Deployment Platform (Vercel with automatic HTTPS/SSL)

Implementation patterns are comprehensive with 8 patterns including good/bad examples. Consistency rules are enforceable through ESLint, Prettier, Lighthouse CI, and Playwright.

**Structure Completeness:**

Complete project tree with 250+ files and directories specified. All integration points clearly defined (API boundaries, component boundaries, service boundaries, data boundaries). Component boundaries well-defined (Server vs Client components, hybrid patterns). No ambiguity for AI agents implementing features.

**Pattern Completeness:**

All potential conflict points addressed:
- Server vs Client component decisions clearly specified
- API key exposure prevented through server-side proxies
- Error handling standardized across all API routes
- Caching strategy defined for all external APIs
- Loading states use skeleton screens with reserved space
- Graceful degradation for all external integrations

Naming conventions are comprehensive. Communication patterns fully specified (Context, Props, API routes, fetch()). Process patterns complete (error handling, caching, validation, graceful degradation).

### Gap Analysis Results

**Critical Gaps:** NONE FOUND ✅

**Important Gaps:** NONE FOUND ✅

**Nice-to-Have Gaps (Optional Future Enhancements):**

1. **Deployment Checklist**: Could add specific deployment steps (environment variables checklist, database migration commands, DNS configuration, Vercel project setup)
2. **Monitoring Configuration**: Could specify Sentry configuration details (DSN setup, source maps, release tracking, custom error boundaries)
3. **Performance Budgets**: Could define specific bundle size limits (e.g., "First Load JS <200KB", "Total Blocking Time <300ms")
4. **Accessibility Testing Automation**: Could specify automated accessibility testing tools (axe-core integration, Lighthouse CI accessibility checks, WAVE API)

**Assessment**: These gaps are truly optional - the architecture is complete and implementation-ready without them. They represent future enhancements that can be added during or after implementation, not blockers.

### Validation Issues Addressed

**No critical or important issues found.** The architecture is coherent, complete, and ready for implementation.

All validation checks passed:
- ✅ Decision compatibility verified
- ✅ Pattern consistency confirmed
- ✅ Structure alignment validated
- ✅ All 56 functional requirements covered
- ✅ All non-functional requirements addressed
- ✅ Implementation readiness confirmed
- ✅ No blocking gaps identified

### Architecture Completeness Checklist

**✅ Requirements Analysis**

- [x] Project context thoroughly analyzed (PRD, UX Design Spec, Research, Project Context)
- [x] Scale and complexity assessed (Medium-High, 15-20 pages, 30-40 components, 5-8 API routes)
- [x] Technical constraints identified (Next.js 14+, TypeScript strict, Performance targets, Security requirements)
- [x] Cross-cutting concerns mapped (Performance optimization, Persona-based content, Error handling, Security)

**✅ Architectural Decisions**

- [x] Critical decisions documented with versions (5 decisions with rationale and alternatives considered)
- [x] Technology stack fully specified (Next.js 14+, TypeScript, Prisma, PostgreSQL, Vercel, shadcn/ui)
- [x] Integration patterns defined (GitHub API, LeetCode API, Vercel Analytics, Plausible, NextAuth)
- [x] Performance considerations addressed (Server Components, ISR, lazy loading, image optimization, caching)

**✅ Implementation Patterns**

- [x] Naming conventions established (kebab-case files, PascalCase components, camelCase functions)
- [x] Structure patterns defined (Route groups, feature-based components, single-responsibility libs)
- [x] Communication patterns specified (Context providers, Props, API routes, fetch())
- [x] Process patterns documented (Error handling, caching, validation, graceful degradation)

**✅ Project Structure**

- [x] Complete directory structure defined (250+ files/directories with full tree)
- [x] Component boundaries established (Server vs Client components, hybrid patterns)
- [x] Integration points mapped (API boundaries, service boundaries, data boundaries, caching boundaries)
- [x] Requirements to structure mapping complete (All FR1-FR56 mapped to specific files/directories)

### Architecture Readiness Assessment

**Overall Status:** ✅ READY FOR IMPLEMENTATION

**Confidence Level:** HIGH

All validation checks passed with no critical or important gaps. The architecture is comprehensive, coherent, and provides clear guidance for AI agents to implement consistently.

**Key Strengths:**

1. **Complete Requirements Coverage**: All 56 functional requirements (FR1-FR56) mapped to specific architectural components with no gaps
2. **Coherent Technology Stack**: Industry-standard, fully compatible technologies (Next.js 14+, TypeScript, Prisma, PostgreSQL, Vercel) with proven track record
3. **Comprehensive Implementation Patterns**: 8 patterns with good/bad examples prevent AI agent conflicts and ensure consistency
4. **Detailed Project Structure**: 250+ files/directories specified, leaving no ambiguity for implementation
5. **Performance-First Architecture**: Server Components by default, ISR caching, lazy loading, image optimization, skeleton screens
6. **Security-First Design**: API keys server-side only, NextAuth authentication, input validation (Zod), rate limiting, CSP headers
7. **Clear Boundaries**: API, component, service, and data boundaries explicitly defined with communication patterns
8. **Graceful Degradation**: All external integrations (GitHub, LeetCode) have fallback strategies with cached data

**Areas for Future Enhancement:**

1. **Deployment Automation**: CI/CD pipeline could be expanded with automated database migrations, environment variable validation, deployment checklists
2. **Monitoring & Observability**: Sentry configuration details, custom dashboards, alert thresholds, performance monitoring
3. **Performance Budgets**: Specific bundle size limits, Lighthouse score thresholds in CI/CD, automated performance regression detection
4. **Accessibility Automation**: axe-core integration, automated WCAG compliance checks in CI/CD, accessibility regression testing

### Implementation Handoff

**AI Agent Guidelines:**

- **Read First**: Read both `project-context.md` (311 lines, 7 sections) AND this `architecture.md` document before implementing any feature
- **Follow Decisions**: Follow all architectural decisions exactly as documented (5 decisions with versions and rationale)
- **Use Patterns**: Use implementation patterns consistently across all components (8 patterns with good/bad examples)
- **Respect Boundaries**: Respect project structure and boundaries (API, component, service, data boundaries)
- **Refer to Examples**: When in doubt, refer to the good/bad examples provided in the "Implementation Patterns & Consistency Rules" section
- **Enforce Rules**: Use ESLint, Prettier, Lighthouse CI, and Playwright to enforce consistency rules automatically

**First Implementation Priority:**

```bash
# Step 1: Initialize Next.js 14+ project with App Router
npx create-next-app@latest portfolio --typescript --tailwind --app --src-dir --import-alias "@/*"

# Step 2: Install core dependencies
cd portfolio
npm install prisma @prisma/client next-auth zod @vercel/analytics

# Step 3: Install shadcn/ui
npx shadcn-ui@latest init

# Step 4: Initialize Prisma
npx prisma init

# Step 5: Create project structure (refer to "Complete Project Directory Structure" section)
# Create all directories: src/components/ui/, src/components/features/, src/lib/, etc.
mkdir -p src/components/{ui,layout,features,admin,shared}
mkdir -p src/{contexts,hooks,lib,types,config}
mkdir -p src/app/{api,\(public\),\(admin\)}
mkdir -p __tests__/{components,hooks,lib,api}
mkdir -p e2e

# Step 6: Implement Prisma schema (refer to "Decision 3: Database Schema & ORM" section)
# Copy the complete schema from the architecture document to prisma/schema.prisma

# Step 7: Run first migration
npx prisma migrate dev --name init

# Step 8: Start development server
npm run dev
```

**Next Steps After Initialization:**

1. **Implement Core Context**: Create `src/contexts/PersonaContext.tsx` (FR1-FR7)
2. **Build Persona Selector**: Create `src/components/features/persona-selector/persona-selector.tsx` (FR1-FR7)
3. **Set Up Database Connection**: Create `src/lib/db.ts` with Prisma Client singleton
4. **Implement API Routes**: Start with `/api/projects` (GET) for project listing (FR8-FR17)
5. **Create Project Components**: Build `src/components/features/projects/project-card.tsx` (FR8-FR17)

**Validation Strategy:**

- Run `npm run build` after each feature to ensure no build errors
- Run Playwright tests (`npm run test:e2e`) for user journey validation
- Run Lighthouse CI to validate Core Web Vitals targets (LCP <2.5s, INP <200ms, CLS <0.1)
- Use `npm run lint` to enforce code quality and consistency rules

---

## Architecture Completion Summary

### Workflow Completion

**Architecture Decision Workflow:** COMPLETED ✅  
**Total Steps Completed:** 8  
**Date Completed:** 2026-01-28  
**Document Location:** `_bmad-output/planning-artifacts/architecture.md`

### Final Architecture Deliverables

**📋 Complete Architecture Document**

- All architectural decisions documented with specific versions
- Implementation patterns ensuring AI agent consistency
- Complete project structure with all files and directories (250+ specified)
- Requirements to architecture mapping (FR1-FR56)
- Validation confirming coherence and completeness

**🏗️ Implementation Ready Foundation**

- **5 architectural decisions** made (Technology Stack, Starter Template, Database Schema, Rendering Strategy, Deployment Platform)
- **8 implementation patterns** defined (Naming Conventions, API Response Format, Error Handling, Caching Strategy, Server vs Client Components, Loading States, Database Access, Real-Time Data Polling)
- **8 architectural components** specified (Persona System, Project Showcase, Real-Time Verification, Admin Panel, Visitor Engagement, Analytics, SEO, System & Performance)
- **56 functional requirements** fully supported (FR1-FR56 across 8 epic categories)

**📚 AI Agent Implementation Guide**

- Technology stack with verified versions (Next.js 14+, TypeScript strict, Prisma ORM, PostgreSQL, Vercel)
- Consistency rules that prevent implementation conflicts (ESLint, Prettier, Lighthouse CI, Playwright)
- Project structure with clear boundaries (API, Component, Service, Data boundaries)
- Integration patterns and communication standards (Context, Props, API routes, fetch())

### Implementation Handoff

**For AI Agents:**

This architecture document is your complete guide for implementing the bmad portfolio project. Follow all decisions, patterns, and structures exactly as documented.

**First Implementation Priority:**

```bash
# Step 1: Initialize Next.js 14+ project with App Router
npx create-next-app@latest portfolio --typescript --tailwind --app --src-dir --import-alias "@/*"

# Step 2: Install core dependencies
cd portfolio
npm install prisma @prisma/client next-auth zod @vercel/analytics

# Step 3: Install shadcn/ui
npx shadcn-ui@latest init

# Step 4: Initialize Prisma
npx prisma init

# Step 5: Create project structure (refer to "Complete Project Directory Structure" section)
mkdir -p src/components/{ui,layout,features,admin,shared}
mkdir -p src/{contexts,hooks,lib,types,config}
mkdir -p src/app/{api,\(public\),\(admin\)}
mkdir -p __tests__/{components,hooks,lib,api}
mkdir -p e2e

# Step 6: Implement Prisma schema (refer to "Decision 3: Database Schema & ORM" section)
# Copy the complete schema from the architecture document to prisma/schema.prisma

# Step 7: Run first migration
npx prisma migrate dev --name init

# Step 8: Start development server
npm run dev
```

**Development Sequence:**

1. Initialize project using documented starter template
2. Set up development environment per architecture
3. Implement core architectural foundations (PersonaContext, database connection)
4. Build features following established patterns (Persona Selector → Project Showcase → Verification → Admin → Engagement → Analytics → SEO)
5. Maintain consistency with documented rules (refer to "Implementation Patterns & Consistency Rules" section)

### Quality Assurance Checklist

**✅ Architecture Coherence**

- [x] All decisions work together without conflicts
- [x] Technology choices are compatible (Next.js 14+ + TypeScript + Prisma + PostgreSQL + Vercel)
- [x] Patterns support the architectural decisions (Server Components, API proxies, standardized errors)
- [x] Structure aligns with all choices (Route groups, feature-based components, test mirroring)

**✅ Requirements Coverage**

- [x] All functional requirements are supported (FR1-FR56 mapped to specific files/directories)
- [x] All non-functional requirements are addressed (Performance, SEO, Accessibility, Security, Reliability, Scalability)
- [x] Cross-cutting concerns are handled (Performance optimization, Persona system, Error handling, Security)
- [x] Integration points are defined (GitHub API, LeetCode API, Vercel Analytics, Plausible, NextAuth)

**✅ Implementation Readiness**

- [x] Decisions are specific and actionable (5 decisions with versions and rationale)
- [x] Patterns prevent agent conflicts (8 patterns with good/bad examples)
- [x] Structure is complete and unambiguous (250+ files/directories specified)
- [x] Examples are provided for clarity (API routes, components, error handling, caching)

### Project Success Factors

**🎯 Clear Decision Framework**

Every technology choice was made collaboratively with clear rationale, ensuring all stakeholders understand the architectural direction. Alternatives were considered and documented for transparency.

**🔧 Consistency Guarantee**

Implementation patterns and rules ensure that multiple AI agents will produce compatible, consistent code that works together seamlessly. ESLint, Prettier, Lighthouse CI, and Playwright enforce these rules automatically.

**📋 Complete Coverage**

All project requirements are architecturally supported, with clear mapping from business needs to technical implementation. No functional requirement (FR1-FR56) is left unsupported.

**🏗️ Solid Foundation**

The chosen starter template (create-next-app) and architectural patterns (Next.js 14+ App Router, Server Components, Prisma ORM) provide a production-ready foundation following current best practices.

---

**Architecture Status:** READY FOR IMPLEMENTATION ✅

**Next Phase:** Begin implementation using the architectural decisions and patterns documented herein.

**Document Maintenance:** Update this architecture when major technical decisions are made during implementation.
