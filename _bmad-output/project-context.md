---
project_name: 'bmad'
user_name: 'Sasa'
date: '2026-01-29'
sections_completed: ['technology_stack', 'language_rules', 'framework_rules', 'testing_rules', 'code_quality_rules', 'workflow_rules', 'critical_rules', 'architectural_decisions']
status: 'complete'
rule_count: 8
optimized_for_llm: true
existing_patterns_found: 0
architecture_source: '_bmad-output/planning-artifacts/architecture.md'
---

# Project Context for AI Agents

_This file contains critical rules and patterns that AI agents must follow when implementing code in this project. Focus on unobvious details that agents might otherwise miss._

---

## Technology Stack & Versions

**Core Framework:**
- Next.js 14+ (App Router with React Server Components)
- React 18+ (Server Components + Client Components)
- TypeScript (strict mode required)

**Styling & UI:**
- Tailwind CSS (utility-first CSS framework)
- shadcn/ui (component library built on Radix UI)

**Development Tools:**
- ESLint (code linting)
- Prettier (code formatting)

**Testing:**
- Playwright (E2E cross-browser testing)
- Jest (unit testing)

**Hosting & Deployment:**
- Vercel (zero-config Next.js deployment with Edge Network CDN)
- Automatic HTTPS/SSL

**External APIs:**
- GitHub API (commit activity, contribution graphs)
- LeetCode/HackerRank API (problem-solving stats)

**Performance Targets:**
- LCP (Largest Contentful Paint): < 2.5 seconds
- INP (Interaction to Next Paint): < 200 milliseconds
- CLS (Cumulative Layout Shift): < 0.1
- Lighthouse Score: 90+ across all categories

---

## Critical Implementation Rules

### Language-Specific Rules (TypeScript)

**TypeScript Configuration:**
- **Strict mode REQUIRED** - All TypeScript strict checks must be enabled
- Use explicit type annotations for function parameters and return types
- Avoid `any` type - use `unknown` or proper type definitions instead
- Enable `noImplicitAny`, `strictNullChecks`, `strictFunctionTypes`

**Import/Export Patterns:**
- Use ES6 module syntax (`import`/`export`) consistently
- Prefer named exports over default exports for better refactoring support
- Use absolute imports with path aliases (e.g., `@/components`, `@/lib`, `@/utils`)
- Group imports: external packages → internal modules → types → styles

**Next.js 14+ Specific:**
- **Server Components by default** - Only add `'use client'` when necessary (interactivity, hooks, browser APIs)
- **Client Components** require `'use client'` directive at top of file
- Server Components cannot use React hooks (useState, useEffect, etc.)
- Async Server Components are allowed and encouraged for data fetching

**Error Handling:**
- Use try-catch blocks for async operations
- Provide specific error types, not generic Error
- Handle API failures gracefully with fallback UI
- Use Error Boundaries for client-side error handling

**Type Safety for APIs:**
- Define TypeScript interfaces for all API responses
- Use Zod or similar for runtime validation of external API data (GitHub, LeetCode)
- Type all props interfaces explicitly (no implicit any)

---

### Framework-Specific Rules (Next.js 14+ & React)

**Next.js App Router Architecture:**
- Use App Router (`app/` directory), NOT Pages Router
- File-based routing: `app/[locale]/page.tsx` for pages, `app/api/route.ts` for API routes
- Use `layout.tsx` for shared layouts, `loading.tsx` for loading states, `error.tsx` for error boundaries
- Metadata API: Export `metadata` object or `generateMetadata()` function for SEO

**Server vs Client Components:**
- **Default to Server Components** - faster, smaller bundle, better SEO
- Use Client Components (`'use client'`) ONLY for:
  - Interactive features (onClick, onChange handlers)
  - React hooks (useState, useEffect, useContext)
  - Browser APIs (localStorage, window, document)
  - Third-party libraries requiring client-side rendering
- **Persona selector, code playgrounds, real-time API polling = Client Components**
- **Static content, project showcases, SEO pages = Server Components**

**Data Fetching Patterns:**
- Server Components: Use async/await directly in component (no useEffect)
- Client Components: Use SWR or React Query for data fetching with caching
- API Routes: Create in `app/api/` for GitHub/LeetCode API proxying (keeps keys secure)
- Cache API responses: 24 hours for GitHub stats, 1 hour for real-time data

**Performance Optimization:**
- Use Next.js `<Image>` component for all images (automatic optimization, WebP/AVIF)
- Implement lazy loading with `next/dynamic` for heavy components (CodeSandbox, Three.js)
- Code splitting: Dynamic imports for persona-specific content
- Streaming with Suspense boundaries for progressive rendering

**Persona-Based Layout Implementation:**
- Use React Context or URL params to track selected persona (Recruiter/Client/Developer)
- Conditional rendering based on persona selection
- Shared components with persona-specific props for content prioritization
- Smooth CSS transitions (< 300ms) for layout transformations

**React Hooks Best Practices:**
- Use `useState` for local component state (persona selection, form inputs)
- Use `useEffect` sparingly - prefer Server Components for data fetching
- Custom hooks for reusable logic (useGitHubStats, usePersonaContext)
- Memoization with `useMemo`/`useCallback` only when necessary (avoid premature optimization)

**Styling with Tailwind CSS:**
- Use Tailwind utility classes, avoid inline styles
- Create reusable components with shadcn/ui as base
- Use Tailwind's responsive modifiers (`sm:`, `md:`, `lg:`) for mobile-first design
- Custom colors in `tailwind.config.ts` for brand consistency

---

### Testing Rules

**Playwright E2E Testing:**
- Test critical user journeys for all three personas (Recruiter/Client/Developer)
- Cross-browser testing: Chrome, Firefox, Safari, Edge (latest 2 versions)
- Test persona selector transformation and layout changes
- Test interactive features: CodeSandbox loading, contact form submission, real-time API updates
- Use Page Object Model pattern for maintainability
- Test mobile responsiveness (viewport testing)

**Jest Unit Testing:**
- Test utility functions, custom hooks, and business logic
- Mock external API calls (GitHub, LeetCode) in unit tests
- Test TypeScript type safety (compile-time checks)
- Aim for high coverage on critical paths (persona logic, API integration, form validation)

**Test Organization:**
- E2E tests: `tests/e2e/` or `__tests__/e2e/`
- Unit tests: Co-locate with source files (`component.test.tsx` next to `component.tsx`)
- Test fixtures and helpers in `tests/fixtures/` and `tests/helpers/`

**Performance Testing:**
- Lighthouse CI in test pipeline to enforce Core Web Vitals targets
- Test LCP < 2.5s, INP < 200ms, CLS < 0.1 on every deployment
- Performance regression tests for critical pages

**Accessibility Testing:**
- Automated accessibility tests with axe-core or Playwright accessibility checks
- Test keyboard navigation for all interactive elements
- Test screen reader compatibility (ARIA labels, semantic HTML)
- Ensure WCAG 2.1 AA compliance

**API Mocking:**
- Mock GitHub API responses for consistent testing
- Test graceful degradation when APIs fail
- Test rate limiting scenarios
- Verify cached data fallback behavior

---

### Code Quality & Style Rules

**ESLint Configuration:**
- Follow Next.js recommended ESLint rules (`eslint-config-next`)
- Enable React hooks rules to prevent common mistakes
- Enforce TypeScript strict rules (no unused vars, no explicit any)
- Auto-fix on save where possible

**Prettier Formatting:**
- Consistent code formatting across all files
- Use single quotes for strings
- Trailing commas in multi-line objects/arrays
- 2-space indentation
- Max line length: 100 characters

**File and Folder Structure:**
- `app/` - Next.js App Router pages and layouts
- `components/` - Reusable React components (organized by feature or type)
- `lib/` - Utility functions, helpers, and shared logic
- `types/` - TypeScript type definitions and interfaces
- `hooks/` - Custom React hooks
- `api/` - API route handlers (inside `app/api/`)
- `public/` - Static assets (images, fonts, etc.)

**Naming Conventions:**
- **Components:** PascalCase (`PersonaSelector.tsx`, `ProjectCard.tsx`)
- **Files:** kebab-case for non-components (`github-api.ts`, `use-persona.ts`)
- **Functions:** camelCase (`fetchGitHubStats`, `handlePersonaChange`)
- **Constants:** UPPER_SNAKE_CASE (`API_BASE_URL`, `CACHE_DURATION`)
- **Types/Interfaces:** PascalCase with descriptive names (`GitHubStatsResponse`, `PersonaType`)

**Component Organization:**
- One component per file
- Export component at bottom of file (named export preferred)
- Group related components in feature folders
- Separate presentational components from container components

**Documentation Requirements:**
- JSDoc comments for public APIs and complex functions
- Inline comments for non-obvious logic
- README.md in feature folders explaining purpose and usage
- Type definitions serve as documentation (use descriptive names)

**Code Review Standards:**
- No console.log in production code (use proper logging)
- Remove commented-out code before committing
- No TODO comments without GitHub issue reference
- All functions should have clear, single responsibility

---

### Development Workflow Rules

**Git Workflow:**
- Use feature branches for all development work
- Branch naming: `feature/persona-selector`, `fix/api-caching`, `docs/readme-update`
- Commit messages: Use conventional commits format (`feat:`, `fix:`, `docs:`, `test:`, `refactor:`)
- Pull requests required before merging to main
- Squash commits on merge to keep history clean

**Deployment Process:**
- Vercel Git integration: Push to main triggers automatic deployment
- Preview deployments for all pull requests
- Environment variables managed in Vercel dashboard
- Zero-downtime deployments (automatic rollback on failure)

**Environment Variables:**
- `NEXT_PUBLIC_*` prefix for client-side accessible variables
- Keep API keys server-side only (GitHub token, LeetCode API key)
- Use `.env.local` for local development (gitignored)
- Document all required env vars in README

---

### Critical Don't-Miss Rules

**Performance Gotchas:**
- **NEVER** use `'use client'` unnecessarily - it increases bundle size and disables Server Component benefits
- **ALWAYS** use Next.js `<Image>` component, never `<img>` tag (automatic optimization critical for Core Web Vitals)
- **AVOID** importing heavy libraries in Client Components (Three.js, CodeSandbox) - use `next/dynamic` with `ssr: false`
- **REMEMBER** to implement loading states for all async operations (Suspense boundaries, skeleton screens)

**Security Rules:**
- **NEVER** expose API keys in client-side code
- **ALWAYS** proxy external API calls through Next.js API routes (`app/api/`)
- **VALIDATE** all user input (contact form, persona selection)
- **SANITIZE** any user-generated content before rendering

**Accessibility Must-Haves:**
- **ALL** interactive elements must be keyboard accessible (tab navigation)
- **ALL** images must have descriptive alt text
- **ALL** forms must have proper labels and error messages
- **MINIMUM** color contrast ratio 4.5:1 for text (WCAG AA)
- **TEST** with keyboard-only navigation before considering feature complete

**Persona-Specific Implementation:**
- **THREE** distinct content hierarchies required (Recruiter/Client/Developer)
- **SMOOTH** transitions < 300ms when switching personas (no jarring layout shifts)
- **CONTEXT-AWARE** contact forms with different fields per persona
- **PROGRESSIVE** disclosure: Show essentials first, reveal depth on-demand

**API Integration Edge Cases:**
- **CACHE** API responses (24h for GitHub, 1h for real-time data)
- **GRACEFUL** degradation when APIs fail (show cached data with timestamp)
- **RATE LIMITING** handling with exponential backoff
- **LOADING** states must not cause layout shift (reserve space, skeleton screens)

**SEO Non-Negotiables:**
- **METADATA** API for all pages (title, description, Open Graph tags)
- **SEMANTIC** HTML5 (header, nav, main, article, footer)
- **SINGLE** H1 per page with logical heading hierarchy
- **STRUCTURED** data (JSON-LD for Person, WebSite schemas)
- **SITEMAP** auto-generated and submitted to Google Search Console

---

## Architectural Decisions

> **Source:** `_bmad-output/planning-artifacts/architecture.md` (completed 2026-01-28)

These are the 5 core architectural decisions that shape the entire implementation. AI agents must follow these decisions exactly.

### Decision 1: State Management for Persona System

**Technology:** React Context + localStorage  
**Pattern:** `PersonaContext` wrapping app, storing selection in localStorage  
**Files:** `src/contexts/PersonaContext.tsx`, `src/hooks/usePersona.ts`

**Critical Rules:**
- Persona state is CLIENT-SIDE ONLY (`'use client'` directive required)
- Three personas: `'recruiter' | 'client' | 'developer' | null`
- Persist to localStorage on every change
- Load from localStorage on mount (useEffect)
- All pages consume persona context for content prioritization

### Decision 2: API Caching & Real-Time Data Strategy

**Technology:** SWR (stale-while-revalidate) with custom polling intervals  
**Pattern:** Custom hooks (`useGitHubStats`, `useLeetCodeStats`) wrapping SWR

**Critical Rules:**
- **GitHub API:** 5-minute polling (`refreshInterval: 5 * 60 * 1000`)
- **LeetCode API:** 1-hour polling (`refreshInterval: 60 * 60 * 1000`)
- **Deduplication:** 1-minute window (`dedupingInterval: 60 * 1000`)
- **Graceful Degradation:** Show stale data with timestamp when API fails
- **Response Format:** `{ data, status: 'success'|'stale'|'error', timestamp, error? }`

### Decision 3: Database Schema (Prisma + PostgreSQL)

**ORM:** Prisma Client  
**Database:** PostgreSQL (Vercel Postgres or external)  
**Schema:** `prisma/schema.prisma`

**Critical Models:**
- **User:** Admin authentication (id, email, name, passwordHash)
- **Project:** Portfolio projects with persona-specific fields (recruiterHighlight, clientHighlight, developerHighlight)
- **Testimonial:** Client testimonials linked to projects
- **Analytics:** Page views, persona selections, engagement tracking
- **PersonaSelection:** Track persona selection events for analytics

**Critical Rules:**
- Use Prisma Client singleton pattern (`src/lib/db.ts`)
- All database access through Prisma (NEVER raw SQL)
- Use `cuid()` for IDs, not auto-increment integers
- Arrays for techStack and screenshotUrls (PostgreSQL native arrays)

### Decision 4: Error Handling & Resilience Patterns

**Pattern:** Graceful degradation with stale data fallback

**Critical Rules:**
- **API Routes:** Try-catch with cached data fallback (return 200 with `status: 'stale'`)
- **Client Components:** Error boundaries (`src/app/error.tsx`, `src/app/global-error.tsx`)
- **Loading States:** Skeleton screens with reserved space (prevent CLS violations)
- **External APIs:** NEVER throw errors to users - always show cached data or friendly message
- **Logging:** Server-side console.error for debugging, user-friendly messages client-side

### Decision 5: Deployment & Environment Configuration

**Platform:** Vercel (zero-config Next.js deployment)  
**Pattern:** Git-based deployments with automatic HTTPS/SSL

**Critical Environment Variables:**
```bash
DATABASE_URL                    # PostgreSQL connection string
NEXTAUTH_SECRET                 # Generate: openssl rand -base64 32
NEXTAUTH_URL                    # Production URL
GITHUB_TOKEN                    # GitHub API token (5,000 req/hour)
GITHUB_USERNAME                 # Your GitHub username
LEETCODE_USERNAME               # Your LeetCode username
NEXT_PUBLIC_VERCEL_ANALYTICS_ID # Auto-set by Vercel
PLAUSIBLE_DOMAIN                # Your domain for Plausible Analytics
SMTP_HOST, SMTP_PORT, SMTP_USER, SMTP_PASSWORD # Email for contact form
```

**Critical Rules:**
- **NEVER** expose API keys client-side (no `NEXT_PUBLIC_` prefix for secrets)
- All external API calls proxied through Next.js API routes
- Build command: `prisma generate && next build`
- Main branch → production, PRs → preview deployments

---

## Usage Guidelines

**For AI Agents:**

- Read this file before implementing any code
- Follow ALL rules exactly as documented
- When in doubt, prefer the more restrictive option
- Update this file if new patterns emerge

**For Humans:**

- Keep this file lean and focused on agent needs
- Update when technology stack changes
- Review quarterly for outdated rules
- Remove rules that become obvious over time

**Last Updated:** 2026-01-29 (Added Architectural Decisions from completed architecture.md)
