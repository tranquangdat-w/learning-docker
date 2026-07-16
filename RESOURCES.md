# Multi-Stage Docker Resources

## Knowledge

- [Docker Docs: Multi-stage builds](https://docs.docker.com/build/building/multi-stage/)
  The canonical reference. Use for: the exact syntax of `FROM ... AS` and `COPY --from`, and the default-last-stage rule.
- [Docker Docs: Get started — Multi-stage builds](https://docs.docker.com/get-started/docker-concepts/building-images/multi-stage-builds/)
  Gentler conceptual intro with a Java/JAR worked example. Use for: a second framing after the Go example, and the `--target` explanation.
- [Docker Blog: Multi-Stage Builds (2017, original announcement)](https://www.docker.com/blog/multi-stage-builds/)
  Historical context — why the feature exists and the "builder pattern" it replaced. Use for: understanding *why* named stages matter.
- [Docker Blog: Advanced Dockerfiles (BuildKit + multistage)](https://www.docker.com/blog/advanced-dockerfiles-faster-builds-and-smaller-images-using-buildkit-and-multistage-builds/)
  Advanced patterns: `FROM stagename` reuse, args in `FROM`, conditional branches. Use for: later sessions once basics are solid.
- [Systems Explained: Docker Multi-Stage Builds](https://systeminternals.dev/docker/multi-stage-builds/)
  Clear prose on stage composition, ARG scope, and choosing scratch/alpine/distroless. Use for: the "pick a runtime" decision and ARG scoping gotchas.
- [Book: _Docker Deep Dive_ — Nigel Poulton](https://www.nigelpoulton.com/books/docker-deep-dive/)
  Highly regarded foundational text. Use for: base images, image layers, and the build cache mental model.

## Knowledge — Buildx, BuildKit & multi-arch

- [Docker Docs: Creating and managing builders](https://docs.docker.com/build/builders/manage/)
  Canonical reference for `docker buildx create/ls/inspect/rm`. Use for: exact flags when setting up a local builder.
- [Docker Docs: Multi-platform builds](https://docs.docker.com/build/building/multi-platform/)
  Explains why the default `docker` driver can't build multi-platform images, and how `--platform` works. Use for: the core "why do I need a new builder" motivation.
- [Docker Docs: docker-container driver](https://docs.docker.com/build/builders/drivers/docker-container/)
  The driver used for local multi-arch builders — runs BuildKit in a dedicated container, supports QEMU emulation. Use for: `--driver-opt` flags and how builder state/cache is stored.
- [Docker Docs: BuildKit](https://docs.docker.com/build/buildkit/)
  Background on the BuildKit engine buildx talks to, and its cache model (layer cache, cache invalidation on the first changed instruction).

## Knowledge — Docker Compose

- [Docker Docs: Compose Quickstart](https://docs.docker.com/compose/gettingstarted/)
  Walks the *same* Flask + Redis counter app as `ddd-book/multi-container`. Use for: the canonical wording behind Lesson 0004, and the first hands-on `up`/`down` loop.
- [Docker Docs: How Compose works](https://docs.docker.com/compose/intro/features-uses/)
  The mental model — declarative app definition, the project concept, why one file. Use for: framing *why* Compose exists after the Dockerfile track.
- [Docker Docs: Compose file reference — services](https://docs.docker.com/reference/compose-file/services/)
  Exhaustive list of every per-service key (`build`, `image`, `ports`, `volumes`, `depends_on`, …). Use for: exact syntax when writing a `compose.yaml` from scratch.
- [Docker Docs: Networking in Compose](https://docs.docker.com/compose/how-tos/networking/)
  How the default network and service-name DNS work. Use for: the service-discovery deep dive (next lesson after 0004).
- [Book: _Docker Deep Dive_ — Nigel Poulton (Ch. 9)](https://www.nigelpoulton.com/books/docker-deep-dive/)
  The chapter this `multi-container` app was written for. Use for: the guided book walkthrough of this exact app.

## Wisdom (Communities)

- [Docker Community Slack (#buildkit channel)](https://dockr.ly/comm-slack)
  High-signal place for multistage/BuildKit questions. Use for: real-world build troubleshooting.
- [r/docker](https://reddit.com/r/docker)
  Broad Docker community. Use for: sharing Dockerfiles for critique and pattern validation.

## Gaps

- No hands-on, exercise-driven tutorial yet inside this workspace (being built as lessons).
- User is not a Go programmer; a Node or Python worked example would ground the writing-goal better than the Go sample alone.
