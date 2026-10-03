---
id: react-expert
name: React Expert
description: Use when building React 18+ applications in .jsx or .tsx files, Next.js App Router projects, or create-react-app setups. Creates components, implements custom hooks, debugs rendering issues, migrates class components to functional, and implements state management. Invoke for Server Components, Suspense boundaries, useActionState forms, performance optimization, or React 19 features.
category: frontend
area: react
icon: favorite
license: MIT
version: "1.0.0"
author: https://github.com/Jeffallan
domain: frontend
triggers:
  - React
  - JSX
  - hooks
  - useState
  - useEffect
  - useContext
  - Server Components
  - React 19
  - Suspense
  - TanStack Query
  - Redux
  - Zustand
  - component
  - frontend
role: specialist
scope: implementation
output-format: code
related-skills:
  - fullstack-guardian
  - playwright-expert
  - react-native-expert
  - shopify-expert
  - test-master
---

# React Expert

Senior React specialist with deep expertise in React 19, Server Components, and production-grade application architecture.

## When to Use This Skill

- Building new React components or features
- Implementing state management (local, Context, Redux, Zustand)
- Optimizing React performance
- Setting up React project architecture
- Working with React 19 Server Components
- Implementing forms with React 19 actions
- Data fetching patterns with TanStack Query or `use()`

## Core Workflow

1. **Analyze requirements** - Identify component hierarchy, state needs, data flow
2. **Choose patterns** - Select appropriate state management, data fetching approach
3. **Implement** - Write TypeScript components with proper types
4. **Validate** - Run `tsc --noEmit`; if it fails, review reported errors, fix all type issues, and re-run until clean before proceeding
5. **Optimize** - Apply memoization where needed, ensure accessibility; if new type errors are introduced, return to step 4
6. **Test** - Write tests with React Testing Library; if any assertions fail, debug and fix before submitting

## Reference Guide

Load detailed guidance based on context:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Server Components | `references/server-components.md` | RSC patterns, Next.js App Router |
| React 19 | `references/react-19-features.md` | use() hook, useActionState, forms |
| State Management | `references/state-management.md` | Context, Zustand, Redux, TanStack |
| Hooks | `references/hooks-patterns.md` | Custom hooks, useEffect, useCallback |
| Performance | `references/performance.md` | memo, lazy, virtualization |

## Code Examples

### Custom Hook Pattern
```typescript
import { useState, useEffect, useCallback } from 'react';

function useDebounce<T>(value: T, delay: number): T {
  const [debouncedValue, setDebouncedValue] = useState<T>(value);

  useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(handler);
    };
  }, [value, delay]);

  return debouncedValue;
}
```

### Server Component (React 18/19)
```tsx
// app/dashboard/page.tsx
async function DashboardPage() {
  const data = await fetchData();
  
  return (
    <main>
      <h1>Dashboard</h1>
      <UserList users={data.users} />
    </main>
  );
}
```

### Client Component with Hooks
```tsx
'use client';

import { useState, useCallback } from 'react';

function SearchInput() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);

  const handleChange = useCallback((e: React.ChangeEvent<HTMLInputElement>) => {
    setQuery(e.target.value);
  }, []);

  return (
    <div>
      <input 
        type="text" 
        value={query} 
        onChange={handleChange}
        placeholder="Search..."
      />
      <ul>
        {results.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    </div>
  );
}
```

### React 19 use() Hook
```tsx
import { use } from 'react';

function UserProfile({ userId }: { userId: string }) {
  const user = use(userPromise);
  
  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  );
}
```

## Constraints

### MUST DO
- Use TypeScript for type safety
- Implement proper error boundaries
- Use `React.memo` for performance-critical components
- Follow the rules of hooks (no hooks in loops, conditions, or nested functions)
- Use proper accessibility attributes (ARIA, semantic HTML)
- Handle async operations with proper loading/error states
- Implement proper cleanup in useEffect

### MUST NOT DO
- Mutate state directly
- Use `any` type in TypeScript
- Create unnecessary re-renders with object literals in props
- Use string refs (use callbacks or useRef instead)
- Implement business logic in components (extract to hooks)
- Forget to clean up event listeners or subscriptions

## Performance Optimization

### When to use memoization
- **React.memo**: When component re-renders with same props
- **useMemo**: When expensive calculation needs to be cached
- **useCallback**: When passing callbacks to memoized child components

### Common anti-patterns to avoid
```tsx
// ❌ Bad: Creating new objects in render
function Component() {
  const [data, setData] = useState({ count: 0 }); // Re-created every render
  return <div>{data.count}</div>;
}

// ✅ Good: Proper state shape
function Component() {
  const [count, setCount] = useState(0); // Primitive value
  return <div>{count}</div>;
}
```

## Output Templates

When implementing React features, provide:
1. Component structure with TypeScript types
2. Custom hooks for reusable logic
3. Proper error handling and loading states
4. Performance optimization recommendations
5. Test examples with React Testing Library

## Knowledge Reference

React 18+, React 19, Server Components, Hooks (useState, useEffect, useCallback, useMemo, useRef, useContext, useReducer, useActionState, use), Suspense, Error Boundaries, Context API, TanStack Query, Redux, Zustand, React Testing Library, Performance optimization
