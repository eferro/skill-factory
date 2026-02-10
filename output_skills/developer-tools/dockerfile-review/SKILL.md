---
name: dockerfile-review
description: Reviews Dockerfiles for build performance, image size, and security issues. Use when optimizing, validating, or improving Dockerfiles.
---

# Dockerfile Review

STARTER_CHARACTER = 🐳

When starting, announce: "🐳 Using DOCKERFILE-REVIEW skill".

## Process

1. Read the Dockerfile (and .dockerignore if present)
2. Evaluate against each dimension below
3. Report findings grouped by severity: critical (security risks), major (significant size/performance impact), minor (incremental improvements)
4. For each finding: state what's wrong, why it matters, and suggest a fix direction
5. If the Dockerfile is solid, say so — don't invent issues

## Review Dimensions

### 1. Layer Cache Ordering

Dependency files (package.json, requirements.txt, go.mod) must be copied and installed BEFORE application source code. Violations cause full dependency reinstalls on every code change.

Anti-pattern: `COPY . .` followed by `RUN pip install` or `RUN npm ci`. The entire dependency layer rebuilds on any source change.

Impact: builds that should take seconds take minutes. With frequent builds, this compounds to hours per week.

### 2. Base Image Selection

Three tiers exist: full (includes compilers, tools), slim (minimal OS, basic tooling), distroless (application only, no shell).

Anti-patterns:
- Using full images in production (node:20 is ~950MB vs node:20-slim at ~220MB)
- Using distroless when debugging access is needed
- Not considering slim as the default production choice

### 3. .dockerignore Coverage

Without .dockerignore, `COPY . .` sends everything to the build context: node_modules (50-500MB), .git (100MB+), coverage reports, IDE configs, .env files.

Anti-patterns:
- No .dockerignore file at all
- Missing .git/ (often the largest offender in mature repos)
- Missing local dependency directories (node_modules/, venv/, __pycache__/)
- Missing .env files (both a size and security issue)

### 4. Multi-Stage Builds

Build tools, compilers, and dev dependencies should not exist in the final image. Multi-stage builds separate construction from execution.

Anti-patterns:
- Single-stage builds that include build toolchains in production
- Copying entire build context into final stage instead of only artifacts
- Not using named stages (makes COPY --from fragile)

### 5. Version Pinning

Tags like `latest` or unpinned package versions create non-reproducible builds.

Anti-patterns:
- `FROM ubuntu:latest` or `FROM node:lts`
- `apt-get install -y curl` without version pinning
- No lock files for language-level dependencies

### 6. Layer Minimization

Each RUN, COPY, ADD creates a layer. Deletions in later layers don't reduce image size — the previous layer still contains the data.

Anti-pattern: separate RUN instructions for install and cleanup. `RUN apt-get update` then `RUN rm -rf /var/lib/apt/lists/*` preserves the cache in the first layer.

Fix direction: combine install and cleanup in a single RUN with `&&`.

### 7. Secret Handling

Credentials, API keys, and tokens embedded in layers are permanently accessible via `docker history` or registry inspection.

Anti-patterns:
- `ENV API_KEY=...` or `ARG` with secrets passed at build time
- COPY of .env, credentials, or key files into the image
- RUN commands with inline secrets

Fix direction: use `--mount=type=secret` with BuildKit for build-time secrets. Never bake secrets into layers.

### 8. Non-Root Execution

Running as root means a container escape or application vulnerability grants full system access.

Anti-patterns:
- No USER instruction (defaults to root)
- USER instruction placed before file operations (causing permission issues)
- Not setting file ownership with chown

Fix direction: create a dedicated user with useradd, chown application files, then switch with USER — placed after all file operations that need root.

## Severity Classification

- **Critical**: secret handling violations, running as root in production
- **Major**: missing multi-stage builds, poor cache ordering, no .dockerignore, full base images in production
- **Minor**: unpinned versions, extra layers, missing specific .dockerignore entries
