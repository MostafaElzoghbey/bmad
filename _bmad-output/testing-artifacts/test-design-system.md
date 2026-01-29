# System-Level Test Design - bmad Portfolio

**Project**: bmad Portfolio  
**Phase**: Phase 3 - Solutioning (Pre-Implementation)  
**Generated**: 2026-01-29  
**Author**: Murat (TEA - Test Engineering Architect)  
**Workflow**: `/bmad:bmm:workflows:test-design` (System-Level Mode)

---

## Executive Summary

This document provides a comprehensive testability assessment of the bmad portfolio architecture before implementation begins. The analysis evaluates architectural decisions against testability criteria, identifies critical risks, defines the test levels strategy, and provides actionable recommendations to ensure the system can be effectively tested.

**Key Findings**:
- ✅ **Overall Testability**: GOOD - Architecture supports robust testing with clear separation of concerns
- ⚠️ **Concerns Identified**: 3 medium-priority testability risks requiring mitigation
- 🎯 **Recommended Test Levels**: E2E (Playwright), Integration (API), Component (React), Unit (Jest)
- 📊 **NFR Coverage**: Performance, Accessibility, SEO require explicit validation strategy

---

## 1. Architecture Testability Assessment

### 1.1 Testability Criteria Evaluation

Based on the loaded architecture and applying TEA knowledge base criteria:

#### ✅ **Strengths (High Testability)**

**1. Clear Separation of Concerns**
- **Decision**: Next.js App Router with Server/Client Components
- **Testability Impact**: HIGH ✅
  - Server Components can be tested in isolation (unit/integration)
  - Client Components can be tested with Playwright Component Testing
  - API routes are independently testable via HTTP requests
  - Clear boundaries enable focused test scopes

**2. Deterministic State Management**
- **Decision**: React Context + localStorage for persona state
- **Testability Impact**: HIGH ✅
  - State is predictable and controllable in tests
  - localStorage can be mocked/seeded for deterministic tests
  - No complex state synchronization issues
  - Easy to set up test fixtures with specific persona states

**3. API Caching Strategy**
- **Decision**: SWR with configurable polling intervals
- **Testability Impact**: MEDIUM-HIGH ✅
  - Network requests can be intercepted and mocked
  - Polling intervals can be controlled in tests
  - Graceful degradation is testable (stale data scenarios)
  - Cache invalidation is deterministic

**4. Database Schema (Prisma)**
- **Decision**: Prisma ORM with PostgreSQL
- **Testability Impact**: HIGH ✅
  - Schema-first approach enables test database seeding
  - Migrations are version-controlled and repeatable
  - Test isolation via transactions or database cleanup
  - Type-safe queries reduce runtime errors

**5. Error Handling Strategy**
- **Decision**: Graceful degradation with user-friendly messages
- **Testability Impact**: HIGH ✅
  - Error paths are explicit and testable
  - Fallback UI states can be validated
  - Network failures can be simulated
  - Error boundaries are testable components

#### ⚠️ **Concerns (Medium Testability Risk)**

**1. Real-Time API Polling (GitHub/LeetCode)**
- **Risk Category**: PERF, DATA
- **Testability Concern**: MEDIUM ⚠️
  - **Issue**: 5-minute GitHub polling and 1-hour LeetCode polling create timing dependencies
  - **Impact**: Tests may be slow or flaky if waiting for real polling intervals
  - **Mitigation Required**:
    - Mock API responses for deterministic tests
    - Use test-specific polling intervals (e.g., 100ms in tests)
    - Implement manual refresh triggers for E2E tests
    - Add network interception to control API timing
  - **Owner**: Development Team
  - **Priority**: P1 (Must address before E2E test implementation)

**2. Persona-Based Content Rendering**
- **Risk Category**: BUS, TECH
- **Testability Concern**: MEDIUM ⚠️
  - **Issue**: Three persona variants (Recruiter/Client/Developer) multiply test scenarios
  - **Impact**: Potential for 3x test duplication if not structured properly
  - **Mitigation Required**:
    - Use parametrized tests for persona-agnostic features
    - Create persona fixtures for setup (avoid manual switching in every test)
    - Test persona switching logic separately from content rendering
    - Use component tests for persona-specific content hierarchies
  - **Owner**: Test Engineering
  - **Priority**: P1 (Test design pattern needed)

**3. External API Dependencies (GitHub, LeetCode)**
- **Risk Category**: OPS, DATA
- **Testability Concern**: MEDIUM ⚠️
  - **Issue**: Tests depend on external APIs that may be rate-limited or unavailable
  - **Impact**: Flaky tests, CI failures due to network issues
  - **Mitigation Required**:
    - Implement network-first interception (HAR capture for replay)
    - Create mock API responses for offline testing
    - Add circuit breaker tests (validate fallback when APIs fail)
    - Use VCR/Polly.js for recording/replaying HTTP interactions
  - **Owner**: Development Team
  - **Priority**: P1 (Required for reliable CI/CD)

#### ✅ **Architectural Decisions Supporting Testability**

| Decision | Testability Benefit | Test Level Impact |
|----------|---------------------|-------------------|
| **Next.js App Router** | Clear routing structure, testable layouts | E2E, Integration |
| **TypeScript Strict Mode** | Type safety reduces runtime errors, better IDE support | Unit, Integration |
| **Tailwind CSS** | Utility-first classes, no CSS-in-JS complexity | Component, E2E |
| **Prisma Schema** | Type-safe DB queries, migration-based schema | Integration, Unit |
| **Vercel Deployment** | Preview deployments for manual testing | Manual, E2E |
| **SWR Caching** | Deterministic cache behavior, mockable | Integration, E2E |
| **Error Boundaries** | Isolated error handling, testable fallbacks | Component, E2E |

---

## 2. Architecturally Significant Requirements (ASRs)

ASRs are requirements that significantly impact architecture and require comprehensive testing.

### 2.1 Identified ASRs

#### ASR-1: Persona-Based Experience (NFR2, FR1-FR7)
- **Requirement**: Persona selection with <500ms transition, localStorage persistence
- **Architectural Impact**: HIGH
  - Drives state management decision (React Context)
  - Affects content rendering strategy (conditional hierarchies)
  - Impacts performance (transition animations)
- **Test Coverage Required**:
  - **E2E**: Persona selection flow, content hierarchy validation
  - **Component**: Persona selector UI, transition animations
  - **Integration**: localStorage persistence, context state updates
  - **Unit**: Persona state logic, content filtering functions
- **Risk Score**: 6 (Probability: 2, Impact: 3)
  - **Justification**: Core differentiator, affects all pages, complex state management

#### ASR-2: Real-Time Skill Verification (NFR3, FR8-FR13)
- **Requirement**: GitHub 5-min polling, LeetCode 1-hour polling, graceful degradation
- **Architectural Impact**: HIGH
  - Drives API caching strategy (SWR with custom intervals)
  - Affects error handling (stale data display)
  - Impacts performance (polling overhead)
- **Test Coverage Required**:
  - **E2E**: API polling behavior, stale data display, manual refresh
  - **Integration**: API client retry logic, cache invalidation
  - **Unit**: Polling interval configuration, error state handling
- **Risk Score**: 8 (Probability: 3, Impact: 3)
  - **Justification**: External API dependency, rate limiting, network failures

#### ASR-3: Performance Standards (NFR1, NFR4, NFR5)
- **Requirement**: <2s initial load, <500ms transitions, 90+ Lighthouse scores
- **Architectural Impact**: HIGH
  - Drives deployment strategy (Vercel Edge Network)
  - Affects image optimization (Next.js Image component)
  - Impacts bundle size (code splitting, lazy loading)
- **Test Coverage Required**:
  - **E2E**: Lighthouse CI validation, Core Web Vitals
  - **Integration**: API response times, image optimization
  - **Load Testing**: k6 for concurrent user simulation
- **Risk Score**: 6 (Probability: 2, Impact: 3)
  - **Justification**: Strict SLOs, affects user experience, SEO ranking

#### ASR-4: Accessibility Compliance (NFR26, NFR27, NFR28)
- **Requirement**: WCAG 2.1 AA, keyboard navigation, screen reader support
- **Architectural Impact**: MEDIUM
  - Affects component design (semantic HTML, ARIA attributes)
  - Impacts routing (focus management)
  - Drives testing strategy (axe-core integration)
- **Test Coverage Required**:
  - **E2E**: Keyboard navigation flows, screen reader announcements
  - **Component**: ARIA attributes, focus management
  - **Automated**: axe-core accessibility scans
- **Risk Score**: 4 (Probability: 2, Impact: 2)
  - **Justification**: Compliance requirement, affects all UI components

#### ASR-5: SEO Optimization (NFR6-NFR10)
- **Requirement**: Meta tags, Open Graph, structured data, sitemap
- **Architectural Impact**: MEDIUM
  - Drives SSR strategy (Next.js metadata API)
  - Affects routing (dynamic sitemap generation)
  - Impacts content structure (semantic HTML)
- **Test Coverage Required**:
  - **E2E**: Meta tag validation, Open Graph preview
  - **Integration**: Sitemap generation, robots.txt
  - **Automated**: SEO audit tools (Lighthouse, SEO analyzer)
- **Risk Score**: 4 (Probability: 2, Impact: 2)
  - **Justification**: Business-critical for discoverability

---

## 3. Test Levels Strategy

### 3.1 Test Pyramid for bmad Portfolio

Based on the architecture and ASRs, the recommended test distribution:

```
        /\
       /  \  E2E (Playwright)
      /____\  15% - Critical user journeys
     /      \
    / INTEG  \ Integration (API + DB)
   /__________\ 35% - Service layer, API contracts
  /            \
 /     UNIT     \ Unit (Jest + React Testing Library)
/________________\ 50% - Business logic, utilities, components
```

### 3.2 Test Level Assignments

#### **Unit Tests (50% coverage target)**
- **Tool**: Jest + React Testing Library
- **Scope**:
  - Pure functions (utility functions, data transformations)
  - React hooks (usePersona, useSkillVerification)
  - Business logic (persona filtering, content hierarchy)
  - Data factories (createUser, createProject)
- **Examples**:
  - `utils/persona-filter.test.ts` - Persona content filtering logic
  - `hooks/usePersona.test.ts` - Persona state management hook
  - `utils/date-formatter.test.ts` - Date formatting utilities
- **Rationale**: Fast feedback, high coverage for business logic

#### **Component Tests (Included in Unit %)**
- **Tool**: Playwright Component Testing (or React Testing Library)
- **Scope**:
  - Isolated UI components (PersonaSelector, ProjectCard, SkillBadge)
  - Component props and events
  - Accessibility (ARIA attributes, keyboard navigation)
- **Examples**:
  - `components/PersonaSelector.spec.tsx` - Persona selection UI
  - `components/ProjectCard.spec.tsx` - Project card rendering
  - `components/SkillVerificationBadge.spec.tsx` - Skill badge states
- **Rationale**: UI component validation without full app context

#### **Integration Tests (35% coverage target)**
- **Tool**: Playwright (API testing) + Prisma (DB)
- **Scope**:
  - API routes (`/api/projects`, `/api/testimonials`, `/api/analytics`)
  - Database operations (CRUD, migrations)
  - External API clients (GitHub, LeetCode with mocks)
  - SWR cache behavior
- **Examples**:
  - `tests/integration/api/projects.spec.ts` - Projects API CRUD
  - `tests/integration/api/github-client.spec.ts` - GitHub API client
  - `tests/integration/db/prisma.spec.ts` - Database operations
- **Rationale**: Validate service layer and data flow

#### **End-to-End Tests (15% coverage target)**
- **Tool**: Playwright (browser automation)
- **Scope**:
  - Critical user journeys (persona selection → project view → contact)
  - Cross-page workflows (navigation, state persistence)
  - Visual regression (persona-specific layouts)
  - Performance validation (Lighthouse CI)
- **Examples**:
  - `tests/e2e/persona-journey.spec.ts` - Recruiter journey end-to-end
  - `tests/e2e/project-showcase.spec.ts` - Interactive project demos
  - `tests/e2e/accessibility.spec.ts` - Keyboard navigation, screen reader
- **Rationale**: Validate complete user experience

#### **Performance Tests (Separate from pyramid)**
- **Tool**: k6 (load testing), Lighthouse CI (Core Web Vitals)
- **Scope**:
  - Load testing (50 concurrent users)
  - Stress testing (breaking point identification)
  - Core Web Vitals (LCP, FID, CLS)
  - API response times (p95 <500ms)
- **Examples**:
  - `tests/performance/load-test.k6.js` - Concurrent user simulation
  - `tests/performance/lighthouse.spec.ts` - Core Web Vitals validation
- **Rationale**: Validate NFR3 (performance SLOs)

---

## 4. NFR Testing Approach

### 4.1 Security (SEC)

**Requirements**: No authentication system (public portfolio), but secure API handling

**Test Strategy**:
- ✅ **Input Validation**: API routes validate input (Zod schemas)
- ✅ **XSS Prevention**: Next.js auto-escapes JSX content
- ✅ **CSRF Protection**: Next.js built-in CSRF tokens
- ⚠️ **Rate Limiting**: Not specified in architecture
  - **Recommendation**: Add rate limiting for API routes (e.g., `/api/contact`)
  - **Test**: Validate rate limiting with k6 (429 responses after threshold)

**Automated Tests**:
```typescript
// tests/nfr/security.spec.ts
test('API routes validate input and reject malicious payloads', async ({ request }) => {
  const xssPayload = '<script>alert("XSS")</script>';
  const response = await request.post('/api/contact', {
    data: { name: xssPayload, email: 'test@example.com', message: 'Test' }
  });
  
  // Should sanitize or reject
  expect(response.status()).toBe(400); // Or 200 with sanitized data
});
```

### 4.2 Performance (PERF)

**Requirements**: <2s initial load, <500ms transitions, 90+ Lighthouse scores

**Test Strategy**:
- ✅ **Lighthouse CI**: Automated Core Web Vitals validation
- ✅ **k6 Load Testing**: Simulate 50 concurrent users
- ✅ **API Response Times**: p95 <500ms for all endpoints
- ✅ **Bundle Size**: Monitor bundle size (Next.js Bundle Analyzer)

**Automated Tests**:
```typescript
// tests/nfr/performance.spec.ts
import { test, expect } from '@playwright/test';

test('homepage loads in under 2 seconds', async ({ page }) => {
  const startTime = Date.now();
  await page.goto('/');
  await page.waitForLoadState('networkidle');
  const loadTime = Date.now() - startTime;
  
  expect(loadTime).toBeLessThan(2000);
});

test('persona transitions complete in under 500ms', async ({ page }) => {
  await page.goto('/');
  
  const startTime = Date.now();
  await page.click('[data-testid="persona-recruiter"]');
  await page.waitForSelector('[data-persona="recruiter"]', { state: 'visible' });
  const transitionTime = Date.now() - startTime;
  
  expect(transitionTime).toBeLessThan(500);
});
```

**k6 Load Test**:
```javascript
// tests/nfr/load-test.k6.js
export const options = {
  stages: [
    { duration: '1m', target: 50 }, // Ramp to 50 users
    { duration: '3m', target: 50 }, // Stay at 50 users
  ],
  thresholds: {
    http_req_duration: ['p(95)<500'], // 95% of requests <500ms
    http_req_failed: ['rate<0.01'],   // Error rate <1%
  },
};

export default function () {
  http.get(`${__ENV.BASE_URL}/`);
  http.get(`${__ENV.BASE_URL}/projects`);
  sleep(1);
}
```

### 4.3 Reliability (OPS)

**Requirements**: Graceful degradation when GitHub/LeetCode APIs fail

**Test Strategy**:
- ✅ **Network Failure Simulation**: Mock API failures, validate stale data display
- ✅ **Retry Logic**: Validate SWR retry behavior (3 attempts)
- ✅ **Error Boundaries**: Test React error boundaries with simulated errors
- ✅ **Offline Mode**: Validate app behavior when offline

**Automated Tests**:
```typescript
// tests/nfr/reliability.spec.ts
test('app shows stale data when GitHub API fails', async ({ page, context }) => {
  // Mock API failure
  await context.route('**/api/github/stats', route => {
    route.fulfill({ status: 500, body: JSON.stringify({ error: 'API Error' }) });
  });
  
  await page.goto('/');
  
  // Should show stale data with timestamp
  await expect(page.getByText(/Last updated:/)).toBeVisible();
  await expect(page.getByText(/Unable to refresh/)).toBeVisible();
});
```

### 4.4 Accessibility (A11Y)

**Requirements**: WCAG 2.1 AA, keyboard navigation, screen reader support

**Test Strategy**:
- ✅ **axe-core Integration**: Automated accessibility scans
- ✅ **Keyboard Navigation**: E2E tests for tab order, focus management
- ✅ **Screen Reader**: Manual testing with NVDA/JAWS
- ✅ **Color Contrast**: Automated contrast ratio validation

**Automated Tests**:
```typescript
// tests/nfr/accessibility.spec.ts
import { test, expect } from '@playwright/test';
import AxeBuilder from '@axe-core/playwright';

test('homepage has no accessibility violations', async ({ page }) => {
  await page.goto('/');
  
  const accessibilityScanResults = await new AxeBuilder({ page }).analyze();
  
  expect(accessibilityScanResults.violations).toEqual([]);
});

test('persona selector is keyboard navigable', async ({ page }) => {
  await page.goto('/');
  
  // Tab to persona selector
  await page.keyboard.press('Tab');
  await page.keyboard.press('Tab'); // Adjust based on page structure
  
  // Select persona with Enter
  await page.keyboard.press('Enter');
  
  // Verify persona selected
  await expect(page.locator('[data-persona="recruiter"]')).toBeVisible();
});
```

### 4.5 Maintainability (TECH)

**Requirements**: Clean code, test coverage ≥80%, no critical vulnerabilities

**Test Strategy**:
- ✅ **Test Coverage**: Jest coverage reports (80% threshold)
- ✅ **Code Duplication**: jscpd in CI (<5% duplication)
- ✅ **Vulnerability Scanning**: npm audit in CI (no critical/high)
- ✅ **Linting**: ESLint + TypeScript strict mode

**CI Validation** (GitHub Actions):
```yaml
# .github/workflows/quality.yml
- name: Check test coverage
  run: |
    npm run test:coverage
    COVERAGE=$(jq '.total.lines.pct' coverage/coverage-summary.json)
    if (( $(echo "$COVERAGE < 80" | bc -l) )); then
      echo "❌ Coverage $COVERAGE% below 80%"
      exit 1
    fi
```

---

## 5. Risk Assessment and Mitigation

### 5.1 Risk Summary

| Risk ID | Category | Title | Probability | Impact | Score | Status |
|---------|----------|-------|-------------|--------|-------|--------|
| RISK-001 | PERF, DATA | Real-time API polling timing dependencies | 3 | 3 | 9 | OPEN |
| RISK-002 | BUS, TECH | Persona-based test scenario multiplication | 2 | 3 | 6 | OPEN |
| RISK-003 | OPS, DATA | External API dependency flakiness | 3 | 2 | 6 | OPEN |
| RISK-004 | PERF | Performance SLO validation complexity | 2 | 2 | 4 | OPEN |
| RISK-005 | A11Y | Accessibility compliance verification | 2 | 2 | 4 | OPEN |

### 5.2 Critical Risk (Score = 9)

#### RISK-001: Real-Time API Polling Timing Dependencies
- **Category**: PERF, DATA
- **Probability**: 3 (High) - Tests will encounter polling delays
- **Impact**: 3 (High) - Slow tests, flaky CI, poor developer experience
- **Score**: 9 (CRITICAL BLOCKER)
- **Status**: OPEN

**Mitigation Plan**:
1. **Action**: Implement test-specific polling intervals
   - **Owner**: Development Team
   - **Deadline**: Before E2E test implementation (Epic 4)
   - **Implementation**:
     ```typescript
     // lib/config.ts
     export const POLLING_INTERVALS = {
       github: process.env.NODE_ENV === 'test' ? 100 : 300000, // 100ms in tests, 5min in prod
       leetcode: process.env.NODE_ENV === 'test' ? 200 : 3600000, // 200ms in tests, 1hr in prod
     };
     ```

2. **Action**: Add manual refresh triggers for E2E tests
   - **Owner**: Test Engineering
   - **Deadline**: Before E2E test implementation
   - **Implementation**:
     ```typescript
     // components/SkillVerification.tsx
     <button data-testid="refresh-skills" onClick={() => mutate()}>
       Refresh
     </button>
     ```

3. **Action**: Mock API responses for deterministic tests
   - **Owner**: Test Engineering
   - **Deadline**: Before integration test implementation
   - **Implementation**: Use Playwright route interception with HAR files

**Verification**:
- E2E tests complete in <1.5 minutes
- No flaky tests due to polling delays
- CI pipeline runs reliably

### 5.3 High Risks (Score 6-8)

#### RISK-002: Persona-Based Test Scenario Multiplication
- **Mitigation**:
  - Use parametrized tests for persona-agnostic features
  - Create persona fixtures (`seedPersona('recruiter')`)
  - Test persona switching logic separately from content rendering
  - Use component tests for persona-specific content hierarchies

#### RISK-003: External API Dependency Flakiness
- **Mitigation**:
  - Implement network-first interception (HAR capture)
  - Create mock API responses for offline testing
  - Add circuit breaker tests (validate fallback when APIs fail)
  - Use VCR/Polly.js for recording/replaying HTTP interactions

---

## 6. Testability Recommendations

### 6.1 Immediate Actions (Before Implementation)

1. **Add Test-Specific Configuration**
   - Create `lib/config.ts` with environment-aware polling intervals
   - Add `data-testid` attributes to all interactive elements
   - Implement manual refresh triggers for real-time features

2. **Set Up Test Infrastructure**
   - Initialize Playwright with TypeScript configuration
   - Set up Jest with React Testing Library
   - Configure test database (PostgreSQL with Docker)
   - Add k6 for performance testing

3. **Create Test Fixtures and Factories**
   - Implement data factories (`createUser`, `createProject`, `createTestimonial`)
   - Create persona fixtures (`seedPersona`, `switchPersona`)
   - Set up database seeding helpers (`seedDatabase`, `cleanupDatabase`)

4. **Define Test Naming Conventions**
   - Unit: `test_{component}_{scenario}`
   - Integration: `test_{flow}_{interaction}`
   - E2E: `test_{journey}_{outcome}`
   - Test IDs: `{EPIC}.{STORY}-{LEVEL}-{SEQ}` (e.g., `2.1-E2E-001`)

### 6.2 Architecture Enhancements

1. **Add Rate Limiting** (Security)
   - Implement rate limiting for `/api/contact` endpoint
   - Test: Validate 429 responses after threshold

2. **Add Health Check Endpoint** (Reliability)
   - Create `/api/health` endpoint monitoring database, external APIs
   - Test: Validate health check returns service status

3. **Add Telemetry Headers** (Observability)
   - Include `Server-Timing` headers for API response times
   - Include `x-trace-id` for request correlation
   - Test: Validate headers present in API responses

### 6.3 Test Quality Standards

All tests must adhere to TEA quality standards:
- ✅ **No Hard Waits**: Use `waitForResponse`, not `waitForTimeout`
- ✅ **No Conditionals**: Tests execute same path every time
- ✅ **<300 Lines**: Keep tests focused, split or extract to fixtures
- ✅ **<1.5 Minutes**: Optimize with API setup, parallel operations
- ✅ **Self-Cleaning**: Use fixtures with auto-cleanup
- ✅ **Explicit Assertions**: Keep `expect()` in test bodies
- ✅ **Unique Data**: Use `faker` for dynamic data
- ✅ **Parallel-Safe**: Tests don't share state

---

## 7. Gate Decision Criteria

### 7.1 Testability Gate (Phase 3 → Phase 4)

**Decision**: ⚠️ **CONCERNS** (Conditional Pass)

**Rationale**:
- ✅ Architecture supports robust testing (clear separation, deterministic state)
- ⚠️ 1 critical risk (RISK-001) requires mitigation before E2E tests
- ⚠️ 2 high risks (RISK-002, RISK-003) require mitigation plans
- ✅ Test levels strategy defined and aligned with architecture
- ✅ NFR testing approach comprehensive

**Conditions for PASS**:
1. **RISK-001 Mitigation**: Implement test-specific polling intervals and manual refresh triggers
2. **Test Infrastructure Setup**: Initialize Playwright, Jest, k6, test database
3. **Fixture Creation**: Implement data factories and persona fixtures

**Recommendations**:
- Address RISK-001 in Epic 1 (Project Foundation) before E2E test implementation
- Create test infrastructure setup story in Epic 1
- Review and approve test design before proceeding to implementation

### 7.2 Next Steps

1. **User Review**: Review this test design document
2. **Risk Mitigation**: Address RISK-001 in implementation plan
3. **Test Infrastructure**: Set up Playwright, Jest, k6 in Epic 1
4. **Implementation**: Proceed to Phase 4 (Implementation) with test-first approach

---

## 8. Appendix

### 8.1 Test Tool Stack

| Tool | Purpose | Justification |
|------|---------|---------------|
| **Playwright** | E2E, Integration (API), Component | Multi-browser support, network interception, fast execution |
| **Jest** | Unit testing | Standard React testing tool, fast, TypeScript support |
| **React Testing Library** | Component testing | User-centric testing, accessibility-focused |
| **k6** | Performance/load testing | Realistic load simulation, SLO validation |
| **axe-core** | Accessibility testing | Industry-standard a11y validation |
| **Lighthouse CI** | Performance/SEO validation | Core Web Vitals, automated audits |

### 8.2 Test Coverage Targets

| Level | Target | Rationale |
|-------|--------|-----------|
| **Unit** | 80%+ | High coverage for business logic |
| **Integration** | 70%+ | API contracts, database operations |
| **E2E** | Critical paths only | Expensive, focus on user journeys |
| **Overall** | 80%+ | Industry standard for production apps |

### 8.3 References

- [Architecture Document](file:///d:/Repositories/portfolio/bmad/_bmad-output/planning-artifacts/architecture.md)
- [Product Requirements Document](file:///d:/Repositories/portfolio/bmad/_bmad-output/planning-artifacts/prd.md)
- [Epics & Stories](file:///d:/Repositories/portfolio/bmad/_bmad-output/planning-artifacts/epics.md)
- [Project Context](file:///d:/Repositories/portfolio/bmad/_bmad-output/project-context.md)
- TEA Knowledge Base: `nfr-criteria.md`, `test-levels-framework.md`, `risk-governance.md`, `test-quality.md`

---

**Document Status**: DRAFT - Awaiting User Review  
**Next Action**: User review and approval before proceeding to implementation
