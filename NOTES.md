# Notes

## User learning preferences (observed)
- Asks extremely granular, token-by-token questions (e.g. "what does `./cmd/server` mean?").
- Prefers step-by-step explanation in the terminal; wants each part explained before moving on.
- Comfortable reading a Go example but is **not** a Go programmer — lean on Node/Python analogies when teaching.
- Goal is practical: **write their own** multi-stage Dockerfiles, not just understand.

## Session history
- 2026-07-15: Walked through `ddd-book/multi-stage` example (problem, go build flags, RUN-in-container, COPY-from-context, stage anatomy). User approved a walkthrough design, then asked to switch into the `teach` skill flow.
- Switched to teaching workspace; mission = "write my own multi-stage Dockerfiles".
