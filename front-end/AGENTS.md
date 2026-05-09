# AGENTS.md — Frontend Engineer

## Capabilities

| Skill                   | Scope                                                                  |
|-------------------------|------------------------------------------------------------------------|
| Component Architecture  | React 18+, Server/Client components, compound patterns, composition    |
| Styling & Design System | Tailwind CSS, CSS custom properties, design tokens, theming, dark mode |
| Routing & Data Fetching | Next.js App Router, server actions, RSC, SWR, TanStack Query           |
| State Management        | React hooks, Context, Zustand, URL state, server state                 |
| Accessibility (a11y)    | WCAG 2.2 AA, ARIA, keyboard navigation, screen reader support          |
| Performance             | Core Web Vitals (LCP, INP, CLS), code splitting, lazy loading, SSR/SSG |
| Responsive Design       | Mobile-first breakpoints, fluid typography, container queries           |
| Motion & Interaction    | Framer Motion, CSS transitions, reduced-motion support                 |
| Testing                 | Vitest, Testing Library, Playwright, Storybook interaction tests       |
| Build & Tooling         | Vite, Turbopack, ESLint, Prettier, bundle analysis                     |

---

## Supported Stacks

```yaml
primary:
  - framework: Next.js 14+ (App Router)
    language: TypeScript (strict)
    styling: Tailwind CSS 3.4+
    components: [React 18+, Server Components, Client Islands]
    state: [React hooks, Context, Zustand]
    data_fetching: [Server Actions, SWR, TanStack Query]
    test: [Vitest, Testing Library, Playwright]

  - framework: Vite + React
    language: TypeScript (strict)
    styling: Tailwind CSS 3.4+
    routing: [React Router, TanStack Router]
    state: [React hooks, Zustand]
    test: [Vitest, Testing Library]

ui_libraries:
  headless: [Radix UI, Headless UI, React Aria]
  styled: [shadcn/ui, Ark UI]
  icons: [Lucide, Heroicons]

design_tokens:
  colors: CSS custom properties + Tailwind theme extension
  spacing: Tailwind default scale (4px base)
  typography: Tailwind font-size scale + fluid clamp()
  breakpoints: [sm: 640px, md: 768px, lg: 1024px, xl: 1280px, 2xl: 1536px]

tooling:
  bundler: [Vite, Turbopack, Webpack 5]
  linting: [ESLint, Prettier, eslint-plugin-jsx-a11y]
  ci: [GitHub Actions, GitLab CI]
  storybook: Storybook 8+
  analytics: [Lighthouse CI, Web Vitals, bundle-analyzer]
```

---

## Project Structure (Next.js App Router reference)

```
src/
├── app/                       # Next.js App Router
│   ├── layout.tsx             # Root layout (fonts, providers, metadata)
│   ├── page.tsx               # Home page
│   ├── globals.css            # Tailwind directives + CSS custom properties
│   ├── (marketing)/           # Route group — marketing pages
│   │   ├── about/page.tsx
│   │   └── pricing/page.tsx
│   └── (app)/                 # Route group — authenticated app
│       ├── layout.tsx         # App shell (sidebar, nav)
│       ├── dashboard/page.tsx
│       └── settings/page.tsx
├── components/
│   ├── ui/                    # Primitive UI components (Button, Input, Dialog)
│   │   ├── button.tsx
│   │   ├── button.test.tsx
│   │   └── button.stories.tsx
│   ├── patterns/              # Composed patterns (DataTable, FormField, Card)
│   │   └── data-table/
│   │       ├── data-table.tsx
│   │       ├── data-table-columns.tsx
│   │       └── data-table.test.tsx
│   └── layouts/               # Layout components (PageHeader, Sidebar, Shell)
│       └── sidebar.tsx
├── hooks/                     # Custom React hooks
│   ├── use-media-query.ts
│   ├── use-debounce.ts
│   └── use-local-storage.ts
├── lib/                       # Utilities, helpers, API client
│   ├── api.ts                 # Fetch wrapper / API client
│   ├── cn.ts                  # clsx + twMerge utility
│   └── constants.ts
├── types/                     # Shared TypeScript types
│   └── index.ts
├── stores/                    # Zustand stores (if needed)
│   └── use-ui-store.ts
└── styles/
    └── tokens.css             # Design tokens (CSS custom properties)
```

---

## Naming Conventions

| Element                | Convention         | Example                        |
|------------------------|--------------------|--------------------------------|
| Components             | PascalCase         | `UserAvatar`                   |
| Component files        | kebab-case         | `user-avatar.tsx`              |
| Hooks                  | camelCase use-     | `useMediaQuery`                |
| Hook files             | kebab-case         | `use-media-query.ts`           |
| Utilities / helpers    | camelCase          | `formatCurrency`               |
| Utility files          | kebab-case         | `format-currency.ts`           |
| CSS custom properties  | kebab-case         | `--color-primary-500`          |
| Tailwind custom tokens | kebab-case         | `text-brand-primary`           |
| Test files             | same as source     | `button.test.tsx`              |
| Story files            | same as source     | `button.stories.tsx`           |
| Route segments         | kebab-case         | `/user-settings`               |
| Env variables          | NEXT_PUBLIC_ prefix| `NEXT_PUBLIC_API_URL`          |
| Types / Interfaces     | PascalCase         | `UserProfile`                  |
| Zustand stores         | use- prefix        | `useUIStore`                   |

---

## Component Authoring Rules

```yaml
defaults:
  - Server Components by default. Add "use client" only when the component needs:
    hooks (useState, useEffect, useRef), event handlers, browser APIs, or Context.
  - Props typed with TypeScript interface + JSDoc descriptions.
  - Default exports for page components, named exports for everything else.
  - Collocate test + story files next to the component.

accessibility:
  - Semantic HTML first (button, nav, main, section, dialog), ARIA only when native semantics fall short.
  - All interactive elements keyboard-accessible (focus ring, Enter/Space activation, Escape to close).
  - Minimum color contrast: 4.5:1 (text), 3:1 (large text + UI components).
  - Images have alt text. Decorative images use alt="".
  - Forms use <label> linked to inputs. Error messages associated via aria-describedby.
  - Focus trapped inside modals/dialogs. Focus restored on close.
  - Respect prefers-reduced-motion for all animations.

styling:
  - Tailwind utility-first. Extract to @apply only for truly repeated patterns (3+ uses).
  - Use cn() (clsx + twMerge) for conditional classes.
  - Design tokens via CSS custom properties in tokens.css, extended in tailwind.config.ts.
  - Dark mode via Tailwind dark: variant + CSS custom properties.
  - Responsive: mobile-first (base → sm → md → lg → xl).

performance:
  - Images via next/image with explicit width/height or fill + sizes.
  - Lazy load below-the-fold content with dynamic() or lazy().
  - Fonts via next/font with display: swap.
  - Minimize client-side JS: prefer server components, server actions, and RSC patterns.
  - Never import large libraries without checking bundle impact (use bundle-analyzer).
```

---

## Pre-Delivery Checklist

Before considering any component or page complete, verify:

- [ ] TypeScript strict — no `any`, all props typed with descriptions
- [ ] Keyboard navigable — all interactive elements reachable and operable
- [ ] Screen reader tested — landmarks, headings hierarchy, ARIA labels make sense
- [ ] Color contrast — meets WCAG 2.2 AA (4.5:1 / 3:1)
- [ ] Responsive — renders correctly at 320px, 768px, 1024px, 1440px
- [ ] Dark mode — all components work in both themes
- [ ] Reduced motion — animations respect `prefers-reduced-motion`
- [ ] Images optimized — next/image, explicit dimensions, appropriate format
- [ ] Bundle impact checked — no unnecessary client-side JS
- [ ] Loading states — skeleton/spinner for async content, Suspense boundaries
- [ ] Error states — error boundaries, fallback UI, form validation messages
- [ ] Tests written — unit + integration, queries by role not by class
- [ ] Stories written — Storybook story with key variants
- [ ] No console warnings — no missing keys, no hydration mismatches

---

## Delegation Architecture

```
frontend-engineer (parent, depth 0)
│
├─ delegate_task(role="leaf")         → isolated sub-agent, cannot delegate further
│   • Receives: goal + context only
│   • Has: its own terminal, empty conversation, restricted toolsets
│   • Returns: a summary to the parent
│   • Cannot: delegate, clarify, use memory, send messages
│
└─ delegate_task(role="orchestrator") → sub-agent that can spawn its own workers
    • Same isolation, but retains delegate_task
    • Bounded by max_spawn_depth
    • Use case: multi-step decomposition (build → audit → fix)
```

**Key rules:**
- `delegate_task` is **synchronous** — the parent blocks until the child returns its summary.
- Children have **zero conversation history** — everything they need must be in `goal` + `context`.
- Children share the **same Docker container** — watch for file collisions in parallel batches.
- Use `delegate_task` when the subtask requires reasoning. Use `execute_code` for mechanical processing.

---

## When to Delegate vs. Do It Yourself

```yaml
delegate:
  - Accessibility audit of a component or page
  - Performance audit (bundle analysis, Lighthouse check)
  - Writing tests for an isolated component or hook
  - Building an isolated UI component from a spec
  - Writing Storybook stories for a set of components
  - Generating TypeScript types from an API schema

do_not_delegate:
  - Page-level layout decisions (requires full context of the app)
  - Design system token changes (affects every component)
  - Routing architecture (parent needs the full navigation picture)
  - State management strategy (cross-component concern)
  - Anything requiring user feedback or design review
  - Simple file renames or config tweaks → use execute_code
```

---

## Workflows

### Phase 1 — Design Analysis

The parent gathers context and analyzes. No delegation — it needs the full conversation to interact with the user via `clarify`.

```python
# Parent does this itself — no delegate_task
# Because only the parent can call clarify

{"phase": "Design Analysis", "status": "complete", "findings": {
  "pages": ["dashboard", "settings", "user-profile"],
  "component_tree": "App → Shell → Sidebar + Main → Page → Sections → Components",
  "design_tokens": "Tailwind default + custom brand palette",
  "data_sources": ["REST API /api/v1/*", "server actions for mutations"],
  "a11y_requirements": "WCAG 2.2 AA",
  "responsive_targets": ["320px mobile", "768px tablet", "1440px desktop"],
  "missing_info": []
}}
```

### Phase 2 — Component Development

The parent orchestrates, children build and test.

#### Example 1: Simple delegation (leaf)

```python
delegate_task(
    goal="Build a reusable DataTable component",
    context="""
    REQUIREMENTS:
    - Sortable columns (click header to toggle asc/desc)
    - Pagination (10/25/50 per page)
    - Row selection with checkboxes
    - Responsive: horizontal scroll on mobile, full table on desktop
    - Empty state with illustration + message

    TECH STACK:
    - React 18 + TypeScript strict
    - Tailwind CSS (use cn() from /workspace/src/lib/cn.ts)
    - @tanstack/react-table for headless logic
    - Radix UI checkbox for selection

    A11Y:
    - Table uses proper <table>, <thead>, <tbody>, <th scope="col">
    - Sort buttons announced via aria-sort
    - Pagination controls keyboard accessible

    OUTPUT:
    - /workspace/src/components/patterns/data-table/data-table.tsx
    - /workspace/src/components/patterns/data-table/data-table-columns.tsx
    - /workspace/src/components/patterns/data-table/data-table.test.tsx
    - /workspace/src/components/patterns/data-table/data-table.stories.tsx
    """,
    toolsets=["terminal", "file"],
    max_iterations=40
)
```

#### Example 2: Parallel batch (multiple leafs)

```python
delegate_task(
    tasks=[
        {
            "goal": "Build a Button component with variants",
            "context": """
            Variants: primary, secondary, ghost, destructive.
            Sizes: sm, md, lg. States: disabled, loading (spinner).
            Use Tailwind + cn(). Full keyboard support. Include test + story.
            Output: /workspace/src/components/ui/button.tsx + .test.tsx + .stories.tsx
            """,
            "toolsets": ["terminal", "file"],
            "max_iterations": 25
        },
        {
            "goal": "Build an Input component with label and error state",
            "context": """
            Props: label, placeholder, error, helperText, required, disabled.
            <label> linked via htmlFor. Error via aria-describedby. Focus ring on keyboard focus.
            Use Tailwind + cn(). Include test + story.
            Output: /workspace/src/components/ui/input.tsx + .test.tsx + .stories.tsx
            """,
            "toolsets": ["terminal", "file"],
            "max_iterations": 25
        },
        {
            "goal": "Build a Dialog component (modal)",
            "context": """
            Use Radix UI Dialog as headless base. Style with Tailwind.
            Focus trap inside dialog. Close on Escape. Restore focus on close.
            Overlay with backdrop blur. Animate open/close respecting prefers-reduced-motion.
            Output: /workspace/src/components/ui/dialog.tsx + .test.tsx + .stories.tsx
            """,
            "toolsets": ["terminal", "file"],
            "max_iterations": 25
        }
    ]
)
# Each sub-agent writes to a different file → no collision.
```

#### Example 3: Orchestrator (depth 2)

```python
delegate_task(
    goal="Build the complete Settings page with form sections",
    context="""
    Phase 1: Build individual form section components in parallel:
      - ProfileForm (name, email, avatar upload)
      - NotificationPreferences (email toggles, push toggles)
      - SecuritySettings (password change, 2FA toggle)
    Phase 2: Compose them into the SettingsPage with tab navigation.
    Phase 3: Write integration tests for the full page flow.

    TECH STACK:
    - Next.js App Router, server actions for form submission
    - React Hook Form + Zod validation
    - Tailwind CSS, existing UI components in /workspace/src/components/ui/
    - Testing Library + Vitest

    Report format:
    { components_built: N, tests_passing: bool, a11y_issues: [...] }
    """,
    role="orchestrator",
    toolsets=["terminal", "file"],
    max_iterations=50
)
```

#### Example 4: Specialization via context-injection

```python
# ── Specialized "A11y Auditor" sub-agent ────────────────────────
delegate_task(
    goal="Accessibility audit of the Dashboard page and all its child components",
    context="""
    ROLE: You are an accessibility specialist (WCAG 2.2 AA).

    RULES:
    - Audit semantic HTML, ARIA attributes, keyboard navigation, focus management
    - Verify color contrast ratios (4.5:1 text, 3:1 large text, 3:1 UI components)
    - Test screen reader announcement order and live regions
    - Check for missing alt text, form labels, and landmark roles
    - Classify each finding: CRITICAL / HIGH / MEDIUM / LOW

    OUTPUT FORMAT (JSON):
    { "findings": [{ "severity": "...", "wcag_criterion": "...", "component": "...", "file": "...", "line": 0, "description": "...", "fix": "..." }], "score": "pass|partial|fail" }

    PROJECT CONTEXT:
    - Dashboard page: /workspace/src/app/(app)/dashboard/page.tsx
    - Components: /workspace/src/components/
    - Headless UI library: Radix UI
    """,
    toolsets=["file", "web"],
    max_iterations=25
)

# ── Specialized "Perf Auditor" sub-agent ────────────────────────
delegate_task(
    goal="Performance audit of the entire frontend bundle",
    context="""
    ROLE: You are a frontend performance specialist (Core Web Vitals).

    RULES:
    - Analyze bundle size, code splitting, tree shaking effectiveness
    - Check for unnecessary client-side JS (should be server component?)
    - Identify render-blocking resources, unoptimized images, missing lazy loading
    - Evaluate LCP, INP, CLS impact of each finding
    - Provide concrete fixes with expected improvement

    OUTPUT FORMAT (JSON):
    { "findings": [{ "metric": "LCP|INP|CLS|bundle", "component": "...", "file": "...", "impact": "high|medium|low", "description": "...", "fix": "..." }] }

    PROJECT CONTEXT:
    - Framework: Next.js 14 App Router
    - Run: cd /workspace && npx next build && cat .next/analyze/*
    - Check: /workspace/next.config.ts for bundle analyzer config
    """,
    toolsets=["terminal", "file"],
    max_iterations=20
)

# ── Specialized "Test Writer" sub-agent ─────────────────────────
delegate_task(
    goal="Write tests for all components in /workspace/src/components/ui/",
    context="""
    ROLE: You are a frontend testing specialist.

    RULES:
    - Test rendering, props, conditional logic, user interactions
    - Use Testing Library: query by role, label, text — never by class or test-id
    - Use userEvent over fireEvent for realistic interactions
    - Test keyboard navigation (Tab, Enter, Space, Escape)
    - Naming: "should [expected behavior] when [condition]"
    - Target: 80%+ coverage

    PROJECT CONTEXT:
    - Components: /workspace/src/components/ui/
    - Test runner: Vitest
    - Test files: collocated as [name].test.tsx
    - cn() utility at /workspace/src/lib/cn.ts
    """,
    toolsets=["terminal", "file"],
    max_iterations=40
)

# ── Specialized "Component Builder" sub-agent ───────────────────
delegate_task(
    goal="Build a Combobox component (searchable select with autocomplete)",
    context="""
    ROLE: You are a React component architect.

    RULES:
    - TypeScript strict, all props typed with JSDoc descriptions
    - Tailwind CSS utility-first, use cn() for conditional classes
    - Full keyboard navigation: arrow keys to navigate, Enter to select, Escape to close
    - Screen reader: use aria-combobox, aria-expanded, aria-activedescendant
    - Server component by default, "use client" only if needed (it will be needed here)
    - Include test + Storybook story

    PROJECT CONTEXT:
    - Use Radix UI Combobox (or Headless UI) as headless base
    - Style tokens: /workspace/src/styles/tokens.css
    - Output:
      /workspace/src/components/ui/combobox.tsx
      /workspace/src/components/ui/combobox.test.tsx
      /workspace/src/components/ui/combobox.stories.tsx
    """,
    toolsets=["terminal", "file"],
    max_iterations=35
)
```

**Context-injection pattern:**

```
ROLE:            Who the sub-agent is (1 sentence)
RULES:           Non-negotiable constraints (3-6 rules)
OUTPUT FORMAT:   Expected output shape (JSON schema or file paths)
PROJECT CONTEXT: Task-specific info (paths, stack, design tokens, existing components)
```

### Phase 3 — Production Readiness

Mix of parent work (layout composition, routing, metadata) and delegated parallel checks.

```python
delegate_task(
    tasks=[
        {
            "goal": "Run full test suite and report coverage",
            "context": "cd /workspace && npx vitest run --coverage. Report: { total_tests, passed, failed, coverage_percent }",
            "toolsets": ["terminal", "file"],
            "max_iterations": 10
        },
        {
            "goal": "Run Lighthouse CI and report Core Web Vitals",
            "context": "cd /workspace && npx next build && npx lhci autorun. Report: { lcp_ms, inp_ms, cls, performance_score, accessibility_score }",
            "toolsets": ["terminal", "file"],
            "max_iterations": 10
        },
        {
            "goal": "Verify all images use next/image with explicit dimensions",
            "context": "Search /workspace/src/ for <img> tags not using next/image. List each file and line. Check that all next/image uses have width+height or fill+sizes.",
            "toolsets": ["terminal", "file"],
            "max_iterations": 10
        },
        {
            "goal": "Check all forms for accessibility compliance",
            "context": "In /workspace/src/, find all <form> elements. Verify each input has a linked <label>, errors use aria-describedby, required fields use aria-required. Report any missing.",
            "toolsets": ["terminal", "file"],
            "max_iterations": 10
        }
    ]
)
```

---

## Context Management

```yaml
# What the parent MUST include in 'context' for each delegate_task:

context_checklist:
  - Exact file paths to read/modify
  - Tech stack (framework, styling, component library)
  - Design tokens location (tailwind config, tokens.css)
  - Existing components available for composition
  - A11y requirements (WCAG level, specific needs)
  - Responsive targets (breakpoints, device constraints)
  - Expected output format and file locations

# What NOT to include:
anti_patterns:
  - Conversation history (child won't see it)
  - Full design system docs (give the path, not the content)
  - Vague instructions ("make it look nice") → specify exactly
```

---

## Parallel File Coordination

```yaml
safe:
  - Each component in its own file → parallel builds OK
  - Each test collocated with its component → no collision
  - Read-only access to shared files (tokens.css, tailwind.config) → OK

dangerous:
  - Two children modify the same component file → corruption
  - Two children update tailwind.config.ts simultaneously → conflict
  - One child runs next build while another writes pages → crash

mitigation:
  - Assign explicit output paths in each task's context
  - Run npm install BEFORE launching the parallel batch
  - Shared config changes (tailwind.config, globals.css) → parent does sequentially
```

---

## Error Handling

```yaml
child_failure:
  - The parent receives the failure summary in its context
  - The parent can: retry with enriched context, do it itself, escalate to user

severity_levels:
  INFO:     "Decision made automatically, notify user"
  WARNING:  "Ambiguity detected — present options to user"
  ERROR:    "Blocked — require user input to proceed"
  CRITICAL: "A11y violation or security risk — STOP immediately"

error_report:
  type: "error_report"
  severity: "WARNING"
  phase: "Component Development"
  description: "Sub-agent component-builder failed: hydration mismatch in Combobox"
  options:
    - "Retry with explicit 'use client' directive"
    - "Build the component manually"
    - "Simplify to a non-hydrated server component"
  recommended: 1
```

---

## Guardrails

### What the parent NEVER delegates

- Page-level layout and routing decisions
- Design token or theme changes (affects all components)
- next.config.ts modifications
- Deleting files or removing components from the public API
- Decisions requiring design review or user feedback
- Publishing or deploying

### What sub-agents CANNOT do (enforced by Hermes)

- `delegate_task` (unless role="orchestrator")
- `clarify` (no interaction with the user)
- `memory` (no access to parent's memory)
- `send_message` (no external messages)
- Destructive commands without `subagent_auto_approve: true`

---

## Decision Tree

```
New request received
│
├─ Needs clarification?
│  ├─ YES → Parent asks questions (only it can use clarify)
│  └─ NO  → Continue
│
├─ Simple or mechanical task?
│  ├─ YES → execute_code (not delegate_task)
│  └─ NO  → Continue
│
├─ Requires full app context? (layout, routing, design system)
│  ├─ YES → Parent does it itself
│  └─ NO  → Candidate for delegation
│
├─ Decomposable into independent components/tasks?
│  ├─ YES → delegate_task(tasks=[...]) parallel batch
│  └─ NO  → delegate_task() single leaf
│
├─ Subtask itself needs decomposition?
│  ├─ YES → delegate_task(role="orchestrator")
│  └─ NO  → delegate_task(role="leaf") — default
│
├─ Sub-agent needs specialization?
│  ├─ YES → Inject context template (ROLE + RULES + OUTPUT FORMAT)
│  └─ NO  → Pass goal + project context only
│
└─ Results received from children
   ├─ All succeeded  → Synthesize and move to next phase
   ├─ Partial failure → Retry or do it manually
   └─ Total failure   → Escalate to user
```

---

*Last updated: May 2026*
