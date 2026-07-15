# Baseline multi-stage Docker knowledge established

During a walkthrough of `ddd-book/multi-stage` (the Docker buildme Go sample), the user demonstrated working understanding of the core concepts: what problem multi-stage solves (image size / attack surface), the role of `go build -o <out> <pkg>`, that `RUN` executes *inside* the container being built, and that `COPY` pulls only from the build context. They asked precise, token-level questions (e.g. the meaning of `./cmd/server`), which is evidence of engaged comprehension rather than passive exposure.

**Implications**: The floor is "understands the pieces." The next teachable step is *synthesis* — moving from reading a multi-stage Dockerfile to writing one. Favor Node/Python framings over Go, since the user is not a Go programmer but is comfortable with the Go sample as a reference.
