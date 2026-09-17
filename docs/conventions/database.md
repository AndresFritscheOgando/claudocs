# Database Conventions

- Every table must have a primary key.
- Use explicit foreign keys when relationships require them.
- Use database constraints to protect important invariants where appropriate.
- Do not rely only on application validation for data integrity.
- Create indexes based on real query patterns, not speculation.
- Avoid N+1 query behavior.
- Use schema migrations for every schema change.
- Never manually mutate production schemas as a normal deployment process.
- Avoid `SELECT *` in deliberate production queries when explicit columns are practical.
- Use pagination for large result sets.

## Naming

Prefer `snake_case` for relational database identifiers:

```text
users
payment_transactions
medical_records
created_at
updated_at
user_id
```

Follow an established project naming scheme if one already exists.
