# Docker Conventions

- Use multi-stage builds when they materially reduce the production image.
- Use explicit base image versions appropriate to the project.
- Keep production images minimal.
- Do not copy unnecessary files into images.
- Maintain a `.dockerignore`.
- Do not run production containers as root when avoidable.
- Pass environment-specific configuration at runtime.
- Add health checks when they provide operational value.
- Keep containers focused on one primary application responsibility.
- Do not bake secrets into images.
