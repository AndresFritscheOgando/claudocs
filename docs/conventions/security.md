# Security Conventions

- Never commit secrets, passwords, tokens, private keys, or production credentials.
- Never hardcode credentials.
- Treat all external input as untrusted.
- Validate input at system boundaries.
- Enforce authorization server-side.
- Authentication does not imply authorization.
- Apply least privilege.
- Do not log secrets, passwords, tokens, payment data, or other sensitive values.
- Use parameterized database access.
- Do not implement custom cryptography.
- Use established password-hashing libraries and algorithms.
- Store secrets in environment configuration or an approved secret manager.
- Keep dependencies patched and remove unused dependencies.
- Prefer secure defaults over optional security controls.
