# Notes

## User learning preferences (observed)
- Asks extremely granular, token-by-token questions (e.g. "what does `./cmd/server` mean?").
- Prefers step-by-step explanation in the terminal; wants each part explained before moving on.
- Comfortable reading a Go example but is **not** a Go programmer — lean on Node/Python analogies when teaching.
- Goal is practical: **write their own** multi-stage Dockerfiles, not just understand.

## Session history
- 2026-07-15: Walked through `ddd-book/multi-stage` example (problem, go build flags, RUN-in-container, COPY-from-context, stage anatomy). User approved a walkthrough design, then asked to switch into the `teach` skill flow.
- Switched to teaching workspace; mission = "write my own multi-stage Dockerfiles".
- 2026-07-16: User brought in own summary notes on Buildx/BuildKit architecture and caching, then asked to create a local builder for multi-arch builds. Mission expanded (confirmed by user) to include multi-platform builds. Checked environment: Docker 29.6.0, buildx v0.34.1, default builder is `docker` driver (single-platform only) with QEMU emulation already available (+3 platforms listed). Reused `exercises/node-express` (pure JS, no native deps — safe first multi-arch target).
- 2026-07-16 (same session, cont.): User's follow-up questions ("why doesn't it show in `docker image ls`", "where was the earlier image", "is `--load` only for multi-arch") caught a factual error in Lesson 0003 (claimed `--load` can't do multi-platform — false on this host's containerd image store). Fixed the lesson, added `reference/builder-drivers.html` as the durable driver/output-flag table. Pattern to repeat: this user's granular "but why/where" questions are a good signal to re-verify against the live machine rather than trust the docs' idealized example.
- 2026-07-16: User asked to start Docker Compose, working in `ddd-book/multi-container`. Compose had been out of scope; confirmed via question and user chose to **add it as a second mission goal** (kept the build track). Updated `MISSION.md` (Goal 2), logged `learning-records/0005`. Verified live: Docker Compose v5.3.1, `docker compose` (space) form. Shipped Lesson 0004 (Compose file anatomy + `up`, grounded in the Flask+Redis counter app) and `reference/compose-file-anatomy.html`; added Compose terms to `GLOSSARY.md` and a Compose section to `RESOURCES.md`. Next candidate lessons: networking/service-discovery deep dive, then volumes/persistence, then writing a `compose.yaml` from scratch (Goal 2 finish line).
