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

## Build engine

**Buildx**:
The CLI client for Docker builds (`docker buildx ...`). It's the frontend — it doesn't build anything itself, it sends build requests to a builder.
_Avoid_: the build tool, buildkit (that's the backend, see below)

**BuildKit**:
The backend build engine that actually executes a Dockerfile: resolves stages, runs instructions, manages the layer cache, assembles the final image. Buildx talks to a BuildKit instance; a builder *is* a BuildKit instance plus the driver that runs it.
_Avoid_: the daemon, the build server

**Builder**:
A named, persistent BuildKit instance that buildx can send builds to (`docker buildx create`, `docker buildx ls`). Every Docker install starts with one default builder; you can create more.
_Avoid_: build target, build context (that's a different thing — see above)

**Driver**:
The mechanism a builder uses to run BuildKit. `docker` (default, uses the Docker Engine's built-in BuildKit, single-platform only) and `docker-container` (runs BuildKit in a dedicated container, supports multi-platform) are the two you'll use locally.
_Avoid_: backend, engine type

**`--platform`**:
Flag on `docker buildx build` naming one or more target OS/architecture pairs (e.g. `linux/amd64`, `linux/arm64`). Comma-separate multiple values to build for several architectures in one command.
_Avoid_: arch flag, target flag

**QEMU emulation**:
Lets BuildKit run instructions for a non-native CPU architecture (e.g. running arm64 code on an amd64 host) by emulating that architecture. Bundled with BuildKit by default. Correct but slower than a native build.
_Avoid_: cross-compilation (that's a different technique — compiling *for* another arch without emulating it)

**Manifest list**:
A single image reference that points to multiple architecture-specific image variants. When you `docker pull` a multi-arch image, the engine reads the manifest list and pulls only the variant matching your machine.
_Avoid_: multi-arch image (imprecise — the list is the thing that makes one image multi-arch), fat manifest

**`--load`**:
Flag on `docker buildx build` that imports the build result into the local Docker image store, so it shows up in `docker image ls`. Required for every driver except `docker` (which does this automatically). Whether it accepts a *multi-platform* result depends on the local image store — works on containerd, fails on classic. See `reference/builder-drivers.html`.
_Avoid_: import flag, save flag (that's `docker save`, a different command)

**`--push`**:
Flag on `docker buildx build` that sends the build result to a registry instead of (or as well as) loading it locally. For multi-platform builds, this is where the manifest list actually gets assembled — pushing is what makes a multi-arch image real, not just proven-to-build.
_Avoid_: upload flag, publish flag

**Build cache (BuildKit)**:
Intermediate, unnamed results BuildKit keeps for each instruction it runs, stored inside the builder itself (e.g. the `docker-container` builder's own container). If a build specifies neither `--load` nor `--push`, the result *only* exists here — not as a runnable image, not visible to `docker image ls`. Only useful for speeding up the next build with matching steps (`CACHED` in the build log). Inspect with `docker buildx du`, clear with `docker buildx prune`.
_Avoid_: image cache (imprecise — it's not a store of images, it's per-instruction build state)
