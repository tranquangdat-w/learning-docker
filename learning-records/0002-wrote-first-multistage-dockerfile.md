# Wrote first multi-stage Dockerfile (Node Express app)

Successfully wrote and built a two-stage Dockerfile for a Node Express app after a walkthrough of the Go buildme example. Debugged `COPY --from` directory semantics (contents vs directory name — `./node_modules` target required) and learned that `npm ci` requires a lockfile.

**Evidence**: `docker build` succeeded and `docker run` returned `{"message":"Hello from Node!"}` on port 3000.

**Implications**: Has the structural understanding to write a simple multi-stage Dockerfile. Next step: pattern for compiled languages (Go example already seen) and working with `scratch`.
