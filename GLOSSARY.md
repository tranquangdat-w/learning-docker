# Multi-Stage Docker Glossary

The canonical language for this teaching workspace. Lessons and records adhere to these terms.

## Build mechanics

**Build context**:
The directory on the host that you pass to `docker build` (the path at the end of the command, e.g. `.`). It is the only set of files `COPY` can reach into.
_Avoid_: project folder, source directory

**Stage**:
One independent build phase in a Dockerfile, started by a `FROM` line and optionally named with `AS <name>`. Each stage has its own filesystem and layer cache.
_Avoid_: step, phase, layer

**Base image**:
The image named in a `FROM` line that a stage starts from (e.g. `golang:1.23-alpine`, `node:20`, `scratch`).
_Avoid_: parent image, source image

**scratch**:
A Docker-reserved keyword — not a real image that can be pulled or stored. It represents a completely empty filesystem with nothing in it (no shell, no libraries, no files). Used as the final stage for fully static binaries; the stage fills up only through `COPY --from`.
_Avoid_: empty image, blank image, downloaded image

**`COPY --from`**:
The instruction that copies files out of a previous named stage (or any image) into the current stage. This is the bridge between stages.
_Avoid_: copy from stage, stage copy

**`WORKDIR`**:
Sets the default working directory inside the container for all following `RUN`, `COPY`, and `ENTRYPOINT` instructions.
_Avoid_: cd, working folder

**Image layer**:
An immutable snapshot produced by each `RUN`, `COPY`, or `ADD` instruction. Stages are composed of layers; only the last stage's layers ship.
_Avoid_: step, slice
