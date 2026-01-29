---
stepsCompleted: ['step-01-validate-prerequisites', 'step-02-design-epics', 'step-03-create-stories', 'step-04-final-validation']
workflowStatus: 'COMPLETE'
inputDocuments:
  - '_bmad-output/planning-artifacts/prd.md'
  - '_bmad-output/planning-artifacts/architecture.md'
  - '_bmad-output/planning-artifacts/ux-design-specification.md'
  - '_bmad-output/analysis/brainstorming-session-2026-01-23.md'
  - '_bmad-output/planning-artifacts/research/domain-developer-portfolios-research-2026-01-23.md'
  - '_bmad-output/planning-artifacts/product-brief-portfolio-2026-01-23.md'
  - '_bmad-output/project-context.md'
---

# bmad - Epic Breakdown

## Overview

This document provides the complete epic and story breakdown for bmad, decomposing the requirements from the PRD, UX Design, and Architecture requirements into implementable stories.

## Requirements Inventory

### Functional Requirements

**FR1:** Visitors can select their persona type (Recruiter, Client, or Developer) from the landing page
**FR2:** The system can display persona-specific content hierarchies based on visitor selection
**FR3:** Recruiters can view skills/experience prominently with availability indicators
**FR4:** Clients can view business impact metrics, ROI case studies, and testimonials prominently
**FR5:** Developers can view technical depth, code quality examples, and architecture decisions prominently
**FR6:** The system can provide a default balanced view if no persona is selected
**FR7:** Visitors can switch between persona views without losing their place on the page
**FR8:** Visitors can browse a gallery of 3-5 featured projects
**FR9:** Visitors can view detailed project information including title, description, technologies used, and role
**FR10:** Visitors can access live demos of projects via embedded iframes or external links
**FR11:** Visitors can interact with code playgrounds (CodeSandbox/StackBlitz) to modify and run project code
**FR12:** Visitors can watch video walkthroughs with technical narration explaining architecture and decisions
**FR13:** Visitors can view performance metrics visualization showing before/after optimization results
**FR14:** Visitors can explore interactive architecture diagrams with clickable layers
**FR15:** Visitors can view project case studies with problem, solution, and business impact sections
**FR16:** Visitors can access GitHub repositories for each project
**FR17:** Visitors can filter or sort projects by technology, type, or other criteria
**FR18:** The system can display real-time GitHub activity including commit history and contribution graphs
**FR19:** The system can display "Last Active" timestamp showing recent coding activity
**FR20:** The system can display a skills matrix with visual proficiency indicators
**FR21:** The system can integrate with GitHub API to fetch and display contribution data
**FR22:** The system can display GitHub-verified badges for active skills
**FR23:** The system can cache API responses to ensure performance when APIs are unavailable
**FR24:** The system can display graceful fallback messages when real-time data is unavailable
**FR25:** Portfolio owner can authenticate securely to access admin panel
**FR26:** Portfolio owner can create new project entries with all required fields
**FR27:** Portfolio owner can edit existing project entries
**FR28:** Portfolio owner can delete project entries
**FR29:** Portfolio owner can upload project images with automatic optimization
**FR30:** Portfolio owner can preview projects in all three persona views before publishing
**FR31:** Portfolio owner can publish projects instantly to the live site
**FR32:** Portfolio owner can manage project visibility (published/draft status)
**FR33:** Portfolio owner can update personal information (bio, skills, experience)
**FR34:** Portfolio owner can manage contact form settings
**FR35:** Visitors can submit contact inquiries via a contact form
**FR36:** The system can customize contact form fields based on selected persona
**FR37:** Visitors can download resume/CV in PDF format
**FR38:** Visitors can view professional bio and background information
**FR39:** Visitors can view comprehensive skills and technology stack information
**FR40:** Visitors can access social media and professional profiles (LinkedIn, GitHub, etc.)
**FR41:** Visitors can book consultations (for client persona)
**FR42:** Visitors can indicate collaboration interest (for developer persona)
**FR43:** The system can track visitor engagement metrics (time on site, pages viewed, interactions)
**FR44:** The system can track persona selection rates
**FR45:** The system can track which projects visitors interact with most
**FR46:** The system can track contact form conversion rates
**FR47:** The system can track Core Web Vitals performance metrics
**FR48:** Portfolio owner can view analytics dashboard with key metrics
**FR49:** The system can generate unique meta tags for each page
**FR50:** The system can generate structured data (JSON-LD) for search engines
**FR51:** The system can generate and maintain an XML sitemap
**FR52:** The system can ensure all pages are crawlable by search engines
**FR53:** The system can provide semantic HTML markup for improved SEO
**FR54:** The system can generate Open Graph tags for social media sharing
**FR55:** The system can render pages with server-side rendering for optimal SEO
**FR56:** The system can pre-render static pages at build time for maximum performance
**FR57:** The system can lazy load images and heavy components to improve initial load time
**FR58:** The system can provide responsive design across all device sizes
**FR59:** The system can ensure all functionality is accessible via keyboard navigation
**FR60:** The system can provide WCAG 2.1 AA compliant accessibility features
**FR61:** The system can handle API failures gracefully without breaking the user experience
**FR62:** The system can cache external API responses to reduce latency
**FR63:** The system can deploy automatically on code changes with zero downtime
**FR64:** The system can serve all traffic over HTTPS
**FR65:** The system can validate and sanitize all user inputs to prevent security vulnerabilities

### NonFunctional Requirements

**NFR1 - Performance (LCP):** Largest Contentful Paint must be < 2.5 seconds
**NFR2 - Performance (INP):** Interaction to Next Paint must be < 200 milliseconds
**NFR3 - Performance (CLS):** Cumulative Layout Shift must be < 0.1
**NFR4 - Performance (Lighthouse):** Performance score must be 90+ / 100
**NFR5 - Accessibility (Lighthouse):** Accessibility score must be 90+ / 100
**NFR6 - Best Practices (Lighthouse):** Best Practices score must be 90+ / 100
**NFR7 - SEO (Lighthouse):** SEO score must be 100 / 100
**NFR8 - Response Time (Page Load):** Initial page load must be < 2 seconds
**NFR9 - Response Time (Transitions):** Page transitions must be < 500 milliseconds
**NFR10 - Response Time (API):** API responses must be < 1 second
**NFR11 - Response Time (Interactive Features):** Code playgrounds must load in < 3 seconds
**NFR12 - Security (HTTPS):** All traffic must be served over HTTPS (TLS 1.3)
**NFR13 - Security (Data Encryption):** Contact form data must be encrypted in transit and at rest
**NFR14 - Security (Client Storage):** No sensitive data stored in client-side storage (localStorage/cookies)
**NFR15 - Security (Authentication):** Admin panel protected by NextAuth.js authentication
**NFR16 - Security (Session Management):** Session management with secure, HTTP-only cookies
**NFR17 - Security (RBAC):** Role-based access control for admin operations
**NFR18 - Security (Input Validation):** All user inputs sanitized to prevent XSS attacks
**NFR19 - Security (Spam Protection):** Contact form protected against spam and injection attacks
**NFR20 - Security (Rate Limiting):** Rate limiting on contact form submissions (max 3 per hour per IP)
**NFR21 - Security (API Keys):** API keys stored securely in environment variables (never in code)
**NFR22 - Security (Server-Side API):** GitHub/LeetCode API calls made server-side to protect credentials
**NFR23 - Security (CSP):** Content Security Policy (CSP) headers to prevent XSS
**NFR24 - Accessibility (Alt Text):** All images must have descriptive alt text
**NFR25 - Accessibility (Color Contrast):** Color contrast ratios must meet minimum standards (4.5:1 for normal text, 3:1 for large text)
**NFR26 - Accessibility (Keyboard Navigation):** All functionality available via keyboard navigation
**NFR27 - Accessibility (Screen Reader):** Screen reader compatible with proper ARIA labels
**NFR28 - Accessibility (No Keyboard Traps):** No keyboard traps or focus issues
**NFR29 - Accessibility (Touch Targets):** Touch targets minimum 44x44px for mobile
**NFR30 - Accessibility (No Hover Dependency):** No hover-dependent functionality (works on touch devices)
**NFR31 - Accessibility (Semantic HTML):** Semantic HTML5 markup required
**NFR32 - Accessibility (Heading Hierarchy):** Proper heading hierarchy (single H1, logical H2-H6)
**NFR33 - Accessibility (Form Labels):** Form labels for all inputs
**NFR34 - Accessibility (Error Messages):** Clear error messages with suggestions
**NFR35 - Integration (GitHub Polling):** GitHub API polling interval: 5 minutes
**NFR36 - Integration (GitHub Caching):** GitHub response caching: 24 hours client-side, 1 hour server-side
**NFR37 - Integration (GitHub Rate Limiting):** GitHub rate limit handling: Exponential backoff on 429 errors
**NFR38 - Integration (GitHub Degradation):** Graceful degradation: Show "Last updated: [timestamp]" if API unavailable
**NFR39 - Integration (LeetCode Polling):** LeetCode API polling interval: 1 hour
**NFR40 - Integration (LeetCode Caching):** LeetCode response caching: 24 hours
**NFR41 - Integration (LeetCode Degradation):** Graceful degradation: Hide section if API unavailable
**NFR42 - Integration (CodeSandbox Enhancement):** Progressive enhancement: Show static code snippets if embed fails
**NFR43 - Integration (CodeSandbox Lazy Loading):** Lazy loading: Load playgrounds on-demand to improve initial page load
**NFR44 - Integration (CodeSandbox Fallback):** Fallback: Link to GitHub repository if playground unavailable
**NFR45 - Deployment (Zero Downtime):** Zero-downtime deployments via Vercel Git integration
**NFR46 - Deployment (Rollback):** Automatic rollback on deployment failures
**NFR47 - Deployment (Uptime):** 99.9% uptime target (Vercel SLA)
**NFR48 - Deployment (Monitoring):** Monitoring and alerts for production errors
**NFR49 - Browser Compatibility (Chrome):** Chrome (latest 2 versions) - Full support
**NFR50 - Browser Compatibility (Firefox):** Firefox (latest 2 versions) - Full support
**NFR51 - Browser Compatibility (Safari):** Safari (latest 2 versions) - Full support (iOS Safari critical for mobile)
**NFR52 - Browser Compatibility (Edge):** Edge (latest 2 versions) - Full support
**NFR53 - Browser Compatibility (Testing):** Automated cross-browser testing via Playwright
**NFR54 - Browser Compatibility (Visual Regression):** Manual visual regression testing before deployment
**NFR55 - Browser Compatibility (Progressive Enhancement):** Core functionality works without JavaScript
**NFR56 - Browser Compatibility (Graceful Degradation):** Modern features fallback to static content

### Additional Requirements

**From Architecture:**

- **Starter Template:** Use `create-next-app` with Next.js 14+ App Router, TypeScript, Tailwind CSS, no src directory, import alias "@/*"
- **Post-Initialization Setup:** Add shadcn/ui, Prisma ORM + PostgreSQL, NextAuth.js, Playwright + Jest testing
- **Additional Dependencies:** SWR for data fetching, Framer Motion for animations, Zod for validation, @vercel/analytics
- **State Management:** React Context + localStorage for persona system (PersonaContext wrapping app)
- **API Caching Strategy:** SWR with 5-minute polling for GitHub, 1-hour polling for LeetCode
- **Database Schema:** Prisma models for User, Project, Testimonial, ProjectAnalytics, PersonaSelection
- **Error Handling:** Graceful degradation with stale data fallback, error boundaries, skeleton screens
- **Deployment Configuration:** Vercel with Git-based deployments, environment variables for API keys
- **File Organization:** App Router structure with app/, components/, lib/, hooks/, types/, public/, prisma/
- **Naming Conventions:** PascalCase for components, kebab-case for files, camelCase for functions, UPPER_SNAKE_CASE for constants
- **Server vs Client Components:** Default to Server Components, use 'use client' only for interactivity, hooks, browser APIs
- **Performance Optimization:** Next.js Image component, lazy loading with next/dynamic, code splitting, streaming with Suspense
- **Styling Approach:** Tailwind CSS utility classes, shadcn/ui components, responsive modifiers (sm:, md:, lg:)
- **Testing Strategy:** Playwright for E2E (cross-browser), Jest for unit tests, Lighthouse CI for performance, axe-core for accessibility
- **TypeScript Configuration:** Strict mode enabled, explicit type annotations, avoid 'any' type, use Zod for runtime validation
- **API Integration:** Proxy all external API calls through Next.js API routes to keep keys secure
- **Metadata API:** Export metadata object or generateMetadata() function for SEO on all pages
- **Structured Data:** JSON-LD schemas for Person, WebSite, CreativeWork
- **Image Optimization:** Use Next.js Image component for automatic optimization (AVIF/WebP), responsive images with srcset
- **Code Splitting:** Dynamic imports for heavy components (CodeSandbox, Three.js) with ssr: false
- **Caching Headers:** Cache-Control headers for static assets (1 year TTL), API responses (24 hours)
- **Real-Time Polling:** Client-side SWR with refreshInterval, not WebSocket
- **Loading States:** Skeleton screens with reserved space to prevent layout shift
- **Form Validation:** Zod runtime validation, client-side validation before submission, specific error messages
- **Git Workflow:** Feature branches, conventional commits (feat:, fix:, docs:, test:, refactor:), squash on merge
- **Environment Variables:** NEXT_PUBLIC_* for client-side, server-side only for API keys, .env.local for local dev
- **Build Command:** `prisma generate && next build`
- **Prisma Patterns:** Singleton pattern for Prisma Client, cuid() for IDs, PostgreSQL native arrays for techStack/screenshotUrls

**From UX Design:**

- **Persona Transformation:** Smooth CSS transitions < 300ms for layout transformations
- **Persona Persistence:** Save persona selection to localStorage, load on mount
- **Context-Aware Forms:** Different form fields per persona (Recruiter: role/company, Client: budget/scope, Developer: collaboration type)
- **Progressive Disclosure:** Show essentials immediately, reveal depth on-demand through expandable sections
- **Responsive Breakpoints:** Mobile < 640px, Tablet 640-1024px, Desktop > 1024px, Large Desktop > 1440px
- **Touch Optimization:** 44x44px minimum touch targets, swipeable project galleries on mobile
- **Mobile-First Design:** Single column stacked layouts on mobile, multi-column on desktop
- **Real-Time Indicators:** Green pulse animation on "Last active" indicator
- **Interactive ROI Calculator:** Slider responds instantly for client persona
- **3D Project Gallery:** Three.js/WebGL visualization on desktop with graceful degradation to 2D on mobile
- **Micro-Interactions:** Hover effects, button animations, smooth scrolling throughout
- **Skeleton Screens:** Reserve space during loading to prevent layout shift
- **Sticky Navigation:** Sticky navigation on scroll with context awareness
- **Back to Top Button:** Prominent button on long pages
- **Clear Visual Hierarchy:** Guide eyes to most important content first per persona
- **Instant Feedback:** All interactions get immediate visual feedback (hover states, click responses)
- **Breadcrumbs:** Clear section headers and breadcrumbs for orientation
- **Action-Oriented CTAs:** "Try the Code", "View Live Demo", "Contact Me" buttons
- **Consistent Navigation:** Same navigation patterns across all persona views
- **No Dead Ends:** Every section has clear next action
- **Accessibility as Excellence:** WCAG AA compliance showcases technical skill and values
- **Dark Mode Support:** Tailwind's dark: variant for dark mode toggle
- **Professional Typography:** Google Fonts (Inter, Roboto, or Outfit) instead of browser defaults
- **Color Palette:** Curated, harmonious colors using HSL, avoid generic colors (plain red, blue, green)
- **Smooth Gradients:** Use subtle gradients for premium feel
- **Semantic HTML5:** header, nav, main, article, aside, footer elements
- **Focus Indicators:** Visible and clear focus indicators for keyboard navigation
- **Skip Navigation Links:** For screen readers to skip to main content
- **ARIA Labels:** Proper ARIA labels where appropriate
- **Error States:** Helpful, specific error states if API fails with timestamps
- **Transparent Limitations:** Graceful degradation messages that admit limitations honestly
- **Real Client Testimonials:** Real names, companies, and specific results (not anonymous)
- **Performance Metrics Display:** Actual Lighthouse scores with timestamps
- **Architecture Diagrams:** Reveal real system design decisions with clickable layers
- **Easter Eggs:** Hidden features in code playgrounds for curious explorers
- **Search Functionality:** For finding specific projects or skills
- **Jump to Links:** In hero section for common goals
- **Clear Completion States:** Form submission confirmation with expected response time
- **Consultation Booking:** For client persona with clear next steps
- **Collaboration Indicators:** Contact form field for collaboration opportunities
- **Leadership Indicators:** Team project showcases, architecture decision documentation
- **Open-Source Contributions:** Showcase with GitHub integration
- **Technical Blog Integration:** RSS feed integration for knowledge sharing
- **Video Walkthroughs:** Technical narration explaining architecture and decisions
- **Performance Metrics Visualization:** Before/after optimization results with charts
- **ROI Case Studies:** Problem → Solution → Business Metrics → Client Testimonial format
- **Business Impact Metrics:** "$2M+ revenue enabled" type metrics for client persona
- **Availability Indicators:** "Available for hire | 3+ years experience | Last active: 4 hours ago"
- **Skills Matrix:** Visual proficiency indicators with GitHub-verified badges
- **Contribution Graphs:** Auto-updating without manual refresh
- **Project Filtering:** Filter/sort by technology, type, or other criteria
- **Multi-Persona Preview:** Admin panel shows preview in all three persona views before publishing
- **Instant Publishing:** Projects go live instantly from admin panel
- **Image Upload Optimization:** Automatic optimization to WebP format
- **Draft Status:** Manage project visibility (published/draft)
- **Personal Information Management:** Update bio, skills, experience from admin panel
- **Analytics Dashboard:** View key metrics (engagement, persona selection, conversion rates)
- **Social Media Links:** LinkedIn, GitHub, Twitter, etc. prominently displayed
- **Resume Download:** PDF format with clear download button
- **Professional Photo:** High-quality professional photo in About section
- **Experience Timeline:** Clear timeline showing career progression
- **Tech Stack Display:** Comprehensive list with proficiency levels
- **Project Thumbnails:** High-quality thumbnails with hover effects
- **Project Screenshots:** Multiple screenshots in carousel or gallery
- **GitHub Repository Links:** Direct links to source code for each project
- **Live Demo Links:** External links to deployed projects
- **Code Playground URLs:** CodeSandbox/StackBlitz embed URLs
- **Video Walkthrough URLs:** Hosted video URLs for technical explanations
- **Performance Scores:** LCP, INP, CLS scores displayed per project
- **Persona-Specific Highlights:** Different highlights for recruiter/client/developer per project
- **ROI Metrics JSON:** Flexible JSON field for evolving ROI data
- **Featured Projects:** Flag to mark projects as featured
- **Project Ordering:** Manual ordering for project display
- **Testimonial Management:** CRUD operations for client testimonials
- **Testimonial Ratings:** 5-star rating system
- **Testimonial Ordering:** Manual ordering for testimonial display
- **Project Analytics Tracking:** Track demo views, code views, time spent per project
- **Persona Analytics:** Track which persona views which projects
- **User Agent Tracking:** Track browser/device information
- **Referrer Tracking:** Track traffic sources
- **Engagement Heatmaps:** Visual representation of user interactions
- **A/B Testing:** Test variations of persona selector placement, demo presentation
- **Conversion Funnel Analysis:** Track visitor journey from landing to contact
- **Email Integration:** SMTP configuration for contact form submissions
- **Spam Protection:** Rate limiting and validation on contact form
- **Expected Response Time:** Display expected response time after form submission
- **Contact Form Context:** Different fields based on persona (role/company for recruiter, budget/timeline for client, collaboration type for developer)
- **XML Sitemap Generation:** Auto-generated and submitted to Google Search Console
- **Robots.txt Configuration:** Properly configured for search engine crawling
- **Canonical URLs:** Prevent duplicate content issues
- **Mobile-Friendly Test:** Responsive design verified on mobile devices
- **Open Graph Tags:** For social media sharing (Facebook, LinkedIn, Twitter)
- **Favicon:** Professional favicon for browser tabs
- **Bundle Analysis:** @next/bundle-analyzer for monitoring bundle size
- **Hot Module Replacement:** Turbopack for instant updates during development
- **ESLint Configuration:** Next.js recommended rules + React hooks rules
- **Prettier Configuration:** Consistent code formatting (single quotes, trailing commas, 2-space indent, 100 char max line)
- **Git Hooks:** Pre-commit hooks for linting and formatting
- **Pull Request Previews:** Automatic preview deployments for all PRs
- **Main Branch Protection:** Require PR approval before merging to main
- **Automatic Rollback:** On deployment failure, automatically rollback to previous version
- **Error Tracking:** Sentry for production error monitoring
- **Uptime Monitoring:** Vercel automatic uptime monitoring
- **Performance Monitoring:** Vercel Analytics for Core Web Vitals tracking
- **Privacy-Friendly Analytics:** Plausible Analytics (GDPR compliant)
- **Content Security Policy:** Prevent XSS attacks with CSP headers
- **Input Sanitization:** Sanitize all user-generated content before rendering
- **Password Hashing:** Secure password hashing for admin authentication
- **Session Expiry:** Automatic session expiry for security
- **CSRF Protection:** Cross-Site Request Forgery protection on forms
- **SQL Injection Prevention:** Prisma ORM prevents SQL injection
- **XSS Prevention:** Input validation and sanitization
- **Clickjacking Prevention:** X-Frame-Options header
- **HTTPS Enforcement:** Redirect all HTTP traffic to HTTPS
- **Secure Cookies:** HTTP-only, secure, SameSite cookies
- **API Rate Limiting:** Prevent API abuse on all endpoints
- **Logging:** Server-side logging for debugging without exposing to users
- **Error Boundaries:** Catch and handle client-side errors gracefully
- **Retry Logic:** Automatic retry with exponential backoff for failed API calls
- **Timeout Handling:** Timeout for slow API responses
- **Offline Detection:** Detect offline state and show appropriate message
- **Service Worker:** Cache static assets for faster repeat visits
- **Progressive Web App:** PWA features for improved mobile experience
- **Web App Manifest:** For "Add to Home Screen" functionality
- **Push Notifications:** (Post-MVP) For engagement and updates
- **Internationalization:** (Post-MVP) Multi-language support
- **Content Versioning:** (Post-MVP) Version control for content changes
- **Advanced Analytics:** (Post-MVP) Predictive analytics, engagement scoring
- **AI Chatbot:** (Post-MVP) AI-powered project Q&A
- **Voice Control:** (Post-MVP) Voice-controlled navigation
- **Blog Platform:** (Post-MVP) Knowledge sharing and SEO
- **Open-Source Showcase:** (Post-MVP) Dedicated section for contributions
- **Community Integration:** (Post-MVP) Developer community features

### FR Coverage Map

**Epic 1: Project Foundation & Deployment Pipeline**
- FR63: System deploys automatically on code changes with zero downtime
- FR64: System serves all traffic over HTTPS
- FR65: System validates and sanitizes all user inputs to prevent security vulnerabilities

**Epic 2: Persona-Based Experience System**
- FR1: Visitors can select their persona type (Recruiter, Client, or Developer) from the landing page
- FR2: System displays persona-specific content hierarchies based on visitor selection
- FR3: Recruiters can view skills/experience prominently with availability indicators
- FR4: Clients can view business impact metrics, ROI case studies, and testimonials prominently
- FR5: Developers can view technical depth, code quality examples, and architecture decisions prominently
- FR6: System provides a default balanced view if no persona is selected
- FR7: Visitors can switch between persona views without losing their place on the page

**Epic 3: Core Pages & SEO Foundation**
- FR37: Visitors can download resume/CV in PDF format
- FR38: Visitors can view professional bio and background information
- FR39: Visitors can view comprehensive skills and technology stack information
- FR40: Visitors can access social media and professional profiles (LinkedIn, GitHub, etc.)
- FR49: System generates unique meta tags for each page
- FR50: System generates structured data (JSON-LD) for search engines
- FR51: System generates and maintains an XML sitemap
- FR52: System ensures all pages are crawlable by search engines
- FR53: System provides semantic HTML markup for improved SEO
- FR54: System generates Open Graph tags for social media sharing
- FR55: System renders pages with server-side rendering for optimal SEO
- FR56: System pre-renders static pages at build time for maximum performance
- FR58: System provides responsive design across all device sizes
- FR59: System ensures all functionality is accessible via keyboard navigation
- FR60: System provides WCAG 2.1 AA compliant accessibility features

**Epic 4: Real-Time Skill Verification**
- FR18: System displays real-time GitHub activity including commit history and contribution graphs
- FR19: System displays "Last Active" timestamp showing recent coding activity
- FR20: System displays a skills matrix with visual proficiency indicators
- FR21: System integrates with GitHub API to fetch and display contribution data
- FR22: System displays GitHub-verified badges for active skills
- FR23: System caches API responses to ensure performance when APIs are unavailable
- FR24: System displays graceful fallback messages when real-time data is unavailable

**Epic 5: Interactive Project Showcase**
- FR8: Visitors can browse a gallery of 3-5 featured projects
- FR9: Visitors can view detailed project information including title, description, technologies used, and role
- FR10: Visitors can access live demos of projects via embedded iframes or external links
- FR11: Visitors can interact with code playgrounds (CodeSandbox/StackBlitz) to modify and run project code
- FR12: Visitors can watch video walkthroughs with technical narration explaining architecture and decisions
- FR13: Visitors can view performance metrics visualization showing before/after optimization results
- FR14: Visitors can explore interactive architecture diagrams with clickable layers
- FR15: Visitors can view project case studies with problem, solution, and business impact sections
- FR16: Visitors can access GitHub repositories for each project
- FR17: Visitors can filter or sort projects by technology, type, or other criteria
- FR57: System lazy loads images and heavy components to improve initial load time

**Epic 6: Visitor Engagement & Conversion**
- FR35: Visitors can submit contact inquiries via a contact form
- FR36: System customizes contact form fields based on selected persona
- FR41: Visitors can book consultations (for client persona)
- FR42: Visitors can indicate collaboration interest (for developer persona)

**Epic 7: Admin Panel & Content Management**
- FR25: Portfolio owner can authenticate securely to access admin panel
- FR26: Portfolio owner can create new project entries with all required fields
- FR27: Portfolio owner can edit existing project entries
- FR28: Portfolio owner can delete project entries
- FR29: Portfolio owner can upload project images with automatic optimization
- FR30: Portfolio owner can preview projects in all three persona views before publishing
- FR31: Portfolio owner can publish projects instantly to the live site
- FR32: Portfolio owner can manage project visibility (published/draft status)
- FR33: Portfolio owner can update personal information (bio, skills, experience)
- FR34: Portfolio owner can manage contact form settings
- FR61: System handles API failures gracefully without breaking the user experience
- FR62: System caches external API responses to reduce latency

**Epic 8: Analytics & Measurement**
- FR43: System tracks visitor engagement metrics (time on site, pages viewed, interactions)
- FR44: System tracks persona selection rates
- FR45: System tracks which projects visitors interact with most
- FR46: System tracks contact form conversion rates
- FR47: System tracks Core Web Vitals performance metrics
- FR48: Portfolio owner can view analytics dashboard with key metrics

## Epic List

### Epic 1: Project Foundation & Deployment Pipeline
Development environment is ready, and the portfolio can be deployed to production with automatic HTTPS and zero-downtime updates. This epic establishes the technical foundation that all subsequent epics will build upon.

**FRs covered:** FR63, FR64, FR65  
**NFRs covered:** NFR12, NFR45-NFR48  
**Key Deliverables:** Next.js 14+ App Router setup, TypeScript configuration, Tailwind CSS + shadcn/ui, Vercel deployment, Git workflow, environment variables, HTTPS/SSL, zero-downtime deployments

---

### Epic 2: Persona-Based Experience System
Visitors can select their persona (Recruiter/Client/Developer) and experience instant, personalized content layouts that respect their unique priorities. This is the core differentiator that makes the portfolio stand out.

**FRs covered:** FR1, FR2, FR3, FR4, FR5, FR6, FR7  
**NFRs covered:** NFR2 (transitions < 500ms), NFR26 (keyboard navigation), NFR55 (progressive enhancement)  
**Key Deliverables:** PersonaContext with React Context API, localStorage persistence, persona selector component, smooth CSS transitions < 300ms, persona-specific content hierarchies, context-aware navigation

---

### Epic 3: Core Pages & SEO Foundation
Visitors can discover the portfolio through search engines, navigate essential pages (Home, About, Skills, Contact), and download resume/CV. This epic ensures discoverability and provides the fundamental information visitors need.

**FRs covered:** FR37, FR38, FR39, FR40, FR49, FR50, FR51, FR52, FR53, FR54, FR55, FR56, FR58, FR59, FR60  
**NFRs covered:** NFR1-NFR11 (Core Web Vitals), NFR7 (SEO score 100), NFR24-NFR34 (accessibility)  
**Key Deliverables:** Home page with persona selector, About page with bio, Skills page with tech stack, Contact page, Resume download, Metadata API for all pages, structured data (JSON-LD), XML sitemap, Open Graph tags, semantic HTML5, responsive design, keyboard navigation, WCAG 2.1 AA compliance

---

### Epic 4: Real-Time Skill Verification
Visitors can see live proof of current, active coding skills through real-time GitHub activity, contribution graphs, and "Last Active" indicators. This builds trust by proving skills are current, not outdated.

**FRs covered:** FR18, FR19, FR20, FR21, FR22, FR23, FR24  
**NFRs covered:** NFR35-NFR38 (GitHub API integration), NFR10 (API response < 1s), NFR61-NFR62 (graceful degradation, caching)  
**Key Deliverables:** GitHub API integration with SWR, 5-minute polling, contribution graphs, "Last Active" timestamp with green pulse indicator, skills matrix with visual proficiency, GitHub-verified badges, graceful degradation with cached data, skeleton screens for loading states

---

### Epic 5: Interactive Project Showcase
Visitors can explore 3-5 featured projects with live demos, code playgrounds, video walkthroughs, performance metrics, and architecture diagrams. This provides hands-on proof of competence through interactive experiences.

**FRs covered:** FR8, FR9, FR10, FR11, FR12, FR13, FR14, FR15, FR16, FR17, FR57  
**NFRs covered:** NFR11 (playgrounds < 3s), NFR42-NFR44 (CodeSandbox integration), NFR57 (lazy loading)  
**Key Deliverables:** Project gallery with 3-5 featured projects, project detail pages with persona-specific highlights, live demo embeds (iframes), CodeSandbox/StackBlitz code playgrounds, video walkthroughs, performance metrics visualization (LCP, INP, CLS), interactive architecture diagrams, project case studies (problem/solution/impact), GitHub repository links, project filtering/sorting, lazy loading for heavy components

---

### Epic 6: Visitor Engagement & Conversion
Visitors can submit context-aware contact inquiries, book consultations, indicate collaboration interest, and access social profiles. This enables frictionless conversion from visitor to contact.

**FRs covered:** FR35, FR36, FR41, FR42  
**NFRs covered:** NFR18-NFR20 (input validation, spam protection, rate limiting), NFR33-NFR34 (form labels, error messages)  
**Key Deliverables:** Context-aware contact form with persona-specific fields (Recruiter: role/company/timeline, Client: budget/scope/goals, Developer: collaboration type), email integration (SMTP), spam protection and rate limiting (max 3/hour per IP), form validation with Zod, consultation booking for clients, collaboration interest for developers, expected response time display, submission confirmation

---

### Epic 7: Admin Panel & Content Management
Portfolio owner can securely authenticate, create/edit/delete projects, upload optimized images, preview in all persona views, and publish instantly. This enables easy content updates without touching code.

**FRs covered:** FR25, FR26, FR27, FR28, FR29, FR30, FR31, FR32, FR33, FR34, FR61, FR62  
**NFRs covered:** NFR15-NFR17 (authentication, session management, RBAC), NFR21-NFR23 (API security)  
**Key Deliverables:** NextAuth.js authentication, Prisma database schema (User, Project, Testimonial, Analytics models), admin dashboard, project CRUD operations (create/read/update/delete), image upload with automatic optimization (WebP/AVIF), multi-persona preview before publishing, instant publishing workflow, draft/published status management, personal information management (bio, skills, experience), contact form settings, error handling with graceful degradation

---

### Epic 8: Analytics & Measurement
Portfolio owner can track visitor engagement, persona selection rates, project interactions, conversion rates, and Core Web Vitals performance. This enables data-driven optimization and iteration.

**FRs covered:** FR43, FR44, FR45, FR46, FR47, FR48  
**NFRs covered:** NFR47-NFR48 (Core Web Vitals tracking, monitoring and alerts)  
**Key Deliverables:** Vercel Analytics integration for Core Web Vitals, Plausible Analytics for privacy-friendly tracking (GDPR compliant), persona selection tracking (PersonaSelection model), project interaction tracking (ProjectAnalytics model), engagement metrics (time on site, pages viewed, interactions), conversion funnel analysis, analytics dashboard for portfolio owner, engagement heatmaps, A/B testing capability, Sentry for error tracking

---

## Epic 1: Project Foundation & Deployment Pipeline

Development environment is ready, and the portfolio can be deployed to production with automatic HTTPS and zero-downtime updates. This epic establishes the technical foundation that all subsequent epics will build upon.

### Story 1.1: Initialize Next.js Project with TypeScript & Tailwind

As a developer,
I want to initialize a Next.js 14+ project with TypeScript and Tailwind CSS configured,
So that I have a modern, type-safe foundation for building the portfolio.

**Acceptance Criteria:**

**Given** I am starting a new portfolio project  
**When** I run the project initialization command  
**Then** a Next.js 14+ project is created with App Router (not Pages Router)  
**And** TypeScript is configured with strict mode enabled  
**And** Tailwind CSS is installed and configured  
**And** ESLint and Prettier are configured with Next.js recommended rules  
**And** the project uses the import alias "@/*" for absolute imports  
**And** no `src/` directory is created (App Router uses `app/` directly)  
**And** the development server runs successfully on `npm run dev`  
**And** a basic "Hello World" page renders at the root route

**Technical Requirements:**
- Next.js 14+ with App Router
- TypeScript with strict mode (`tsconfig.json`)
- Tailwind CSS with default configuration
- ESLint + Prettier with single quotes, trailing commas, 2-space indent
- Import alias: `@/*` maps to `./*`

---

### Story 1.2: Configure shadcn/ui Component Library

As a developer,
I want to set up shadcn/ui component library with Tailwind CSS,
So that I can use pre-built, accessible UI components throughout the portfolio.

**Acceptance Criteria:**

**Given** the Next.js project is initialized with Tailwind CSS  
**When** I configure shadcn/ui  
**Then** the shadcn/ui CLI is installed and initialized  
**And** the `components.json` configuration file is created  
**And** the `components/ui/` directory structure is set up  
**And** Tailwind CSS configuration is updated with shadcn/ui theme variables  
**And** at least one test component (e.g., Button) is installed and renders correctly  
**And** the component uses Radix UI primitives for accessibility  
**And** dark mode support is configured via Tailwind's `dark:` variant

**Technical Requirements:**
- shadcn/ui initialized with `npx shadcn-ui@latest init`
- Tailwind config includes shadcn/ui theme tokens
- Install at least Button component as proof of concept
- Verify component renders with proper styling

---

### Story 1.3: Set Up Prisma ORM with PostgreSQL

As a developer,
I want to configure Prisma ORM with PostgreSQL database,
So that I can manage database schema and perform type-safe database operations.

**Acceptance Criteria:**

**Given** the Next.js project is set up  
**When** I configure Prisma ORM  
**Then** Prisma is installed as a dependency  
**And** Prisma is initialized with PostgreSQL provider  
**And** the `prisma/schema.prisma` file is created with PostgreSQL datasource  
**And** a Prisma Client singleton pattern is implemented in `lib/db.ts`  
**And** environment variable `DATABASE_URL` is documented in `.env.example`  
**And** `.env.local` is added to `.gitignore`  
**And** `prisma generate` command runs successfully  
**And** a basic test connection to the database succeeds

**Technical Requirements:**
- Prisma installed: `npm install prisma @prisma/client`
- `prisma/schema.prisma` with PostgreSQL provider
- Prisma Client singleton in `lib/db.ts` to prevent connection issues
- Environment variable: `DATABASE_URL`
- Add `prisma generate` to build command

---

### Story 1.4: Configure Vercel Deployment with Environment Variables

As a portfolio owner,
I want to deploy the portfolio to Vercel with automatic HTTPS and environment variables configured,
So that the site is accessible online with secure connections and proper configuration.

**Acceptance Criteria:**

**Given** the Next.js project is ready for deployment  
**When** I deploy to Vercel  
**Then** the project is connected to a Git repository (GitHub)  
**And** Vercel deployment is configured for automatic deployments on push to main  
**And** preview deployments are enabled for all pull requests  
**And** environment variables are configured in Vercel dashboard (`DATABASE_URL`, `NEXTAUTH_SECRET`, etc.)  
**And** the production site is accessible via HTTPS with automatic SSL certificate  
**And** the build command includes `prisma generate && next build`  
**And** zero-downtime deployments are confirmed (new version replaces old atomically)  
**And** automatic rollback is configured for failed deployments

**Technical Requirements:**
- Vercel project linked to Git repository
- Environment variables set in Vercel dashboard
- Build command: `prisma generate && next build`
- Automatic HTTPS/SSL via Vercel
- Preview deployments for PRs
- Main branch → production deployment

**Fulfills:** FR63 (automatic deployment), FR64 (HTTPS), NFR12 (TLS 1.3), NFR45-NFR48 (deployment requirements)

---

### Story 1.5: Implement Git Workflow & Branch Protection

As a development team,
I want to establish a Git workflow with branch protection and conventional commits,
So that code quality is maintained and deployment is controlled.

**Acceptance Criteria:**

**Given** the project repository is set up on GitHub  
**When** I configure Git workflow and branch protection  
**Then** the main branch has protection rules enabled  
**And** pull requests are required before merging to main  
**And** at least one approval is required for PRs  
**And** branch naming convention is documented (feature/, fix/, docs/, test/, refactor/)  
**And** conventional commit format is documented (feat:, fix:, docs:, test:, refactor:)  
**And** commits are squashed on merge to keep history clean  
**And** a `.gitignore` file excludes node_modules, .env.local, .next, and other build artifacts  
**And** a README.md documents the setup process and environment variables

**Technical Requirements:**
- GitHub branch protection on `main`
- PR required before merge
- Conventional commits format documented
- Squash commits on merge
- `.gitignore` properly configured
- README.md with setup instructions

**Fulfills:** FR65 (input validation through code review), NFR46 (rollback capability)
## Epic 2: Persona-Based Experience System

Visitors can select their persona (Recruiter/Client/Developer) and experience instant, personalized content layouts that respect their unique priorities. This is the core differentiator that makes the portfolio stand out.

### Story 2.1: Create PersonaContext with React Context API

As a developer,
I want to implement a PersonaContext using React Context API,
So that persona selection state can be shared across all components.

**Acceptance Criteria:**

**Given** the Next.js project is set up  
**When** I create the PersonaContext  
**Then** a `PersonaContext` is created in `contexts/PersonaContext.tsx` with `'use client'` directive  
**And** the context provides `persona` state (type: `'recruiter' | 'client' | 'developer' | null`)  
**And** the context provides `setPersona` function to update persona selection  
**And** the context provider wraps the entire application in `app/layout.tsx`  
**And** a custom hook `usePersona()` is created in `hooks/usePersona.ts` for easy access  
**And** TypeScript types are defined for PersonaType in `types/persona.ts`

**Technical Requirements:**
- Client Component with `'use client'` directive
- React Context API for state management
- TypeScript types: `PersonaType = 'recruiter' | 'client' | 'developer' | null`
- Custom hook for consuming context
- Provider wraps app in root layout

**Fulfills:** FR1, FR2

---

### Story 2.2: Implement localStorage Persistence for Persona Selection

As a visitor,
I want my persona selection to be remembered across page visits,
So that I don't have to re-select my persona every time I visit the portfolio.

**Acceptance Criteria:**

**Given** the PersonaContext is implemented  
**When** a visitor selects a persona  
**Then** the selection is saved to localStorage with key `'bmad-persona'`  
**And** on page load, the persona is read from localStorage and set as initial state  
**And** if no persona is saved, the default state is `null` (balanced view)  
**And** the persona persists across page refreshes and browser sessions  
**And** clearing localStorage resets to default balanced view

**Technical Requirements:**
- Use `useEffect` to sync persona state with localStorage
- Handle SSR safely (check `typeof window !== 'undefined'`)
- localStorage key: `'bmad-persona'`
- Default value: `null` (balanced view)

**Fulfills:** FR6, FR7

---

### Story 2.3: Build Persona Selector Component with Smooth Transitions

As a visitor,
I want to see a clean persona selector on the landing page,
So that I can choose my persona and see the layout transform smoothly.

**Acceptance Criteria:**

**Given** the PersonaContext is available  
**When** I view the landing page  
**Then** a persona selector component is displayed prominently  
**And** three buttons are shown: "Recruiter", "Client", "Developer"  
**And** clicking a button updates the persona context  
**And** the selected button has visual feedback (highlighted state)  
**And** the layout transformation happens with smooth CSS transitions < 300ms  
**And** the component is keyboard accessible (tab navigation, enter to select)  
**And** the component uses shadcn/ui Button components for consistency

**Technical Requirements:**
- Client Component (`'use client'`)
- shadcn/ui Button components
- CSS transitions < 300ms using Tailwind transition utilities
- Keyboard accessible (tab, enter, space)
- Visual feedback for selected state
- Responsive design (mobile: stacked buttons, desktop: inline buttons)

**Fulfills:** FR1, NFR2 (transitions < 500ms), NFR26 (keyboard navigation)

---

### Story 2.4: Implement Persona-Specific Content Hierarchies

As a visitor,
I want to see content prioritized based on my selected persona,
So that the most relevant information for my needs is prominently displayed.

**Acceptance Criteria:**

**Given** a persona is selected  
**When** I view the home page  
**Then** content is reordered based on persona priorities  
**And** for Recruiter persona: Skills/Experience section appears first, followed by Projects, then Contact  
**And** for Client persona: Business Impact/ROI section appears first, followed by Case Studies, then Contact  
**And** for Developer persona: Technical Depth/Architecture section appears first, followed by Code Examples, then GitHub  
**And** for null persona (balanced view): All sections appear in default order with equal prominence  
**And** content sections use conditional rendering based on `usePersona()` hook  
**And** transitions between layouts are smooth with no layout shift (CLS < 0.1)

**Technical Requirements:**
- Conditional rendering based on persona state
- Smooth CSS transitions for reordering
- No cumulative layout shift (reserve space for content)
- Use Tailwind's `order-*` utilities for flex/grid reordering
- Server Components for static content, Client Components for dynamic reordering

**Fulfills:** FR2, FR3, FR4, FR5, NFR3 (CLS < 0.1)

---

### Story 2.5: Add Persona Switcher in Navigation

As a visitor,
I want to switch personas without losing my place on the page,
So that I can compare how different personas view the same content.

**Acceptance Criteria:**

**Given** I am viewing the portfolio with a persona selected  
**When** I click the persona switcher in the navigation  
**Then** a dropdown or toggle appears with all three persona options  
**And** clicking a different persona updates the context immediately  
**And** the page content updates without scrolling to top  
**And** my scroll position is maintained  
**And** the transition is smooth < 300ms  
**And** the switcher is accessible via keyboard (tab, arrow keys, enter)  
**And** the current persona is visually indicated in the switcher

**Technical Requirements:**
- shadcn/ui DropdownMenu or Select component
- Preserve scroll position on persona change
- Smooth transitions < 300ms
- Keyboard accessible (ARIA labels, keyboard navigation)
- Visual indicator for current persona
- Sticky navigation with persona switcher always visible

**Fulfills:** FR7, NFR2 (transitions < 500ms), NFR26 (keyboard navigation), NFR55 (progressive enhancement)

---

## Epic 3: Core Pages & SEO Foundation

Visitors can discover the portfolio through search engines, navigate essential pages (Home, About, Skills, Contact), and download resume/CV. This epic ensures discoverability and provides the fundamental information visitors need.

### Story 3.1: Create Home Page with Metadata and Structured Data

As a visitor,
I want to land on a compelling home page that loads quickly and is optimized for search engines,
So that I can immediately understand the portfolio owner's value proposition and find the site via Google.

**Acceptance Criteria:**

**Given** I navigate to the portfolio URL  
**When** the home page loads  
**Then** a hero section displays with professional photo, name, tagline, and persona selector  
**And** the page uses Server Components for optimal performance  
**And** metadata is exported with title, description, and Open Graph tags  
**And** structured data (JSON-LD) is included for Person schema  
**And** the page is server-side rendered for SEO  
**And** semantic HTML5 is used (header, main, section elements)  
**And** the page loads in < 2 seconds (LCP < 2.5s)  
**And** all images use Next.js Image component with proper alt text

**Technical Requirements:**
- Server Component (no `'use client'` unless needed)
- Export `metadata` object with title, description, Open Graph tags
- JSON-LD structured data for Person schema
- Semantic HTML5 (header, main, section, article)
- Next.js Image component for all images
- Responsive design (mobile-first)
- LCP < 2.5 seconds

**Fulfills:** FR38, FR49, FR50, FR53, FR54, FR55, FR56, NFR1 (LCP < 2.5s), NFR7 (SEO score 100), NFR31 (semantic HTML)

---

### Story 3.2: Build About Page with Bio and Experience Timeline

As a visitor,
I want to read a professional bio and view career progression,
So that I can understand the portfolio owner's background and expertise.

**Acceptance Criteria:**

**Given** I navigate to the About page  
**When** the page loads  
**Then** a professional bio is displayed with high-quality photo  
**And** an experience timeline shows career progression with dates, companies, and roles  
**And** the page uses Server Components for performance  
**And** metadata is exported with unique title and description  
**And** structured data (JSON-LD) is included for Person schema  
**And** the page is responsive across all device sizes  
**And** semantic HTML5 is used (article, section, time elements)  
**And** the page is keyboard accessible with proper heading hierarchy (H1 → H2 → H3)

**Acceptance Criteria:**

**Given** I navigate to the About page  
**When** the page loads  
**Then** a professional bio is displayed with high-quality photo  
**And** an experience timeline shows career progression with dates, companies, and roles  
**And** the page uses Server Components for performance  
**And** metadata is exported with unique title and description  
**And** structured data (JSON-LD) is included for Person schema  
**And** the page is responsive across all device sizes  
**And** semantic HTML5 is used (article, section, time elements)  
**And** the page is keyboard accessible with proper heading hierarchy (H1 → H2 → H3)

**Technical Requirements:**
- Server Component
- Export `metadata` object
- JSON-LD for Person schema
- Semantic HTML5 (article, section, time)
- Next.js Image component for photo
- Responsive timeline component
- Proper heading hierarchy (single H1, logical H2-H6)

**Fulfills:** FR38, FR49, FR50, FR53, FR55, NFR7 (SEO score 100), NFR31-NFR32 (semantic HTML, heading hierarchy)

---

### Story 3.3: Create Skills Page with Tech Stack and Proficiency Indicators

As a visitor,
I want to view a comprehensive list of skills and technologies,
So that I can quickly assess technical competencies.

**Acceptance Criteria:**

**Given** I navigate to the Skills page  
**When** the page loads  
**Then** a skills matrix is displayed with categories (Frontend, Backend, DevOps, etc.)  
**And** each skill has a visual proficiency indicator (beginner, intermediate, advanced, expert)  
**And** skills are grouped by category for easy scanning  
**And** the page uses Server Components for performance  
**And** metadata is exported with unique title and description  
**And** the page is responsive with mobile-friendly layout  
**And** semantic HTML5 is used (section, ul, li elements)  
**And** the page is keyboard accessible

**Technical Requirements:**
- Server Component
- Export `metadata` object
- Visual proficiency indicators (progress bars or badges)
- Grouped by category (Frontend, Backend, DevOps, Tools, etc.)
- Responsive grid layout (1 column mobile, 2-3 columns desktop)
- Semantic HTML5 (section, ul, li)
- Keyboard accessible

**Fulfills:** FR39, FR49, FR53, FR55, FR58, NFR7 (SEO score 100), NFR31 (semantic HTML)

---

### Story 3.4: Implement Resume Download Functionality

As a visitor,
I want to download the portfolio owner's resume in PDF format,
So that I can review credentials offline or share with colleagues.

**Acceptance Criteria:**

**Given** I am viewing the portfolio  
**When** I click the "Download Resume" button  
**Then** a PDF file is downloaded to my device  
**And** the PDF is stored in the `public/` directory  
**And** the download button is prominently displayed on the Home and About pages  
**And** the button uses shadcn/ui Button component with download icon  
**And** the button is keyboard accessible  
**And** the PDF filename is descriptive (e.g., `Sasa-Portfolio-Resume-2026.pdf`)  
**And** the download triggers immediately without opening a new tab

**Technical Requirements:**
- PDF file stored in `public/resume/` directory
- Download link: `<a href="/resume/Sasa-Portfolio-Resume-2026.pdf" download>`
- shadcn/ui Button component with download icon
- Keyboard accessible
- Descriptive filename
- Prominent placement on Home and About pages

**Fulfills:** FR37

---

### Story 3.5: Add Social Media Links and Contact Information

As a visitor,
I want to access social media profiles and professional networks,
So that I can connect on multiple platforms.

**Acceptance Criteria:**

**Given** I am viewing the portfolio  
**When** I look for social media links  
**Then** links to LinkedIn, GitHub, Twitter, and email are prominently displayed  
**And** links are in the footer on all pages  
**And** links are also in the Contact page header  
**And** each link has an appropriate icon (using lucide-react or similar)  
**And** links open in a new tab with `rel="noopener noreferrer"` for security  
**And** links are keyboard accessible  
**And** hover states provide visual feedback

**Technical Requirements:**
- Social links in footer (all pages) and Contact page
- Icons from lucide-react or similar library
- `target="_blank" rel="noopener noreferrer"` for external links
- Keyboard accessible
- Hover states with Tailwind utilities
- ARIA labels for accessibility

**Fulfills:** FR40, NFR26 (keyboard navigation), NFR31 (semantic HTML)

---

### Story 3.6: Generate XML Sitemap and Robots.txt

As a search engine crawler,
I want to discover all pages via an XML sitemap,
So that the portfolio is properly indexed.

**Acceptance Criteria:**

**Given** the portfolio is deployed  
**When** a search engine crawler accesses `/sitemap.xml`  
**Then** an XML sitemap is returned with all public pages  
**And** the sitemap includes Home, About, Skills, Contact, and Projects pages  
**And** each URL has a `<lastmod>` timestamp  
**And** each URL has a `<priority>` value (Home: 1.0, others: 0.8)  
**And** a `robots.txt` file exists at `/robots.txt`  
**And** `robots.txt` allows all crawlers and references the sitemap  
**And** the sitemap is automatically generated using Next.js `sitemap.ts`

**Technical Requirements:**
- Create `app/sitemap.ts` to generate sitemap dynamically
- Create `app/robots.ts` to generate robots.txt
- Include all public pages in sitemap
- Set appropriate priority and lastmod values
- Reference sitemap in robots.txt

**Fulfills:** FR51, FR52, NFR7 (SEO score 100)

---

### Story 3.7: Implement Responsive Design and Accessibility

As a visitor using any device or assistive technology,
I want the portfolio to be fully accessible and responsive,
So that I can navigate and consume content regardless of my device or abilities.

**Acceptance Criteria:**

**Given** I access the portfolio from any device  
**When** I interact with the site  
**Then** the layout is responsive across all breakpoints (mobile < 640px, tablet 640-1024px, desktop > 1024px)  
**And** all interactive elements are keyboard accessible (tab, enter, space, arrow keys)  
**And** all images have descriptive alt text  
**And** color contrast ratios meet WCAG AA standards (4.5:1 for text, 3:1 for large text)  
**And** focus indicators are visible and clear  
**And** skip navigation links are provided for screen readers  
**And** ARIA labels are used where appropriate  
**And** semantic HTML5 is used throughout  
**And** touch targets are minimum 44x44px on mobile  
**And** no hover-dependent functionality (works on touch devices)

**Technical Requirements:**
- Tailwind responsive modifiers (sm:, md:, lg:, xl:)
- Keyboard navigation for all interactive elements
- Descriptive alt text for all images
- Color contrast checker (4.5:1 minimum)
- Visible focus indicators
- Skip navigation links (`<a href="#main-content">Skip to content</a>`)
- ARIA labels where needed
- Semantic HTML5 (header, nav, main, footer, article, section)
- Touch targets 44x44px minimum
- No hover-only functionality

**Fulfills:** FR58, FR59, FR60, NFR5 (Accessibility score 90+), NFR24-NFR34 (all accessibility requirements)

---

## Epic 4: Real-Time Skill Verification

Visitors can see live proof of current, active coding skills through real-time GitHub activity, contribution graphs, and "Last Active" indicators. This builds trust by proving skills are current, not outdated.

### Story 4.1: Create GitHub API Proxy Route

As a developer,
I want to create a Next.js API route that proxies GitHub API calls,
So that API keys remain secure on the server and rate limits are properly managed.

**Acceptance Criteria:**

**Given** the Next.js project is set up  
**When** I create the GitHub API proxy  
**Then** an API route is created at `app/api/github/stats/route.ts`  
**And** the route fetches data from GitHub API using server-side `GITHUB_TOKEN`  
**And** the route returns user profile, contribution stats, and recent activity  
**And** the route implements caching with 1-hour TTL  
**And** the route handles rate limiting with exponential backoff  
**And** the route returns graceful error responses if GitHub API fails  
**And** the route is protected from CORS issues  
**And** environment variable `GITHUB_TOKEN` is documented in `.env.example`

**Technical Requirements:**
- API Route: `app/api/github/stats/route.ts`
- Server-side GitHub API calls with `GITHUB_TOKEN`
- Caching with Next.js `revalidate` or custom cache (1-hour TTL)
- Exponential backoff on 429 errors
- Graceful error handling (return cached data or friendly error)
- Environment variable: `GITHUB_TOKEN`, `GITHUB_USERNAME`

**Fulfills:** FR21, NFR22 (server-side API calls), NFR21 (API keys in env vars), NFR37 (rate limiting)

---

### Story 4.2: Implement SWR Hook for GitHub Data Fetching

As a developer,
I want to create a custom SWR hook for fetching GitHub data,
So that data is automatically refreshed and cached on the client side.

**Acceptance Criteria:**

**Given** the GitHub API proxy route exists  
**When** I create the `useGitHubStats` hook  
**Then** a custom hook is created in `hooks/useGitHubStats.ts`  
**And** the hook uses SWR to fetch data from `/api/github/stats`  
**And** the hook polls every 5 minutes (`refreshInterval: 5 * 60 * 1000`)  
**And** the hook deduplicates requests within 1 minute  
**And** the hook returns `{ data, status, timestamp, error }` object  
**And** the hook handles loading, success, stale, and error states  
**And** the hook provides graceful degradation (shows stale data with timestamp if API fails)

**Technical Requirements:**
- Custom hook: `hooks/useGitHubStats.ts`
- SWR with `refreshInterval: 5 * 60 * 1000` (5 minutes)
- Deduplication: `dedupingInterval: 60 * 1000` (1 minute)
- Return type: `{ data, status: 'success'|'stale'|'error', timestamp, error? }`
- Handle all states: loading, success, stale, error

**Fulfills:** FR21, FR23, FR24, NFR35 (5-minute polling), NFR36 (caching), NFR38 (graceful degradation)

---

### Story 4.3: Display GitHub Contribution Graph

As a visitor,
I want to see a visual contribution graph showing recent coding activity,
So that I can verify the portfolio owner is actively coding.

**Acceptance Criteria:**

**Given** GitHub data is being fetched  
**When** I view the Skills or Home page  
**Then** a contribution graph is displayed showing the last 12 months of activity  
**And** the graph uses a heatmap visualization (green squares like GitHub)  
**And** hovering over a square shows the date and contribution count  
**And** the graph is responsive (scrollable on mobile, full width on desktop)  
**And** the graph shows a loading skeleton while data is being fetched  
**And** if data is unavailable, a message displays: "Last updated: [timestamp]"  
**And** the component is accessible with proper ARIA labels

**Technical Requirements:**
- Use `useGitHubStats` hook
- Heatmap visualization (consider `react-calendar-heatmap` or custom component)
- Responsive design (scrollable on mobile)
- Loading skeleton with reserved space (prevent CLS)
- Graceful degradation with timestamp
- ARIA labels for accessibility

**Fulfills:** FR18, FR21, FR23, FR24, NFR38 (graceful degradation)

---

### Story 4.4: Add "Last Active" Timestamp with Pulse Indicator

As a recruiter,
I want to see when the portfolio owner was last active on GitHub,
So that I can verify they are currently coding, not just showcasing old work.

**Acceptance Criteria:**

**Given** GitHub data is being fetched  
**When** I view the Home page  
**Then** a "Last Active" indicator is displayed prominently  
**And** the indicator shows time since last commit (e.g., "Last active: 4 hours ago")  
**And** if activity is within 24 hours, a green pulse animation is shown  
**And** if activity is within 7 days, a yellow indicator is shown  
**And** if activity is older than 7 days, a gray indicator is shown  
**And** the timestamp updates automatically every 5 minutes  
**And** if data is unavailable, it shows "Last updated: [cached timestamp]"

**Technical Requirements:**
- Use `useGitHubStats` hook
- Calculate time since last commit
- Green pulse animation (CSS keyframes) if < 24 hours
- Yellow indicator if < 7 days
- Gray indicator if > 7 days
- Auto-update every 5 minutes via SWR
- Graceful degradation with cached timestamp

**Fulfills:** FR19, FR24, NFR38 (graceful degradation)

---

### Story 4.5: Create Skills Matrix with GitHub-Verified Badges

As a visitor,
I want to see which skills are actively used based on GitHub activity,
So that I can trust the skill claims are current.

**Acceptance Criteria:**

**Given** GitHub data includes language statistics  
**When** I view the Skills page  
**Then** each skill in the skills matrix has a verification badge  
**And** skills actively used in recent GitHub repos show a "GitHub Verified" badge  
**And** the badge is green with a checkmark icon  
**And** hovering over the badge shows: "Actively used in recent projects"  
**And** skills without recent GitHub activity show no badge  
**And** the verification is based on language statistics from GitHub API  
**And** the component handles missing data gracefully

**Technical Requirements:**
- Use `useGitHubStats` hook to get language statistics
- Match GitHub languages to skills matrix
- Display "GitHub Verified" badge for active skills
- Green badge with checkmark icon (lucide-react)
- Tooltip on hover with explanation
- Graceful handling of missing data

**Fulfills:** FR20, FR22, FR23, FR24

---

### Story 4.6: Implement Skeleton Screens for Loading States

As a visitor,
I want to see skeleton screens while GitHub data loads,
So that the page doesn't jump around when data appears (preventing layout shift).

**Acceptance Criteria:**

**Given** GitHub data is being fetched  
**When** the page loads  
**Then** skeleton screens are displayed in place of GitHub components  
**And** skeletons reserve the exact space that real content will occupy  
**And** skeletons use subtle pulse animations to indicate loading  
**And** no layout shift occurs when real data replaces skeletons (CLS < 0.1)  
**And** skeletons match the shape of real components (graph, badges, timestamps)  
**And** skeletons are accessible (ARIA labels: "Loading GitHub data")

**Technical Requirements:**
- Skeleton components for contribution graph, "Last Active", badges
- Reserve exact space to prevent layout shift
- Pulse animation using Tailwind `animate-pulse`
- CLS < 0.1 (no cumulative layout shift)
- ARIA labels for accessibility

**Fulfills:** NFR3 (CLS < 0.1), NFR61 (graceful UX during loading)

---

## Epic 5: Interactive Project Showcase

Visitors can explore 3-5 featured projects with live demos, code playgrounds, video walkthroughs, performance metrics, and architecture diagrams. This provides hands-on proof of competence through interactive experiences.

### Story 5.1: Create Project Database Schema

As a developer,
I want to define the Project model in Prisma schema,
So that project data can be stored and retrieved from the database.

**Acceptance Criteria:**

**Given** Prisma is configured  
**When** I define the Project model  
**Then** the `prisma/schema.prisma` file includes a Project model  
**And** the model has fields: id (cuid), title, description, techStack (String[]), role, liveDemoUrl, githubUrl, codePlaygroundUrl, videoWalkthrough Url, performanceMetrics (Json), architectureDiagramUrl, caseStudy (Json), recruiterHighlight, clientHighlight, developerHighlight, thumbnailUrl, screenshotUrls (String[]), isFeatured, isPublished, displayOrder, createdAt, updatedAt  
**And** the model uses `cuid()` for IDs  
**And** the model uses PostgreSQL native arrays for techStack and screenshotUrls  
**And** the model uses Json type for performanceMetrics and caseStudy  
**And** `prisma migrate dev` creates the database table successfully  
**And** `prisma generate` generates TypeScript types

**Technical Requirements:**
- Prisma model: Project
- Fields: id, title, description, techStack[], role, URLs, metrics, highlights, flags, timestamps
- Use `cuid()` for IDs
- PostgreSQL arrays for techStack, screenshotUrls
- Json type for performanceMetrics, caseStudy
- Run `prisma migrate dev` to create table

**Fulfills:** FR8, FR9, FR26, FR27, FR28

---

### Story 5.2: Build Project Gallery Component

As a visitor,
I want to browse a gallery of featured projects,
So that I can explore the portfolio owner's work.

**Acceptance Criteria:**

**Given** projects exist in the database  
**When** I view the Projects page or Home page  
**Then** a project gallery displays 3-5 featured projects  
**And** each project card shows thumbnail, title, tech stack, and brief description  
**And** project cards are responsive (1 column mobile, 2-3 columns desktop)  
**And** clicking a card navigates to the project detail page  
**And** cards have hover effects (scale, shadow)  
**And** the gallery uses Next.js Image component for thumbnails  
**And** the gallery is keyboard accessible (tab navigation, enter to open)  
**And** the gallery lazy loads images for performance

**Technical Requirements:**
- Fetch featured projects from database (isPublished=true, isFeatured=true)
- Server Component for initial render
- Responsive grid layout (1 column mobile, 2-3 columns desktop)
- Next.js Image component for thumbnails
- Hover effects with Tailwind utilities
- Keyboard accessible
- Lazy loading for images

**Fulfills:** FR8, FR9, FR57 (lazy loading), NFR1 (LCP < 2.5s)

---

### Story 5.3: Create Project Detail Page with Persona-Specific Highlights

As a visitor,
I want to view detailed project information tailored to my persona,
So that I see the most relevant aspects of the project for my needs.

**Acceptance Criteria:**

**Given** I click on a project card  
**When** the project detail page loads  
**Then** the page displays title, description, tech stack, role, and screenshots  
**And** if Recruiter persona: recruiterHighlight is shown prominently (e.g., "Built in 8 weeks, deployed to 10K users")  
**And** if Client persona: clientHighlight is shown prominently (e.g., "Increased conversion rate by 40%")  
**And** if Developer persona: developerHighlight is shown prominently (e.g., "Microservices architecture with Redis caching")  
**And** if no persona selected: all highlights are shown equally  
**And** the page uses Server Components for performance  
**And** metadata is generated dynamically with project title and description  
**And** the page is responsive and accessible

**Technical Requirements:**
- Dynamic route: `app/projects/[id]/page.tsx`
- Fetch project by ID from database
- Conditional rendering based on persona context
- Server Component with dynamic metadata (`generateMetadata`)
- Responsive layout
- Keyboard accessible

**Fulfills:** FR9, FR3, FR4, FR5, FR49 (unique meta tags), FR55 (SSR)

---

### Story 5.4: Embed Live Demos with iframes

As a visitor,
I want to interact with live demos of projects,
So that I can experience the functionality firsthand.

**Acceptance Criteria:**

**Given** a project has a liveDemoUrl  
**When** I view the project detail page  
**Then** a "View Live Demo" button is prominently displayed  
**And** clicking the button opens the demo in an iframe modal  
**And** the iframe is responsive and fills the modal  
**And** the modal has a close button (X) and can be closed with Escape key  
**And** the modal is keyboard accessible (tab trap, focus management)  
**And** if liveDemoUrl is null, the button is hidden  
**And** the iframe uses `loading="lazy"` for performance

**Technical Requirements:**
- shadcn/ui Dialog component for modal
- iframe with `loading="lazy"`
- Responsive iframe (aspect-ratio or full modal)
- Close button and Escape key handler
- Keyboard accessible (focus trap)
- Conditional rendering if liveDemoUrl exists

**Fulfills:** FR10, NFR11 (load time < 3s), NFR57 (lazy loading)

---

### Story 5.5: Integrate CodeSandbox/StackBlitz Code Playgrounds

As a developer,
I want to interact with code playgrounds to modify and run project code,
So that I can verify code quality and explore implementation details.

**Acceptance Criteria:**

**Given** a project has a codePlaygroundUrl  
**When** I view the project detail page  
**Then** a "Try the Code" button is prominently displayed  
**And** clicking the button opens CodeSandbox/StackBlitz in a new tab  
**And** the playground loads with the project's code pre-loaded  
**And** if codePlaygroundUrl is null, the button is hidden  
**And** the button uses shadcn/ui Button component with code icon  
**And** the button is keyboard accessible  
**And** a fallback "View on GitHub" link is shown if playground URL is unavailable

**Technical Requirements:**
- "Try the Code" button with external link to CodeSandbox/StackBlitz
- `target="_blank" rel="noopener noreferrer"`
- shadcn/ui Button component with code icon (lucide-react)
- Conditional rendering if codePlaygroundUrl exists
- Fallback to GitHub link if playground unavailable
- Keyboard accessible

**Fulfills:** FR11, NFR42 (progressive enhancement), NFR44 (fallback to GitHub)

---

### Story 5.6: Add Video Walkthroughs with Technical Narration

As a visitor,
I want to watch video walkthroughs explaining project architecture and decisions,
So that I can understand the technical depth beyond just seeing the code.

**Acceptance Criteria:**

**Given** a project has a videoWalkthroughUrl  
**When** I view the project detail page  
**Then** a video player is embedded on the page  
**And** the video uses HTML5 `<video>` element or YouTube/Vimeo embed  
**And** the video has controls (play, pause, volume, fullscreen)  
**And** the video is responsive (16:9 aspect ratio)  
**And** the video is lazy loaded (not loaded until user scrolls to it)  
**And** if videoWalkthroughUrl is null, the section is hidden  
**And** the video player is keyboard accessible

**Technical Requirements:**
- HTML5 `<video>` element or YouTube/Vimeo iframe embed
- Responsive aspect ratio (16:9 using aspect-ratio CSS)
- Lazy loading (Intersection Observer or native `loading="lazy"`)
- Controls enabled
- Conditional rendering if videoWalkthroughUrl exists
- Keyboard accessible

**Fulfills:** FR12, NFR57 (lazy loading)

---

### Story 5.7: Display Performance Metrics Visualization

As a visitor,
I want to see performance metrics (LCP, INP, CLS) for each project,
So that I can verify the portfolio owner's commitment to performance optimization.

**Acceptance Criteria:**

**Given** a project has performanceMetrics (Json)  
**When** I view the project detail page  
**Then** a performance metrics section displays LCP, INP, and CLS scores  
**And** each metric is visualized with a progress bar or gauge  
**And** metrics are color-coded (green: good, yellow: needs improvement, red: poor)  
**And** Lighthouse scores are shown (Performance, Accessibility, Best Practices, SEO)  
**And** a timestamp shows when metrics were last measured  
**And** if performanceMetrics is null, the section is hidden  
**And** the visualization is responsive and accessible

**Technical Requirements:**
- Parse performanceMetrics Json field
- Display LCP, INP, CLS with visual indicators (progress bars or gauges)
- Color-coding based on Core Web Vitals thresholds
- Display Lighthouse scores (4 categories)
- Timestamp for last measurement
- Conditional rendering if performanceMetrics exists
- Responsive and accessible

**Fulfills:** FR13, NFR1-NFR7 (performance and quality scores)

---

### Story 5.8: Create Interactive Architecture Diagrams

As a developer,
I want to explore interactive architecture diagrams with clickable layers,
So that I can understand system design decisions in depth.

**Acceptance Criteria:**

**Given** a project has an architectureDiagramUrl  
**When** I view the project detail page  
**Then** an architecture diagram is displayed  
**And** the diagram is interactive (clickable layers reveal details)  
**And** clicking a component shows a tooltip or modal with explanation  
**And** the diagram is responsive (zoomable on mobile, full size on desktop)  
**And** if architectureDiagramUrl is null, the section is hidden  
**And** the diagram is keyboard accessible (tab through components, enter to expand)  
**And** the diagram uses SVG or image with clickable hotspots

**Technical Requirements:**
- SVG diagram with clickable elements or image with hotspots
- Tooltips or modals for component details
- Responsive (zoomable on mobile)
- Keyboard accessible (tab navigation, enter to expand)
- Conditional rendering if architectureDiagramUrl exists
- Consider using a library like react-zoom-pan-pinch for interactivity

**Fulfills:** FR14, NFR26 (keyboard navigation)

---

### Story 5.9: Build Case Study Section with Problem/Solution/Impact

As a client,
I want to read case studies showing business impact,
So that I can understand how the portfolio owner solves real-world problems.

**Acceptance Criteria:**

**Given** a project has caseStudy (Json)  
**When** I view the project detail page  
**Then** a case study section is displayed with three parts: Problem, Solution, Impact  
**And** the Problem section describes the business challenge  
**And** the Solution section explains the technical approach  
**And** the Impact section shows measurable business results (e.g., "40% increase in conversion rate")  
**And** client testimonials are included if available  
**And** the section uses clear visual hierarchy (headings, spacing)  
**And** if caseStudy is null, the section is hidden  
**And** the section is responsive and accessible

**Technical Requirements:**
- Parse caseStudy Json field (structure: { problem, solution, impact, testimonial? })
- Display three sections with clear headings
- Visual hierarchy with Tailwind typography
- Conditional rendering if caseStudy exists
- Responsive layout
- Accessible (proper heading hierarchy)

**Fulfills:** FR15, FR4 (client persona: business impact)

---

### Story 5.10: Add Project Filtering and Sorting

As a visitor,
I want to filter and sort projects by technology or type,
So that I can quickly find projects relevant to my interests.

**Acceptance Criteria:**

**Given** multiple projects exist  
**When** I view the Projects page  
**Then** filter buttons are displayed for common technologies (React, Next.js, TypeScript, etc.)  
**And** clicking a filter shows only projects using that technology  
**And** a sort dropdown allows sorting by: Featured, Newest, Oldest  
**And** filters and sorting work together (filter by React, sort by Newest)  
**And** the URL updates with query parameters for sharing filtered views  
**And** the component is keyboard accessible  
**And** the component uses Client Component for interactivity

**Technical Requirements:**
- Client Component (`'use client'`)
- Filter buttons for common tech stack items
- Sort dropdown (Featured, Newest, Oldest)
- Update URL with query parameters (useSearchParams, useRouter)
- Filter and sort logic on client side
- Keyboard accessible
- Responsive layout

**Fulfills:** FR17, NFR26 (keyboard navigation)

---

I'll continue with the remaining epics in the next message to keep this organized. This is Epic 5 complete with 10 stories. Shall I continue with Epics 6, 7, and 8?
## Epic 6: Visitor Engagement & Conversion

Visitors can submit context-aware contact inquiries, book consultations, indicate collaboration interest, and access social profiles. This enables frictionless conversion from visitor to contact.

### Story 6.1: Create Contact Form with Zod Validation

As a visitor,
I want to submit a contact inquiry via a form,
So that I can reach out to the portfolio owner for opportunities.

**Acceptance Criteria:**

**Given** I navigate to the Contact page  
**When** I view the contact form  
**Then** a form is displayed with fields: Name, Email, Message  
**And** all fields have proper labels and placeholders  
**And** the form uses Zod for runtime validation  
**And** client-side validation occurs before submission  
**And** validation errors are displayed with specific, helpful messages  
**And** the form is keyboard accessible (tab navigation, enter to submit)  
**And** the form uses shadcn/ui Form components  
**And** a submit button is prominently displayed

**Technical Requirements:**
- Client Component (`'use client'`)
- shadcn/ui Form components (Input, Textarea, Button)
- Zod schema for validation (name: min 2 chars, email: valid email, message: min 10 chars)
- Client-side validation before submission
- Error messages displayed below each field
- Keyboard accessible
- ARIA labels for accessibility

**Fulfills:** FR35, NFR18 (input validation), NFR33 (form labels), NFR34 (error messages)

---

### Story 6.2: Implement Persona-Specific Form Fields

As a visitor with a selected persona,
I want to see form fields tailored to my needs,
So that I can provide relevant information for my inquiry.

**Acceptance Criteria:**

**Given** I have selected a persona  
**When** I view the contact form  
**Then** additional fields appear based on my persona  
**And** for Recruiter persona: fields for "Role Title", "Company Name", "Timeline"  
**And** for Client persona: fields for "Project Budget", "Project Scope", "Business Goals"  
**And** for Developer persona: fields for "Collaboration Type", "Tech Stack Interest"  
**And** for no persona (balanced view): only basic fields (Name, Email, Message)  
**And** persona-specific fields are optional but encouraged  
**And** the form layout adjusts smoothly with transitions < 300ms  
**And** all fields are validated appropriately

**Technical Requirements:**
- Use `usePersona()` hook for conditional rendering
- Conditional fields based on persona state
- Smooth CSS transitions < 300ms
- Zod schema updates based on persona
- All fields validated appropriately
- Responsive layout

**Fulfills:** FR36, NFR2 (transitions < 500ms)

---

### Story 6.3: Add Email Integration with SMTP

As a portfolio owner,
I want to receive contact form submissions via email,
So that I can respond to inquiries promptly.

**Acceptance Criteria:**

**Given** a visitor submits the contact form  
**When** the form is submitted  
**Then** an API route processes the submission  
**And** an email is sent to the portfolio owner's email address  
**And** the email includes all form fields (name, email, message, persona-specific fields)  
**And** the email subject includes the persona type (e.g., "New Recruiter Inquiry from [Name]")  
**And** the email is sent using SMTP configuration (Nodemailer or similar)  
**And** environment variables store SMTP credentials (`SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASSWORD`)  
**And** the API route returns success or error response  
**And** the submission is logged server-side for debugging

**Technical Requirements:**
- API Route: `app/api/contact/route.ts`
- Nodemailer for SMTP email sending
- Environment variables: `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASSWORD`, `CONTACT_EMAIL`
- Email template with all form data
- Subject line includes persona type
- Server-side logging (console.log for debugging)
- Return JSON response: `{ success: boolean, message: string }`

**Fulfills:** FR35, NFR13 (data encryption in transit)

---

### Story 6.4: Implement Spam Protection and Rate Limiting

As a portfolio owner,
I want to protect the contact form from spam and abuse,
So that I only receive legitimate inquiries.

**Acceptance Criteria:**

**Given** a visitor attempts to submit the contact form  
**When** the submission is processed  
**Then** rate limiting is enforced (max 3 submissions per hour per IP address)  
**And** if rate limit is exceeded, an error message is shown: "Too many requests. Please try again in [X] minutes."  
**And** input sanitization prevents XSS attacks  
**And** honeypot field is added (hidden from users, rejects if filled)  
**And** submission timestamp validation prevents replay attacks  
**And** the API route validates all inputs server-side  
**And** suspicious submissions are logged for review

**Technical Requirements:**
- Rate limiting: max 3 submissions per hour per IP (use in-memory store or Redis)
- Input sanitization (strip HTML tags, escape special characters)
- Honeypot field (hidden input, reject if filled)
- Server-side validation with Zod
- Timestamp validation
- Logging for suspicious submissions

**Fulfills:** FR65, NFR18 (XSS prevention), NFR19 (spam protection), NFR20 (rate limiting)

---

### Story 6.5: Add Consultation Booking for Client Persona

As a client,
I want to book a consultation directly from the contact form,
So that I can discuss my project needs in detail.

**Acceptance Criteria:**

**Given** I have selected the Client persona  
**When** I view the contact form  
**Then** a "Book Consultation" checkbox is displayed  
**And** checking the box reveals additional fields: "Preferred Date", "Preferred Time", "Timezone"  
**And** the date picker uses shadcn/ui Calendar component  
**And** the time picker uses shadcn/ui Select component  
**And** timezone is auto-detected but can be manually changed  
**And** the consultation request is included in the email to the portfolio owner  
**And** the form validates that date/time are in the future  
**And** the component is keyboard accessible

**Technical Requirements:**
- Conditional rendering for Client persona
- shadcn/ui Calendar and Select components
- Auto-detect timezone (Intl.DateTimeFormat().resolvedOptions().timeZone)
- Validation: date/time must be in future
- Include consultation details in email
- Keyboard accessible

**Fulfills:** FR41, NFR33 (form labels)

---

### Story 6.6: Add Collaboration Interest for Developer Persona

As a developer,
I want to indicate collaboration interest,
So that I can explore partnership opportunities.

**Acceptance Criteria:**

**Given** I have selected the Developer persona  
**When** I view the contact form  
**Then** a "Collaboration Type" field is displayed  
**And** options include: "Open Source Contribution", "Freelance Project", "Full-Time Opportunity", "Partnership", "Other"  
**And** the field uses shadcn/ui Select component  
**And** selecting "Other" reveals a text input for custom collaboration type  
**And** the collaboration type is included in the email to the portfolio owner  
**And** the component is keyboard accessible

**Technical Requirements:**
- Conditional rendering for Developer persona
- shadcn/ui Select component
- Options: Open Source, Freelance, Full-Time, Partnership, Other
- Conditional text input if "Other" selected
- Include collaboration type in email
- Keyboard accessible

**Fulfills:** FR42, NFR33 (form labels)

---

### Story 6.7: Display Expected Response Time and Confirmation

As a visitor,
I want to know when to expect a response after submitting the form,
So that I have clear expectations.

**Acceptance Criteria:**

**Given** I successfully submit the contact form  
**When** the submission is processed  
**Then** a success message is displayed: "Thank you! Your message has been sent."  
**And** the expected response time is shown: "I typically respond within 24-48 hours."  
**And** the form fields are cleared after successful submission  
**And** a confirmation email is sent to the visitor's email address  
**And** the confirmation email includes a copy of their message  
**And** if submission fails, an error message is shown with retry option  
**And** the success/error message is accessible (ARIA live region)

**Technical Requirements:**
- Success message with expected response time
- Clear form fields after success
- Send confirmation email to visitor
- Error handling with retry option
- ARIA live region for accessibility
- shadcn/ui Toast or Alert component for messages

**Fulfills:** FR35, NFR34 (clear error messages)

---

## Epic 7: Admin Panel & Content Management

Portfolio owner can securely authenticate, create/edit/delete projects, upload optimized images, preview in all persona views, and publish instantly. This enables easy content updates without touching code.

### Story 7.1: Implement NextAuth.js Authentication

As a portfolio owner,
I want to authenticate securely to access the admin panel,
So that only I can manage portfolio content.

**Acceptance Criteria:**

**Given** NextAuth.js is configured  
**When** I navigate to `/admin`  
**Then** I am redirected to a login page  
**And** the login page has email and password fields  
**And** credentials are validated against the User model in the database  
**And** passwords are hashed using bcrypt  
**And** successful login creates a secure, HTTP-only session cookie  
**And** the session expires after 7 days of inactivity  
**And** logout functionality clears the session  
**And** environment variables `NEXTAUTH_SECRET` and `NEXTAUTH_URL` are configured

**Technical Requirements:**
- NextAuth.js with Credentials provider
- User model in Prisma schema (id, email, name, passwordHash)
- bcrypt for password hashing
- Secure, HTTP-only session cookies
- Session expiry: 7 days
- Environment variables: `NEXTAUTH_SECRET`, `NEXTAUTH_URL`
- Login page: `app/admin/login/page.tsx`
- Logout API route

**Fulfills:** FR25, NFR15 (NextAuth.js), NFR16 (secure sessions), NFR17 (RBAC)

---

### Story 7.2: Create Admin Dashboard Layout

As a portfolio owner,
I want to access an admin dashboard with navigation,
So that I can manage all aspects of my portfolio.

**Acceptance Criteria:**

**Given** I am authenticated  
**When** I navigate to `/admin`  
**Then** an admin dashboard is displayed  
**And** the dashboard has a sidebar with navigation links: Projects, Personal Info, Contact Settings, Analytics  
**And** the dashboard uses a clean, professional layout  
**And** the dashboard is responsive (collapsible sidebar on mobile)  
**And** a logout button is prominently displayed  
**And** the current page is highlighted in the navigation  
**And** the dashboard uses shadcn/ui components for consistency

**Technical Requirements:**
- Protected route: `/admin` (requires authentication)
- Admin layout with sidebar navigation
- Navigation links: Projects, Personal Info, Contact Settings, Analytics
- Responsive sidebar (collapsible on mobile)
- Logout button
- Active page highlighting
- shadcn/ui components

**Fulfills:** FR25, NFR26 (keyboard navigation)

---

### Story 7.3: Build Project CRUD Interface

As a portfolio owner,
I want to create, edit, and delete projects,
So that I can keep my portfolio up to date.

**Acceptance Criteria:**

**Given** I am in the admin dashboard  
**When** I navigate to the Projects page  
**Then** a table displays all projects (published and draft)  
**And** each row shows: title, status (published/draft), featured flag, actions (edit, delete)  
**And** a "Create New Project" button is prominently displayed  
**And** clicking "Create" opens a form with all project fields  
**And** clicking "Edit" opens a form pre-populated with project data  
**And** clicking "Delete" shows a confirmation dialog before deleting  
**And** the form includes fields for: title, description, techStack, role, URLs, highlights, thumbnailUrl, isFeatured, isPublished  
**And** the form uses shadcn/ui Form components  
**And** form submission creates/updates the project in the database  
**And** success/error messages are displayed after submission

**Technical Requirements:**
- Projects table with shadcn/ui Table component
- CRUD operations via API routes (`app/api/admin/projects/route.ts`)
- Form with all Project model fields
- shadcn/ui Form, Input, Textarea, Select, Checkbox components
- Confirmation dialog for delete (shadcn/ui AlertDialog)
- Success/error toast messages
- Optimistic UI updates

**Fulfills:** FR26, FR27, FR28, NFR26 (keyboard navigation)

---

### Story 7.4: Implement Image Upload with Automatic Optimization

As a portfolio owner,
I want to upload project images with automatic optimization,
So that images are web-optimized without manual processing.

**Acceptance Criteria:**

**Given** I am creating or editing a project  
**When** I upload an image (thumbnail or screenshot)  
**Then** the image is uploaded to a storage service (Vercel Blob or similar)  
**And** the image is automatically optimized to WebP format  
**And** the image is resized to appropriate dimensions (thumbnail: 800x600, screenshot: 1920x1080)  
**And** the optimized image URL is saved to the database  
**And** a preview of the uploaded image is shown immediately  
**And** multiple screenshots can be uploaded (up to 5)  
**And** upload progress is shown with a progress bar  
**And** file size and type validation is enforced (max 5MB, jpg/png/webp only)

**Technical Requirements:**
- Image upload API route (`app/api/admin/upload/route.ts`)
- Vercel Blob storage or similar (Cloudinary, AWS S3)
- Image optimization to WebP (sharp library)
- Resize: thumbnail 800x600, screenshot 1920x1080
- Multiple file upload support (up to 5 screenshots)
- Progress bar (shadcn/ui Progress component)
- Validation: max 5MB, jpg/png/webp only
- Preview after upload

**Fulfills:** FR29, NFR24 (alt text), NFR57 (image optimization)

---

### Story 7.5: Add Multi-Persona Preview Before Publishing

As a portfolio owner,
I want to preview projects in all three persona views before publishing,
So that I can ensure content looks good for all audiences.

**Acceptance Criteria:**

**Given** I am creating or editing a project  
**When** I click the "Preview" button  
**Then** a preview modal opens showing the project detail page  
**And** tabs allow switching between Recruiter, Client, Developer, and Balanced views  
**And** each tab shows how the project appears to that persona  
**And** persona-specific highlights are displayed correctly in each view  
**And** the preview uses the actual project detail page component  
**And** the modal is full-screen or large enough to see the full layout  
**And** a "Close Preview" button exits the modal  
**And** the preview is keyboard accessible (tab navigation, Escape to close)

**Technical Requirements:**
- Preview modal with shadcn/ui Dialog component
- Tabs for each persona view (shadcn/ui Tabs component)
- Render actual project detail page component with preview data
- Full-screen or large modal
- Keyboard accessible (Escape to close, tab navigation)
- Use project data from form (not yet saved)

**Fulfills:** FR30, NFR26 (keyboard navigation)

---

### Story 7.6: Implement Instant Publishing Workflow

As a portfolio owner,
I want to publish projects instantly to the live site,
So that updates appear immediately without deployment delays.

**Acceptance Criteria:**

**Given** I have created or edited a project  
**When** I toggle the "Published" status to true  
**Then** the project is immediately visible on the live site  
**And** the project appears in the project gallery if `isFeatured` is true  
**And** the project detail page is accessible at `/projects/[id]`  
**And** setting "Published" to false immediately hides the project from the live site  
**And** draft projects are only visible in the admin panel  
**And** a success message confirms the publish/unpublish action  
**And** the change is reflected in the database immediately

**Technical Requirements:**
- `isPublished` boolean field in Project model
- API route to update `isPublished` status
- Immediate database update (no caching issues)
- Conditional rendering on live site (only show if `isPublished=true`)
- Success toast message
- Optimistic UI update in admin panel

**Fulfills:** FR31, FR32

---

### Story 7.7: Create Personal Information Management Interface

As a portfolio owner,
I want to update my bio, skills, and experience,
So that my portfolio reflects my current expertise.

**Acceptance Criteria:**

**Given** I am in the admin dashboard  
**When** I navigate to the Personal Info page  
**Then** a form displays with fields for: bio, skills (array), experience (array of objects)  
**And** the bio field is a rich text editor or large textarea  
**And** skills can be added/removed with an array input component  
**And** experience entries have fields: company, role, startDate, endDate, description  
**And** experience entries can be added/removed/reordered  
**And** form submission updates the User model or a separate PersonalInfo model  
**And** changes are reflected on the live site immediately  
**And** success/error messages are displayed after submission

**Technical Requirements:**
- Personal Info form with shadcn/ui components
- Rich text editor or Textarea for bio
- Array input for skills (add/remove chips)
- Dynamic form for experience entries (add/remove/reorder)
- API route to update personal info
- Immediate reflection on live site
- Success/error toast messages

**Fulfills:** FR33, FR38, FR39

---

### Story 7.8: Add Contact Form Settings Management

As a portfolio owner,
I want to manage contact form settings,
So that I can control email notifications and auto-responses.

**Acceptance Criteria:**

**Given** I am in the admin dashboard  
**When** I navigate to the Contact Settings page  
**Then** a form displays with settings: notification email, auto-response enabled, auto-response message, expected response time  
**And** the notification email field allows changing where contact form submissions are sent  
**And** the auto-response toggle enables/disables automatic confirmation emails  
**And** the auto-response message is a textarea for customizing the confirmation email  
**And** the expected response time is a text input (e.g., "24-48 hours")  
**And** form submission updates the settings in the database  
**And** changes are reflected in contact form behavior immediately  
**And** success/error messages are displayed after submission

**Technical Requirements:**
- Contact Settings form with shadcn/ui components
- Fields: notificationEmail, autoResponseEnabled, autoResponseMessage, expectedResponseTime
- Store settings in database (ContactSettings model or User model)
- API route to update settings
- Immediate reflection in contact form behavior
- Success/error toast messages

**Fulfills:** FR34

---

### Story 7.9: Implement Error Handling with Graceful Degradation

As a portfolio owner,
I want the admin panel to handle errors gracefully,
So that I can continue working even if some features fail.

**Acceptance Criteria:**

**Given** I am using the admin panel  
**When** an API call fails  
**Then** an error message is displayed with a specific, helpful description  
**And** the error does not crash the entire admin panel  
**And** cached data is shown if available with a "Last updated: [timestamp]" indicator  
**And** a retry button is provided for failed operations  
**And** errors are logged server-side for debugging  
**And** error boundaries catch and handle client-side errors  
**And** the user can continue using other features despite the error

**Technical Requirements:**
- Error boundaries for client-side error handling
- Try-catch blocks in API routes
- Graceful degradation with cached data
- Error toast messages with retry option
- Server-side logging (console.error)
- Specific error messages (not generic "Something went wrong")

**Fulfills:** FR61, FR62, NFR61 (graceful UX), NFR62 (caching)

---

## Epic 8: Analytics & Measurement

Portfolio owner can track visitor engagement, persona selection rates, project interactions, conversion rates, and Core Web Vitals performance. This enables data-driven optimization and iteration.

### Story 8.1: Integrate Vercel Analytics for Core Web Vitals

As a portfolio owner,
I want to track Core Web Vitals (LCP, INP, CLS) automatically,
So that I can monitor performance and ensure targets are met.

**Acceptance Criteria:**

**Given** Vercel Analytics is integrated  
**When** visitors use the portfolio  
**Then** Core Web Vitals metrics are automatically tracked (LCP, INP, CLS)  
**And** metrics are sent to Vercel Analytics dashboard  
**And** I can view real-time and historical performance data in Vercel dashboard  
**And** alerts are configured for performance regressions (LCP > 2.5s, INP > 200ms, CLS > 0.1)  
**And** the analytics script has minimal impact on page performance  
**And** environment variable `NEXT_PUBLIC_VERCEL_ANALYTICS_ID` is configured

**Technical Requirements:**
- Install `@vercel/analytics`
- Add Analytics component to root layout
- Environment variable: `NEXT_PUBLIC_VERCEL_ANALYTICS_ID` (auto-set by Vercel)
- Configure alerts in Vercel dashboard
- Minimal performance impact

**Fulfills:** FR47, NFR47 (Core Web Vitals tracking), NFR48 (monitoring and alerts)

---

### Story 8.2: Integrate Plausible Analytics for Privacy-Friendly Tracking

As a portfolio owner,
I want to track visitor behavior without compromising privacy,
So that I can understand engagement while respecting GDPR compliance.

**Acceptance Criteria:**

**Given** Plausible Analytics is integrated  
**When** visitors use the portfolio  
**Then** page views, unique visitors, and bounce rate are tracked  
**And** no personal data or cookies are stored (GDPR compliant)  
**And** I can view analytics in the Plausible dashboard  
**And** custom events are tracked: persona selection, project views, contact form submissions  
**And** the analytics script is lightweight and doesn't impact performance  
**And** environment variable `PLAUSIBLE_DOMAIN` is configured

**Technical Requirements:**
- Add Plausible script to root layout
- Environment variable: `PLAUSIBLE_DOMAIN`
- Track custom events: `plausible('Persona Selected', { props: { persona: 'recruiter' } })`
- Custom events: persona selection, project view, contact submission
- Lightweight script (< 1KB)

**Fulfills:** FR43, FR44, FR45, FR46, NFR48 (monitoring)

---

### Story 8.3: Create PersonaSelection Tracking Model

As a portfolio owner,
I want to track which personas visitors select,
So that I can understand my audience composition.

**Acceptance Criteria:**

**Given** a visitor selects a persona  
**When** the persona is set in PersonaContext  
**Then** a PersonaSelection event is recorded in the database  
**And** the event includes: persona type, timestamp, sessionId, userAgent, referrer  
**And** the event is sent to an API route asynchronously (doesn't block UI)  
**And** the PersonaSelection model is defined in Prisma schema  
**And** I can query persona selection rates in the analytics dashboard  
**And** the tracking respects user privacy (no PII stored)

**Technical Requirements:**
- Prisma model: PersonaSelection (id, persona, timestamp, sessionId, userAgent, referrer)
- API route: `app/api/analytics/persona-selection/route.ts`
- Async tracking (doesn't block UI)
- Generate sessionId (UUID) on client side
- Store userAgent and referrer server-side
- No PII (personally identifiable information)

**Fulfills:** FR44, NFR48 (monitoring)

---

### Story 8.4: Create ProjectAnalytics Tracking Model

As a portfolio owner,
I want to track which projects visitors interact with,
So that I can understand which work resonates most.

**Acceptance Criteria:**

**Given** a visitor interacts with a project  
**When** they view a project detail page, click "View Live Demo", or click "Try the Code"  
**Then** a ProjectAnalytics event is recorded in the database  
**And** the event includes: projectId, eventType (view, demo, code), persona, timestamp, sessionId, timeSpent  
**And** time spent on project detail page is tracked  
**And** the event is sent to an API route asynchronously  
**And** the ProjectAnalytics model is defined in Prisma schema  
**And** I can query project interaction rates in the analytics dashboard

**Technical Requirements:**
- Prisma model: ProjectAnalytics (id, projectId, eventType, persona, timestamp, sessionId, timeSpent)
- API route: `app/api/analytics/project-interaction/route.ts`
- Track events: view, demo, code
- Track time spent using Intersection Observer or visibility API
- Async tracking (doesn't block UI)
- Link to Project model (foreign key)

**Fulfills:** FR45, NFR48 (monitoring)

---

### Story 8.5: Build Analytics Dashboard for Portfolio Owner

As a portfolio owner,
I want to view key metrics in an analytics dashboard,
So that I can make data-driven decisions about content.

**Acceptance Criteria:**

**Given** I am in the admin dashboard  
**When** I navigate to the Analytics page  
**Then** a dashboard displays key metrics: total visitors, persona selection breakdown, top projects, contact form conversion rate, Core Web Vitals scores  
**And** persona selection is shown as a pie chart or bar chart  
**And** top projects are ranked by views and interactions  
**And** contact form conversion rate shows: (submissions / total visitors) * 100  
**And** Core Web Vitals are shown with color-coded indicators (green/yellow/red)  
**And** date range filters allow viewing data for: last 7 days, last 30 days, last 90 days, all time  
**And** the dashboard is responsive and accessible  
**And** data is fetched from the database and Vercel/Plausible APIs

**Technical Requirements:**
- Analytics dashboard page: `app/admin/analytics/page.tsx`
- Fetch data from PersonaSelection and ProjectAnalytics models
- Fetch Core Web Vitals from Vercel Analytics API
- Charts using recharts or similar library
- Date range filters
- Responsive layout
- Keyboard accessible

**Fulfills:** FR48, NFR48 (monitoring)

---

### Story 8.6: Implement Engagement Heatmaps

As a portfolio owner,
I want to visualize where visitors click and scroll,
So that I can optimize layout and content placement.

**Acceptance Criteria:**

**Given** I am viewing the analytics dashboard  
**When** I navigate to the Heatmaps section  
**Then** a heatmap visualization shows click patterns on key pages  
**And** scroll depth is visualized showing how far visitors scroll  
**And** heatmaps are generated for: Home, About, Skills, Projects pages  
**And** I can toggle between click heatmap and scroll heatmap  
**And** the heatmap uses a color gradient (blue: low activity, red: high activity)  
**And** the heatmap is overlaid on a screenshot of the page  
**And** the data is collected using a lightweight tracking script

**Technical Requirements:**
- Heatmap tracking script (consider Hotjar, Microsoft Clarity, or custom solution)
- Store click coordinates and scroll depth in database
- Heatmap visualization library (heatmap.js or similar)
- Toggle between click and scroll heatmaps
- Color gradient visualization
- Overlay on page screenshot

**Fulfills:** FR43, NFR48 (monitoring)

---

### Story 8.7: Add Conversion Funnel Analysis

As a portfolio owner,
I want to track the visitor journey from landing to contact,
So that I can identify drop-off points and optimize conversion.

**Acceptance Criteria:**

**Given** I am viewing the analytics dashboard  
**When** I navigate to the Conversion Funnel section  
**Then** a funnel visualization shows: Landing → Persona Selection → Project View → Contact Form → Submission  
**And** each step shows the number and percentage of visitors who progressed  
**And** drop-off rates are highlighted for each step  
**And** I can filter by persona to see persona-specific funnels  
**And** the funnel is visualized as a bar chart or funnel chart  
**And** the data is calculated from PersonaSelection, ProjectAnalytics, and contact form submissions

**Technical Requirements:**
- Funnel visualization using recharts or similar
- Calculate funnel steps from database queries
- Steps: Landing → Persona Selection → Project View → Contact Form → Submission
- Show counts and percentages for each step
- Filter by persona
- Highlight drop-off rates

**Fulfills:** FR46, NFR48 (monitoring)

---

### Story 8.8: Integrate Sentry for Error Tracking

As a portfolio owner,
I want to track production errors automatically,
So that I can fix issues before they impact many users.

**Acceptance Criteria:**

**Given** Sentry is integrated  
**When** an error occurs in production  
**Then** the error is automatically captured and sent to Sentry  
**And** error details include: stack trace, user context, breadcrumbs, environment  
**And** I receive email notifications for new errors  
**And** errors are grouped by type for easy triage  
**And** source maps are uploaded for readable stack traces  
**And** environment variable `SENTRY_DSN` is configured  
**And** Sentry has minimal impact on performance

**Technical Requirements:**
- Install `@sentry/nextjs`
- Configure Sentry in `sentry.client.config.ts` and `sentry.server.config.ts`
- Environment variable: `SENTRY_DSN`
- Upload source maps during build
- Email notifications for new errors
- Minimal performance impact

**Fulfills:** NFR48 (monitoring and alerts)

---
