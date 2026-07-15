# Mission: Write my own multi-stage Dockerfiles

## Why
I want to be able to write multi-stage Dockerfiles for my own real projects (Node, Python, Go) so I can ship small, secure images instead of bloated single-stage ones. The goal is practical ability to write them, not just understand the idea.

## Success looks like
- I can write a correct multi-stage Dockerfile from scratch for a simple app in a language I choose
- I can explain why each stage exists and what the final image actually contains
- I can use `--target` to build a single stage and compare image sizes

## Constraints
- Learning through this workspace; comfortable reading a Go example but not a Go programmer
- Prefers step-by-step, token-by-token explanations and asks very granular questions

## Out of scope (for now)
- Docker Compose / swarm orchestration
- Multi-platform and cross-compilation builds
- Registries, CI/CD pipelines, and deployment
