# Junior React Developer Checklist

> Comprehensive skills checklist with personal assessment based on interview and learning progress. Goal: Junior+ Frontend Developer in 5-6 months

---

## 📊 Legend

|Symbol|Meaning|
|---|---|
|✅|Confident — can explain and apply|
|🟡|Partial — understands concept, needs practice|
|🔴|Gap — needs to learn/practice|
|⭐|Interview favorite — frequently asked|

---

## 1. JavaScript Core

### 1.1 Variables & Scope

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|var / let / const differences|Explain + examples|✅|Strong understanding including hoisting|
|Hoisting mechanism|Explain behavior|✅|Knows TDZ (Temporal Dead Zone)|
|⭐ Block vs function scope|Explain + demonstrate|✅|Solid grasp|
|⭐ Temporal Dead Zone (TDZ)|Explain why it exists|✅|Mentioned in interview|

### 1.2 Data Types & References

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Primitives vs Objects|Know all types|✅|Solid|
|⭐ Pass by value vs reference|Explain + pitfalls|✅|Understands const + object mutation|
|Shallow vs deep copy|Implement both|🟡|Knows concept, needs practice|
|Type coercion (== vs ===)|Explain quirks|🟡|Basic understanding|

### 1.3 Functions

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Function declaration vs expression|Know differences|✅|Solid|
|Arrow functions|Syntax + `this` behavior|🟡|Syntax yes, `this` needs work|
|⭐ Closures|Explain + practical use|🟡|Knows purpose, lacks practice|
|⭐ `this` keyword|All binding rules|🔴|Identified gap in interview|
|Higher-order functions|map, filter, reduce|✅|Used in interview task|
|Callback functions|Create and use|✅|Solid|

### 1.4 Asynchronous JavaScript

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|⭐ Event Loop|Explain mechanism|✅|**Excellent!** Knows microtasks vs macrotasks|
|Callbacks & callback hell|Understand problem|✅|Knows why Promises exist|
|Promises|Create, chain, error handle|🟡|Theory strong, needs API practice|
|⭐ async/await|Syntax + error handling|🟡|Completed Day 3 assessment|
|Promise.all / allSettled / race|When to use each|🟡|Knows parallel execution concept|
|⭐ try/catch in async|Proper error handling|🟡|Needs more practice|
|Fetch API|GET, POST, headers, errors|🔴|Critical gap — needs immediate practice|

### 1.5 Modern JavaScript (ES6+)

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Destructuring|Objects and arrays|✅|Used in code|
|Spread / Rest operators|All use cases|✅|Solid|
|Template literals|Basic usage|✅|Solid|
|Optional chaining (?.)|Usage and gotchas|🟡|Knows syntax|
|Nullish coalescing (??)|Difference from \||🟡|Needs practice|
|ES Modules (import/export)|Named, default, dynamic|✅|Used in React|

---

## 2. React Fundamentals

### 2.1 Core Concepts

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|JSX syntax|Write fluently|✅|Solid|
|⭐ Components (functional only)|Create, compose, split|✅|Strong foundation|
|Props|Pass, receive, spread|✅|Understands data flow|
|⭐ Props vs State|When to use each|✅|Clear understanding|
|Children prop|Usage patterns|✅|Basic usage|
|Conditional rendering|All patterns|✅|Good|
|⭐ Lists and keys|Why key matters|✅|Knows reconciliation reason|
|Event handling|onClick, onChange, etc.|✅|Solid|
|Controlled vs uncontrolled|When to use each|🟡|Knows concept|

### 2.2 React Hooks

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|⭐ useState|Basic + functional updates|✅|Solid|
|⭐ useEffect|Deps, cleanup, common patterns|🟡|Knows deps behavior, cleanup needs practice|
|useRef|DOM refs + mutable values|🟡|Basic understanding|
|useContext|Create + consume|🔴|Not practiced|
|useMemo|When to use, pitfalls|🔴|Knows it exists|
|useCallback|When to use, pitfalls|🔴|Knows it exists|
|useReducer|Complex state logic|🔴|Not practiced|
|⭐ Custom hooks|Extract logic, naming|🔴|Needs to learn|
|⭐ Rules of Hooks|Why order matters|✅|**Knows the mechanism!** (hook call order)|

### 2.3 React Internals (Interview Topics)

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|⭐ Virtual DOM|What and why|✅|**Excellent explanation** in interview|
|⭐ Reconciliation|How React diffs|✅|Strong understanding|
|⭐ Re-render triggers|All causes|🟡|Knows state trigger, missed parent re-render cascade|
|React.memo|Purpose and usage|🔴|Needs to learn|
|Fiber architecture|Basic awareness|🟡|Heard of it|
|Batching|How React batches updates|🟡|Basic awareness|

### 2.4 State Management

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Lifting state up|When and how|✅|Understands pattern|
|⭐ Prop drilling problem|Identify and solve|🟡|Knows concept|
|Context API|Create, provide, consume|🔴|Needs to learn|
|Zustand basics|Create store, use in components|🔴|Planned learning|
|When to use what|Local vs global state|🟡|Intuitive understanding|

### 2.5 Routing

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|React Router setup|BrowserRouter, Routes, Route|✅|Has experience|
|Link vs useNavigate|When to use each|🟡|Basic usage|
|Route parameters|useParams, dynamic routes|🟡|Basic usage|
|Protected routes|Auth guards|🔴|Needs to implement|
|Nested routes|Layouts, Outlet|🔴|Needs to learn|

---

## 3. TypeScript

### 3.1 Basics

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Type annotations|Variables, functions|🟡|Started Day 4|
|⭐ Interfaces vs type aliases|Differences, when to use|🔴|In progress|
|Union types|Create and narrow|🔴|Learning|
|Literal types|Usage patterns|🔴|Not yet|
|Type inference|When to rely on it|🔴|Learning|
|Enums|When to use, alternatives|🔴|Not yet|

### 3.2 Advanced Types

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|⭐ Generics|Basic usage|🔴|Next milestone|
|Utility types|Partial, Pick, Omit, Required|🔴|Next milestone|
|Type guards|Narrowing techniques|🔴|Future|
|Discriminated unions|State management pattern|🔴|Future|

### 3.3 TypeScript + React

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Typing props|Interface for props|🔴|Priority after basics|
|Typing state|useState with generics|🔴|Priority|
|⭐ Typing events|ChangeEvent, FormEvent, etc.|🔴|Priority|
|Typing refs|useRef with types|🔴|Future|
|Generic components|Reusable typed components|🔴|Future|

---

## 4. Data Fetching

### 4.1 Fundamentals

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|⭐ Fetch API|GET, POST, headers|🔴|Critical gap|
|Response handling|.json(), status codes|🔴|Needs practice|
|Error handling|HTTP errors vs network errors|🔴|Knows the difference theoretically|
|Loading states|UI patterns|🟡|Concept understood|
|Abort controller|Cancel requests|🔴|Not learned|

### 4.2 React Integration

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|useEffect + fetch|Basic pattern|🔴|Needs to implement|
|Race conditions|Understand and prevent|🔴|Theory only|
|Custom useFetch hook|Create reusable hook|🔴|Future goal|

### 4.3 TanStack Query (React Query)

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|useQuery basics|Simple queries|🔴|Planned|
|useMutation|Create, update, delete|🔴|Planned|
|Query invalidation|When and how|🔴|Future|
|Caching concepts|staleTime, gcTime|🔴|Future|

---

## 5. Forms

### 5.1 Native Forms

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Controlled inputs|value + onChange|✅|Basic pattern known|
|Form submission|preventDefault, data collection|🟡|Basic usage|
|Basic validation|Required, patterns|🟡|Basic|

### 5.2 React Hook Form + Zod

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|useForm basics|Register, handleSubmit|🔴|Planned|
|Zod schemas|Define validation|🔴|Planned|
|zodResolver|Connect Zod to RHF|🔴|Planned|
|Error display|formState.errors|🔴|Planned|
|TypeScript integration|Infer types from Zod|🔴|Planned|

---

## 6. Testing

### 6.1 Fundamentals

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Test types|Unit, integration, e2e|🟡|Concept known|
|AAA pattern|Arrange, Act, Assert|🔴|Not practiced|
|What to test|Priorities and strategies|🔴|Future|

### 6.2 Vitest

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Test structure|describe, it, expect|🔴|Planned for Month 4|
|Matchers|toBe, toEqual, etc.|🔴|Future|
|Mocking|vi.fn(), vi.mock()|🔴|Future|

### 6.3 React Testing Library

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Queries|getByRole, findBy, etc.|🔴|Future|
|User events|click, type|🔴|Future|
|Async testing|waitFor, findBy|🔴|Future|

---

## 7. Tooling & Development Environment

### 7.1 Package Management

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|npm / pnpm|Install, scripts, lockfiles|✅|Daily use|
|package.json|Dependencies, scripts|✅|Understands|

### 7.2 Build Tools

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Vite|Setup, dev server, build|✅|Uses regularly|
|Environment variables|.env files, VITE_ prefix|🟡|Basic awareness|

### 7.3 Code Quality

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|ESLint|Configuration, rules|🟡|Uses default|
|Prettier|Setup, format on save|🟡|Uses default|
|TypeScript strict mode|Enable and handle|🔴|Learning|

### 7.4 Version Control

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Git basics|add, commit, push, pull|✅|Daily use|
|Branching|Create, merge|🟡|Basic usage|
|Conventional commits|Message format|🔴|Not practiced|

### 7.5 Debugging

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Browser DevTools|Console, Network, Elements|🟡|Basic usage|
|⭐ React DevTools|Components, Profiler|🔴|Needs to install and use daily|
|console methods|log, table, dir, group|🟡|Basic usage|
|debugger statement|Breakpoints|🟡|Aware|

---

## 8. Security (Your Cybersecurity Advantage)

### 8.1 Frontend Security

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|⭐ XSS prevention|How React helps, dangerouslySetInnerHTML|🟡|Cybersec background helps|
|⭐ Input validation|Client-side patterns|🟡|Understands importance|
|CSRF basics|What and how to prevent|🟡|From university|
|Secure storage|localStorage limitations|🟡|Aware of risks|
|HTTPS importance|Why it matters|✅|Cybersec background|

### 8.2 Authentication

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|JWT basics|Structure, storage, expiry|🟡|Concept known|
|OAuth flow|High-level understanding|🟡|From cybersec|
|Secure token handling|Best practices|🟡|Knows pitfalls|

---

## 9. Soft Skills & Professional Development

### 9.1 Problem Solving

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Breaking down problems|Systematic approach|✅|Good analytical skills|
|Debugging methodology|Step-by-step|🟡|Needs more practice|
|Reading documentation|Effective usage|✅|Good habit|
|Asking questions|Clear, specific questions|✅|Demonstrated in sessions|

### 9.2 Communication

|Skill|Required Level|Your Level|Notes|
|---|---|---|---|
|Technical English|B2+ reading/writing|🟡|Progressing B1-B2 → C1|
|Explaining code|Clear verbal explanation|🟡|Improving through interviews|
|Code comments|When and how|🟡|Basic|

### 9.3 Learning Approach

| Skill                   | Required Level          | Your Level | Notes                          |
| ----------------------- | ----------------------- | ---------- | ------------------------------ |
| Theory-practice balance | Apply what you learn    | 🟡         | Tends to over-theorize (known) |
| Consistent practice     | Daily coding            | 🟡         | 2-6 hours daily available      |
| Note-taking             | Effective documentation | ✅          | Obsidian vault setup           |

---

## 📈 Overall Assessment Summary

### By Category

| Category           | Score | Status                                       |
| ------------------ | ----- | -------------------------------------------- |
| JavaScript Core    | 70%   | 🟡 Strong theory, async practice needed      |
| React Fundamentals | 65%   | 🟡 Basics solid, hooks/state management gaps |
| TypeScript         | 15%   | 🔴 Just started, critical to progress        |
| Data Fetching      | 10%   | 🔴 Critical gap — priority                   |
| Forms              | 25%   | 🟡 Basic patterns only                       |
| Testing            | 5%    | 🔴 Not started (Month 4 planned)             |
| Tooling            | 60%   | 🟡 Good basics, DevTools needed              |
| Security           | 50%   | 🟡 Cybersec background is an asset           |

### Overall Level

```
Current:     Junior- / Junior (border)
Target:      Junior+ (5-6 months)
Confidence:  5.5/10 for Junior position today
```

### Key Strengths (Interview Advantages)

1. ✅ Event Loop understanding — better than most Juniors
2. ✅ Virtual DOM / Reconciliation — can explain "under the hood"
3. ✅ Rules of Hooks — knows WHY, not just WHAT
4. ✅ Cybersecurity mindset — unique differentiator
5. ✅ Systematic learning approach — theory-first with good notes

### Critical Gaps (Fix First)

1. 🔴 Fetch API + async practice in React
2. 🔴 TypeScript basics (in progress)
3. 🔴 `this` keyword and closures practice
4. 🔴 React DevTools daily usage
5. 🔴 Custom hooks

---

## 🎯 Priority Action Plan

### Week 1-2: Async JavaScript (CRITICAL)

- [ ] Implement 5+ fetch examples with JSONPlaceholder
- [ ] Handle loading/error states in React
- [ ] Use Promise.all for parallel requests
- [ ] Write custom useFetch hook (even basic)

### Week 2-3: TypeScript Basics

- [ ] Complete primitive types, interfaces, type aliases
- [ ] Type existing React components
- [ ] Learn basic generics
- [ ] Enable strict mode in a project

### Week 3-4: React Patterns

- [ ] Install and use React DevTools daily
- [ ] Implement useEffect with cleanup
- [ ] Learn useContext
- [ ] Write first custom hook

### Month 2: State Management + Forms

- [ ] Zustand implementation
- [ ] React Hook Form + Zod
- [ ] Protected routes

### Month 3: Polish + Testing Basics

- [ ] Vitest setup and first tests
- [ ] Performance optimization (memo, useMemo)
- [ ] Code splitting

### Month 4-5: Portfolio + Interview Prep

- [ ] 2-3 portfolio projects
- [ ] Interview question practice
- [ ] Code review practice

---

_Last updated: January 8, 2026_ _Based on mock interview and learning sessions_