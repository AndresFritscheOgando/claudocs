# TypeScript Conventions

Primarily intended for React and Next.js projects.

## Compiler

Enable strict TypeScript mode.

`any` is prohibited.

Use this preference order:

1. Known concrete type.
2. Generic type.
3. `unknown` with explicit narrowing.
4. Never `any`.

Do not use `as any` or `// @ts-ignore`.
Fix the type or narrow the value correctly.

## Naming

- Components and exported types: `PascalCase`.
- Variables and functions: `camelCase`.
- Constants: follow local conventions; use `UPPER_SNAKE_CASE` for true global constants.
- Boolean names should read clearly, e.g. `isLoading`, `hasPermission`, `canSubmit`.

## `type` vs `interface`

- Use `interface` for object contracts intended for extension.
- Use `type` for unions, intersections, aliases, and utility compositions.
- Follow an existing project convention if it is already consistent.

## Enums

Prefer string literal unions or `as const` objects over TypeScript enums for most application code.

```ts
export const STATUS = {
  ACTIVE: "active",
  INACTIVE: "inactive",
} as const;

export type Status = (typeof STATUS)[keyof typeof STATUS];
```

## Functions

- Use named function declarations for reusable top-level behavior.
- Use arrow functions for callbacks and closures.
- Keep functions focused and explicit about inputs and outputs when inference is insufficient.

## React / Next.js

- Prefer Server Components by default in Next.js when client behavior is not required.
- Add `"use client"` only when browser APIs, client-side state, effects, or event handlers require it.
- Keep components focused on a clear UI responsibility.
- Extract repeated or complex behavior into hooks or domain utilities when that improves clarity.
- Avoid unnecessary state; derive values when possible.
- Keep loading, error, empty, and success states explicit for async UI.
- Avoid global state when local or server state is sufficient.
- Use semantic HTML.

## Tanstack / React Query

- Query keys are arrays, ordered from general to specific, and include every variable the query depends on (filters, ids, pagination). Use a query key factory per entity instead of hand-writing keys inline.

```ts
export const userKeys = {
  all: ["users"] as const,
  lists: () => [...userKeys.all, "list"] as const,
  list: (filters: UserFilters) => [...userKeys.lists(), filters] as const,
  details: () => [...userKeys.all, "detail"] as const,
  detail: (id: string) => [...userKeys.details(), id] as const,
};
```

- Wrap each query in a named hook (`useUser`, `useUserList`) rather than calling `useQuery` directly in components. Keep the query function in a colocated `api`/`queries` module.

```ts
export function useUser(id: string) {
  return useQuery({
    queryKey: userKeys.detail(id),
    queryFn: () => fetchUser(id),
    enabled: Boolean(id),
  });
}
```

- Set `staleTime` deliberately based on data volatility instead of relying on the default of `0` for data that does not need to be refetched constantly.
- Use `enabled` for dependent queries instead of conditionally calling hooks.
- Handle `isPending`/`isLoading`, `isError`, and success states explicitly in the UI; do not assume data is defined once `isLoading` is `false`.
- After mutations, invalidate the related query keys (prefer the narrowest key that covers the affected data) rather than refetching broadly or manually patching the cache.

```ts
export function useUpdateUser(id: string) {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: (input: UpdateUserInput) => updateUser(id, input),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: userKeys.detail(id) });
    },
  });
}
```

- Use `isPending` from `useMutation` for submit/button loading states, and surface mutation errors at the UI boundary that triggered the mutation.
- For optimistic updates, set the new value in `onMutate`, capture the previous value for rollback, and roll back in `onError`.


## Runtime validation

Use Zod or an established project equivalent at untrusted runtime boundaries when schema validation is needed.
For complex React forms, React Hook Form is preferred when appropriate, typically integrated with runtime validation.

## Utilities

`utils`, `helpers`, `common`, and `shared` are allowed, but keep their purpose clear.
Do not turn them into unstructured dumping grounds.

## Exports

Barrel files are allowed when they provide useful module ergonomics. Avoid circular dependencies and unclear ownership.

## Errors

Do not swallow rejected promises.
Use typed errors or discriminated result structures where they improve clarity.
Handle UI errors at meaningful boundaries.
