# Mission: Write my own multi-stage Dockerfiles, and build them for multiple architectures

## Why
I want to be able to write multi-stage Dockerfiles for my own real projects (Node, Python, Go) so I can ship small, secure images instead of bloated single-stage ones. The goal is practical ability to write them, not just understand the idea.

Extended (2026-07-16): I also want to understand the build engine itself — Buildx/BuildKit architecture, how caching works, and how to set up a local builder that can produce images for multiple CPU architectures (amd64 + arm64) from one machine.

## Success looks like
- I can write a correct multi-stage Dockerfile from scratch for a simple app in a language I choose
- I can explain why each stage exists and what the final image actually contains
- I can use `--target` to build a single stage and compare image sizes
- I can explain why the default `docker` driver can't do multi-platform builds, and create a `docker-container` builder that can
- I can run a `--platform linux/amd64,linux/arm64` build on my local machine and explain what QEMU emulation is doing

## Constraints
- Learning through this workspace; comfortable reading a Go example but not a Go programmer
- Prefers step-by-step, token-by-token explanations and asks very granular questions

## Out of scope (for now)
- Docker Compose / swarm orchestration
- Remote builders / Docker Build Cloud (local builders only for now)
- Registries, CI/CD pipelines, and deployment (pushing multi-arch manifests is a later step)
