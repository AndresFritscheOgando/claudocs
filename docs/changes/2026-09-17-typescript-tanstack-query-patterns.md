# TanStack / React Query common patterns added to TypeScript conventions

**Date:** 2026-09-17
**Type:** Documentation

## Summary

The "Tanstack / React Query" section in `docs/conventions/typescript.md` was previously an empty heading. Added common query patterns: query key factories, named query hooks, `staleTime` guidance, dependent queries via `enabled`, explicit loading/error/success state handling, mutation cache invalidation, mutation loading state via `isPending`, and optimistic update rollback.

## Rationale

The convention doc had no guidance for TanStack Query usage, leaving query key structure, cache invalidation, and mutation patterns undocumented for new code in React/Next.js projects.
