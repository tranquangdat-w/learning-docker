# Added Docker Compose as a second mission goal

The user asked to start learning Docker Compose, working in `ddd-book/multi-container`. Compose was previously listed *out of scope* in `MISSION.md` (alongside Swarm). Offered three framings — add as a second goal, pivot fully, or treat as a one-off detour — and the user chose **add as a second goal**, keeping the multi-stage/multi-arch build track intact.

**Evidence / decisions**:
- Updated `MISSION.md`: retitled the mission, added a "Goal 2 — Docker Compose" success section, and narrowed the out-of-scope note from "Docker Compose / swarm orchestration" to just Swarm + multi-host/production deployment. Compose (local, single-host) is now in scope.
- Confirmed the toolchain live on this host: **Docker Compose v5.3.1**, invoked as `docker compose` (the v2+ plugin form, not the legacy `docker-compose` hyphen). `docker compose config --services` parses both `web-fe` and `redis` from the example.
- Chosen first teaching target: `ddd-book/multi-container` — a Flask front end (`web-fe`, `build: .`) + Redis (`image: redis:alpine`) counter app on a shared `counter-net` network with a `counter-vol` volume. Grounds the single most important Compose idea (service-name DNS discovery: `app.py` connects to `host='redis'`).
- Produced Lesson 0004 (anatomy + `docker compose up`) and `reference/compose-file-anatomy.html`. Added Compose terms to `GLOSSARY.md` and a Compose section to `RESOURCES.md`.

**Implications**: Compose builds directly on the user's existing image/build-context knowledge — the `build: .` service is a natural bridge from the Dockerfile track, so lean on that link. The `multi-container` app is a reusable teaching surface for the next Compose lessons (networks deep-dive, volumes/persistence, `depends_on` vs readiness, then writing a `compose.yaml` from scratch — the Goal 2 finish line). Keep the "verify live on this host" habit: the Dockerfile here has an exec-form `ENTRYPOINT` *and* the compose `command:` repeats it, a quirk worth checking live if the user asks why the app still starts.
