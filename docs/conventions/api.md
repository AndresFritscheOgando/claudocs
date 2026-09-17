# API Conventions

- Use nouns for REST resources.
- Use plural resource names consistently.
- Avoid action verbs in REST resource paths when normal HTTP semantics are sufficient.
- Use appropriate HTTP methods and status codes.
- Validate all external input.
- Never expose persistence entities directly through public APIs.
- Use explicit request and response models.
- Paginate collections that can grow large.
- Preserve backward compatibility unless the task explicitly changes the contract.
- Document breaking changes.

## Example

```text
GET    /api/v1/users/{id}
POST   /api/v1/users
PATCH  /api/v1/users/{id}
DELETE /api/v1/users/{id}
```

## Api Response

```json
{

public record ApiResponse<T>(
        String message,
        int status,
        Instant timestamp,
        T data,
        boolean success
) {
}
}
```

## Error response baseline

Use a predictable structure such as:

```json
{
  "message": "User was not found",
  "timestamp": "...",
  "error": "{error status code}",
  "path": "../../.."
}
```
ApiError and ApiResponse should be in `/dto/payload/ApiResponse.Java`  and `dto/payload/ApiError.Java`
Adapt fields to the project, but keep the structure consistent.
