# Mission: Write my own multi-stage Dockerfiles, build them for multiple architectures, and run multi-service apps with Compose

## Why
I want to be able to write multi-stage Dockerfiles for my own real projects (Node, Python, Go) so I can ship small, secure images instead of bloated single-stage ones. The goal is practical ability to write them, not just understand the idea.

Extended (2026-07-16): I also want to understand the build engine itself — Buildx/BuildKit architecture, how caching works, and how to set up a local builder that can produce images for multiple CPU architectures (amd64 + arm64) from one machine.

Extended (2026-07-16, Goal 2 added): Once I can build good images, I want to *run* real apps made of several containers together — a web service plus its data store — using Docker Compose. Practical ability to read and write a `compose.yaml` and bring an app up, starting from the `ddd-book/multi-container` Flask + Redis example.

## Goal 1 — Multi-stage & multi-arch builds — Success looks like
- I can write a correct multi-stage Dockerfile from scratch for a simple app in a language I choose
- I can explain why each stage exists and what the final image actually contains
- I can use `--target` to build a single stage and compare image sizes
- I can explain why the default `docker` driver can't do multi-platform builds, and create a `docker-container` builder that can
- I can run a `--platform linux/amd64,linux/arm64` build on my local machine and explain what QEMU emulation is doing

## Goal 2 — Docker Compose — Success looks like
- I can read a `compose.yaml` and say what each service, network, and volume is for
- I can explain why one service uses `build:` and another uses `image:`
- I can explain how one service reaches another by its service name (service discovery)
- I can bring the multi-container app up and down with `docker compose up` / `down`, and read `compose ps` / `logs`
- Later: write my own `compose.yaml` for a two-service app from scratch

## Constraints
- Learning through this workspace; comfortable reading a Go example but not a Go programmer
- Prefers step-by-step, token-by-token explanations and asks very granular questions

## Out of scope (for now)
- Swarm orchestration and multi-host / production deployment of Compose apps
- Remote builders / Docker Build Cloud (local builders only for now)
- Registries, CI/CD pipelines, and deployment (pushing multi-arch manifests is a later step)
