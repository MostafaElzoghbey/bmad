---
stepsCompleted: [1, 2, 3, 4]
status: 'complete'
completedDate: '2026-01-24'
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
- State management for persona system
- API caching and polling strategy
- Database schema design
- Error handling patterns
- Deployment configuration

**All critical decisions have been made collaboratively and documented below.**

---

### Decision 1: State Management for Persona System

**Decision:** React Context + localStorage

**Rationale:**
- Persona selection is **UX personalization**, not SEO-critical (search engines see default view)
- Meets <300ms transition requirement with pure client-side state updates
- localStorage persistence provides excellent UX (users return to preferred view)
- Aligns with "boring technology for stability" principle - no cookie management or URL complexity
- Clean separation: Server Components for static content, Client Components for persona-aware interactivity

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

export function PersonaProvider({ children }: { children: React.Node }) {
  const [persona, setPersonaState] = useState<Persona>(null)
  
  useEffect(() => {
    // Load from localStorage on mount
    const saved = localStorage.getItem('selectedPersona')
    if (saved) setPersonaState(saved as Persona)
  }, [])
  
  const setPersona = (newPersona: Persona) => {
    setPersonaState(newPersona)
    if (newPersona) {
      localStorage.setItem('selectedPersona', newPersona)
    }
  }
  
  return (
    <PersonaContext.Provider value={{ persona, setPersona }}>
      {children}
    </PersonaContext.Provider>
  )
}

export const usePersona = () => useContext(PersonaContext)
```

**Affects:** All pages, PersonaSelector component, content prioritization logic

---

### Decision 2: API Caching & Real-Time Data Strategy

**Decision:** SWR (stale-while-revalidate) with custom polling intervals

**Version:** `swr@latest` (Vercel's official library)

**Rationale:**
- Built specifically for Next.js by Vercel - perfect ecosystem fit
- Tiny bundle size (5KB) - critical for LCP <2.5s performance target
- Built-in features: automatic revalidation, deduplication, focus revalidation, error handling
- Meets all requirements: 5-min GitHub polling, 1-hour LeetCode polling, graceful degradation
- Hooks-based API is clean and maintainable

**Implementation Pattern:**
```typescript
// hooks/useGitHubStats.ts
import useSWR from 'swr'

const fetcher = (url: string) => fetch(url).then(r => r.json())

export function useGitHubStats() {
  const { data, error, isLoading } = useSWR(
    '/api/github/stats',
    fetcher,
    {
      refreshInterval: 5 * 60 * 1000, // 5 minutes
      revalidateOnFocus: false,
      dedupingInterval: 60 * 1000, // 1 minute
      fallbackData: null,
    }
  )
  
  return {
    stats: data?.data,
    timestamp: data?.timestamp,
    status: data?.status, // 'success' | 'stale'
    isLoading,
    isError: error
  }
}

// hooks/useLeetCodeStats.ts
export function useLeetCodeStats() {
  const { data, error, isLoading } = useSWR(
    '/api/leetcode/stats',
    fetcher,
    {
      refreshInterval: 60 * 60 * 1000, // 1 hour
      revalidateOnFocus: false,
      dedupingInterval: 10 * 60 * 1000, // 10 minutes
    }
  )
  
  return { stats: data?.data, isLoading, isError: error }
}
```

**API Route Pattern (Server-Side Caching):**
```typescript
// app/api/github/stats/route.ts
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

**Affects:** SkillVerification component, GitHub/LeetCode API routes, real-time data display

---

### Decision 3: Database Schema Design

**Decision:** Full Prisma schema with User, Project, Testimonial, and Analytics models

**Rationale:**
- Supports all PRD requirements (projects, testimonials, analytics)
- Persona-specific fields (recruiterHighlight, clientHighlight, developerHighlight) enable tri-persona architecture
- Performance metrics fields (LCP, INP, CLS) support "proof over claims" principle
- Analytics from day 1 enables data-driven optimization
- Flexible JSON fields (roiMetrics) for evolving requirements
- PostgreSQL native arrays for tech stack and screenshots

**Prisma Schema:**
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

**Affects:** Admin panel CRUD operations, project showcase, testimonials, analytics tracking

---

### Decision 4: Error Handling & Resilience Patterns

**Decision:** Graceful degradation with stale data fallback, error boundaries, and skeleton screens

**Rationale:**
- Aligns with project-context.md requirement for graceful degradation when APIs fail
- Prevents layout shift (CLS <0.1 requirement) with skeleton screens
- User-friendly error messages instead of technical errors
- Server-side logging for debugging without exposing internals

**Error Handling Patterns:**

**1. API Route Error Handling:**
```typescript
// app/api/github/stats/route.ts
export async function GET() {
  try {
    const stats = await fetchGitHubStats()
    return Response.json({ data: stats, status: 'success' })
  } catch (error) {
    console.error('GitHub API error:', error) // Server-side logging
    const cachedStats = await getCachedStats()
    return Response.json({ 
      data: cachedStats,
      timestamp: cachedStats?.timestamp,
      status: 'stale',
      error: 'API temporarily unavailable'
    }, { status: 200 }) // Still 200 to avoid SWR error state
  }
}
```

**2. Client-Side Error Boundaries:**
```typescript
// app/error.tsx (catches Server Component errors)
'use client'
export default function Error({ error, reset }: { error: Error, reset: () => void }) {
  return (
    <div className="error-container">
      <h2>Something went wrong</h2>
      <p>We're working on fixing this. Please try again.</p>
      <button onClick={() => reset()}>Try again</button>
    </div>
  )
}

// components/ErrorBoundary.tsx (for Client Components)
// Standard React Error Boundary implementation
```

**3. Loading States (No Layout Shift):**
```typescript
// app/loading.tsx
export default function Loading() {
  return <SkeletonScreen /> // Reserves space, prevents CLS
}

// components/SkillVerification.tsx
const { stats, isLoading, isError, status } = useGitHubStats()

if (isLoading) return <SkeletonStats />
if (isError || status === 'stale') {
  return (
    <div>
      <StaleDataIndicator timestamp={timestamp} />
      <p>GitHub stats temporarily unavailable</p>
    </div>
  )
}
```

**4. Form Validation:**
```typescript
// Use Zod for runtime validation
import { z } from 'zod'

const contactFormSchema = z.object({
  email: z.string().email('Please enter a valid email'),
  message: z.string().min(10, 'Message must be at least 10 characters').max(1000),
  persona: z.enum(['recruiter', 'client', 'developer'])
})

// Provide specific, user-friendly error messages
```

**Key Principles:**
- Show stale data with timestamp instead of error screens
- Skeleton screens reserve space during loading (no CLS)
- User-friendly messages: "Last updated 2 hours ago"
- Server-side logging for debugging
- SWR handles automatic retries with exponential backoff

**Affects:** All API integrations, loading states, form submissions, error displays

---

### Decision 5: Deployment & Environment Configuration

**Decision:** Vercel hosting with Git-based deployment and environment variable management

**Rationale:**
- Zero-config Next.js deployment (Vercel is built by Next.js creators)
- Automatic HTTPS/SSL and Edge Network CDN
- Preview deployments for pull requests
- Zero-downtime deployments with automatic rollback
- Environment variable management in dashboard (secure)

**Environment Variables:**
```bash
# Database
DATABASE_URL="postgresql://user:password@host:5432/database"

# Authentication (NextAuth.js)
NEXTAUTH_SECRET="<generate with: openssl rand -base64 32>"
NEXTAUTH_URL="https://your-domain.com"

# GitHub API (Skill Verification)
GITHUB_TOKEN="ghp_..." # Personal access token (5,000 req/hour)
GITHUB_USERNAME="your-username"

# LeetCode API
LEETCODE_USERNAME="your-username"

# Analytics
NEXT_PUBLIC_VERCEL_ANALYTICS_ID="<auto-set by Vercel>"
PLAUSIBLE_DOMAIN="your-domain.com" # If using Plausible

# Email (Contact Form)
SMTP_HOST="smtp.gmail.com"
SMTP_PORT="587"
SMTP_USER="your-email@gmail.com"
SMTP_PASSWORD="<app-specific password>"
```

**Vercel Configuration (`vercel.json`):**
```json
{
  "buildCommand": "prisma generate && next build",
  "installCommand": "npm install",
  "framework": "nextjs",
  "regions": ["iad1"]
}
```

**Git Workflow:**
- `main` branch → Production deployment (automatic)
- Pull requests → Preview deployments (automatic)
- Feature branches → Manual deployment (optional)

**Deployment Steps:**
1. Push to GitHub repository
2. Vercel automatically detects changes
3. Runs `prisma generate && next build`
4. Deploys to Edge Network
5. Zero-downtime with automatic rollback on failure

**Affects:** All deployment, environment configuration, CI/CD pipeline

---

### Decision Impact Analysis

**Implementation Sequence:**

1. **Project Initialization** (Story 1)
   - Run `create-next-app` with TypeScript + Tailwind
   - Initialize Git repository
   - Deploy to Vercel (empty app)

2. **Database Setup** (Story 2)
   - Add Prisma + PostgreSQL
   - Create schema (User, Project, Testimonial, Analytics models)
   - Run migrations
   - Seed initial data

3. **Authentication** (Story 3)
   - Add NextAuth.js
   - Configure credentials provider
   - Protect admin routes

4. **State Management** (Story 4)
   - Create PersonaContext
   - Implement PersonaProvider
   - Add localStorage persistence

5. **API Integration** (Story 5)
   - Add SWR dependency
   - Create GitHub/LeetCode API routes
   - Implement caching and error handling
   - Create custom hooks (useGitHubStats, useLeetCodeStats)

6. **UI Components** (Story 6)
   - Add shadcn/ui
   - Create PersonaSelector
   - Build SkillVerification component
   - Implement error boundaries and loading states

**Cross-Component Dependencies:**

- **PersonaContext** affects all pages and components that display persona-specific content
- **SWR hooks** depend on API routes being implemented first
- **Prisma schema** must be created before admin panel CRUD operations
- **Error boundaries** wrap all client components that may fail
- **Environment variables** must be configured in Vercel before deployment
