# Corrected mental model of where a buildx result actually lands

After Lesson 0003, the user kept asking sharp follow-up questions that exposed a gap in the lesson itself: "why doesn't `docker image ls` show anything after a multi-arch build," "how do I retag it to push," "why do I see it now but not before," "where was that earlier image the whole time," "is `--load` only needed for multi-arch, or always?" Each question was answered by running the real command live rather than reasoning from the docs, which surfaced a factual error in the lesson.

**Evidence**: Live-tested on the user's machine (Docker 29.6.0, containerd image store enabled). Confirmed:
- Without `--load`/`--push`, a `docker-container` build's result lives only in BuildKit's own build cache (`docker buildx du` showed unnamed, content-hashed entries) — never touches the Docker image store, regardless of platform count.
- `--load` **does** support multi-platform results here, contradicting Lesson 0003's original claim — because this host uses the containerd image store (`docker info` → `io.containerd.snapshotter.v1`). The result imports as one OCI index; `docker image ls --tree` unpacks it per-platform. On the classic image store this would fail.
- The need for `--load`/`--push` is driven by **driver**, not platform count: the `docker` driver auto-loads always; every other driver (`docker-container`, `remote`, `kubernetes`) needs the flag explicitly even for a single platform.
- `docker buildx imagetools inspect` only works against registry references; pointing it at a local-only tag gives a misleading "pull access denied."

Fixed Lesson 0003 in place (corrected the `--load` claim with a visible correction callout) and added `reference/builder-drivers.html` as the durable lookup table (driver × auto-load × multi-platform-support, plus the inspect/cleanup commands). Added `--load`, `--push`, and `Build cache (BuildKit)` to `GLOSSARY.md`.

**Implications**: The user's debugging instinct here was strong — they didn't accept the lesson's claim, kept pushing "but where is it, why is it different now," which is exactly the kind of question that catches stale documentation. Future lessons on this track should default to verifying flag behavior live against this specific host rather than trusting docs' idealized examples, since image-store behavior (containerd vs. classic) materially changes what's true.
