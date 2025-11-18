# 🎯 Pragmatic TypeScript: Ship First, Perfect Later

## The Manifesto

**Perfect types are not the goal. Shipping is the goal.**

- **Vibe code with `any` that works > Broken code with perfect types**
- **Refine incrementally, not all at once**
- **Always test after each refine stage**
- **When in doubt, be more permissive with types**
- **It's OK to have some `any` in your codebase**

> Remember: TypeScript is a tool to help you, not a religion. Use it pragmatically.
> 
> The best refine is the one that makes your code slightly better without breaking anything. 🎯

---

## The Philosophy

TypeScript is a powerful tool, but it's just that—a **tool**. This guide embraces a pragmatic approach to TypeScript that prioritizes shipping working code over achieving type perfection.

## Core Principles

### 1. 🚀 Vibe Code > Broken Code

```typescript
// ✅ GOOD: Works, ships, helps users
function processData(data: any): any {
  return data.map(item => item.value);
}

// ❌ BAD: Perfect types but blocked for days
// (Still trying to figure out the exact generic constraints...)
```

**Vibe code with `any` that works > Broken code with perfect types**

### 2. 🔄 Refine Incrementally, Not All at Once

Don't try to fix all types in one massive PR. Instead:

```typescript
// Stage 1: Get it working
function getUserData(id: any): any {
  return fetch(`/api/users/${id}`).then(r => r.json());
}

// Stage 2: Add basic types (later)
interface User {
  id: string;
  name: string;
}

function getUserData(id: string): Promise<User> {
  return fetch(`/api/users/${id}`).then(r => r.json());
}

// Stage 3: Add validation (when needed)
function getUserData(id: string): Promise<User> {
  return fetch(`/api/users/${id}`)
    .then(r => r.json())
    .then(data => validateUser(data));
}
```

### 3. ✅ Always Test After Each Refine Stage

**The Golden Rule:** Every incremental type improvement must be followed by testing.

```bash
# After each refine stage:
npm test
npm run build
npm run lint

# If it breaks, you refined too much at once
# Roll back and take smaller steps
```

### 4. 🎨 When in Doubt, Be More Permissive

```typescript
// ✅ GOOD: Permissive, won't block development
interface Config {
  apiUrl: string;
  timeout?: number;
  [key: string]: any; // Allow extra properties
}

// ❌ AVOID: Too strict, will cause friction
interface Config {
  apiUrl: string;
  timeout?: number;
  // No extra properties allowed - might break things
}
```

### 5. 🤝 It's OK to Have Some `any` in Your Codebase

Strategic use of `any` is perfectly acceptable:

```typescript
// ✅ OK: Third-party library with no types
const weirdLib: any = require('some-untyped-legacy-lib');

// ✅ OK: Temporary placeholder during prototyping
function experimentalFeature(params: any) {
  // TODO: Refine types after we validate the approach
}

// ✅ OK: Genuinely dynamic data
function handleWebhook(payload: any) {
  // Webhooks can have various shapes
  console.log(payload);
}

// ❌ AVOID: Lazy typing when you know the shape
function getUser(): any { // Should at least have basic interface
  return { id: 1, name: "John" };
}
```

## The Pragmatic Workflow

### Stage 1: Make It Work 💚
- Use `any` liberally
- Focus on functionality
- Get tests passing
- Ship to production

### Stage 2: Make It Type-Safe 🟡
- Add basic interfaces
- Type function signatures
- Replace obvious `any` uses
- Test after each change

### Stage 3: Make It Refined 💙
- Add generics where helpful
- Improve union types
- Add strict null checks
- Consider edge cases

### Stage 4: Make It Bulletproof 💜
- Add runtime validation
- Implement error boundaries
- Add comprehensive types
- Document complex types

**Remember:** You can stop at any stage! Not everything needs to reach Stage 4.

## Common Scenarios

### Scenario: Adding a New Feature

```typescript
// Day 1: Ship it! 🚀
function newFeature(input: any): any {
  // Implementation that works
  return processInput(input);
}

// Week 2: Refine (if needed) 🔧
interface FeatureInput {
  userId: string;
  options: any; // Still OK!
}

function newFeature(input: FeatureInput): Promise<Result> {
  return processInput(input);
}
```

### Scenario: Refactoring Existing Code

```typescript
// Before: Working code
function calculate(a, b) {
  return a + b;
}

// Don't jump to this:
function calculate<T extends number | bigint>(
  a: T,
  b: T
): T extends number ? number : bigint {
  return (a + b) as any;
}

// Instead, do this:
function calculate(a: number, b: number): number {
  return a + b;
}

// Later, if needed:
function calculate(a: number | bigint, b: number | bigint) {
  return a + b;
}
```

### Scenario: Working with External APIs

```typescript
// ✅ GOOD: Pragmatic approach
interface ApiResponse {
  data: any; // We don't control the API shape
  status: number;
  message?: string;
}

async function fetchData(): Promise<ApiResponse> {
  const response = await fetch('/api/data');
  return response.json();
}

// Use runtime validation instead of complex types
function isValidData(data: any): boolean {
  return data && typeof data.id === 'string';
}
```

## Warning Signs You're Over-Typing

- 🚨 You've spent more than 30 minutes on types for a simple function
- 🚨 You're writing custom type guards for everything
- 🚨 You have more type code than actual logic
- 🚨 You're using `as unknown as X` frequently
- 🚨 Your PR is blocked because of type issues
- 🚨 New team members are confused by your types

## When to Be More Strict

Be more strict with types when:

- ✅ Working on critical business logic
- ✅ Building public APIs
- ✅ Creating reusable libraries
- ✅ Preventing common bugs (null checks, etc.)
- ✅ You have time and it's not blocking progress

## The Ultimate Test

Ask yourself:

1. **Does it work?** ✅
2. **Does it ship?** ✅
3. **Can others understand it?** ✅
4. **Is it tested?** ✅

If yes to all four, you're done! Perfect types can wait.

## Anti-Patterns to Avoid

```typescript
// ❌ Type gymnastics that nobody understands
type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

// ❌ Over-engineering simple things
type StringOrNumber = string | number;
type MaybeArray<T> = T | T[];
type Nullable<T> = T | null | undefined;
type AsyncMaybe<T> = Promise<Nullable<MaybeArray<T>>>;

// ✅ Simple, clear, works
function getData(): Promise<string[]> {
  // Implementation
}
```

## Quick Reference

| Situation | Approach |
|-----------|----------|
| New feature | Start with `any`, refine later |
| Bug fix | Don't change types unless necessary |
| Refactoring | One small type improvement at a time |
| External API | Use `any` or basic interface |
| Prototype | `any` everywhere is fine |
| Production code | Add basic types, test thoroughly |
| Critical path | Consider strict types + validation |
| Time pressure | Ship first, types later |

## Mantras to Live By

1. **"If it works, it works"** - Don't fix what isn't broken
2. **"Ship early, ship often"** - Types can be improved in follow-ups
3. **"Progress > Perfection"** - Some types are better than no code
4. **"Test, don't guess"** - Runtime tests > compile-time guarantees
5. **"Future you will thank present you"** - For shipping, not for perfect types

## Resources

- When you DO want to improve types gradually:
  - Use `// @ts-expect-error` for known issues
  - Use `// TODO: improve types` comments
  - Create issues for type improvements (not blockers!)
  
- TypeScript config for pragmatic projects:
```json
{
  "compilerOptions": {
    "strict": false,           // Start here
    "noImplicitAny": false,    // Allow any
    "strictNullChecks": false, // Be permissive
    "skipLibCheck": true       // Save time
  }
}
```

## Conclusion

TypeScript should accelerate your development, not block it. Use types as a helpful guide, not a strict enforcer. Ship working code, then improve it incrementally.

**Happy shipping! 🚀**

---

*Remember: The best code is the code that ships and solves real problems.*