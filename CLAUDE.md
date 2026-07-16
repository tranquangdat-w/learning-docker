# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is a **personal learning workspace**, not a software product. Its purpose is to teach the owner to write multi-stage Dockerfiles and set up local multi-architecture builds (see `MISSION.md`). There is no application to build, lint, or test as a whole — "the work" is producing lessons, exercises, and records that move the mission forward.

Because there is no build/test/lint pipeline, the meaningful commands are the Docker commands the lessons teach. Verify their behavior **live on the user's machine** rather than trusting docs (see the workflow note below). Current host: Docker 29.6.0, buildx v0.34.1, **containerd image store enabled** — this last fact changes what `--load` does and has already caused one factual error in a lesson.

## Layout and how the pieces relate

- **`MISSION.md`** — the single source of truth for the learning goal, success criteria, and what's out of scope. Read this first; check any proposed work against it. Edit it (with the user's confirmation) when the mission genuinely changes — it has already been expanded once.
- **`GLOSSARY.md`** — the *canonical* vocabulary for this workspace. Every term has an "_Avoid_" list of imprecise synonyms. Lessons, records, and your own explanations must use these exact terms and avoid the listed alternatives. Add a term here when a lesson introduces one.
- **`NOTES.md`** — user learning preferences (below) plus a running session history. Append to the session history at the end of substantial sessions.
- **`RESOURCES.md`** — curated external links, each annotated with *when to use it*. Draw teaching references from here.
- **`lessons/NNNN-kebab-title.html`** — self-contained HTML lessons, zero-padded and sequentially numbered, each linking `../assets/style.css`. Match the existing house style: a `<main>`, an `h1` + `.subtitle`, and `.stage-box` callouts that break a command down flag-by-flag. Commands must be individually runnable/self-contained.
- **`learning-records/NNNN-kebab-title.md`** — after-the-fact records of what was learned or discovered, same numbering. Structure: what happened → **Evidence** (what was tested live) → **Implications** for future sessions. These capture *corrections and insight*, not lesson content.
- **`reference/*.html`** — durable lookup tables (e.g. `builder-drivers.html`: driver × auto-load × multi-platform support). Promote something here when it's a fact worth looking up repeatedly rather than a one-time lesson.
- **`exercises/`** — hands-on code the user builds against. `exercises/node-express` is pure JS (no native deps) — the safe first multi-arch target.
- **`ddd-book/`** — companion source for the *Docker Deep Dive* book (external, upstream code). Treat as read-only reference material; it is **not** the user's own work and is largely out of scope for the current mission.

The `lessons` / `learning-records` / `reference` numbering is a shared sequence per directory — always continue from the highest existing number.

## Teaching workflow (how to work here)

This workspace is driven through a teaching flow, not ad-hoc edits. Two habits matter most:

1. **Verify against the live machine, not the docs.** This user asks extremely granular "but why / but where" follow-ups, and those questions have already caught an idealized-docs claim that was false on this host (containerd image store). When teaching a command's behavior, run it and read the real output before asserting what it does. See `learning-records/0004`.
2. **Keep the artifacts in sync.** A new concept usually touches several files: the lesson (`lessons/`), any new vocabulary (`GLOSSARY.md`), a record if something was corrected or discovered (`learning-records/`), and the session log (`NOTES.md`). Don't leave the glossary or records stale after a lesson lands.

## User learning preferences (from NOTES.md — honor these)

- Asks **extremely granular, token-by-token** questions (e.g. "what does `./cmd/server` mean?"). Explain step by step; don't move on until each part is understood.
- Comfortable **reading** a Go example but is **not** a Go programmer — lean on **Node / Python analogies** when teaching.
- Goal is practical: get to **writing their own** Dockerfiles, not just understanding the concept.
