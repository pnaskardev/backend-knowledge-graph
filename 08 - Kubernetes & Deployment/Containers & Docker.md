---
aliases: [Container, Docker]
---
# Containers & Docker

> A container is the concept; Docker is the tool that made it usable.

## What a container actually is
<!-- a process with namespaces (isolation) and cgroups (limits). Not a VM — same kernel, no guest OS. -->

## Image vs container
<!-- image = the layered, immutable filesystem. Container = a running instance of it. -->

## Docker
<!-- Dockerfile → build → image → registry → run. Layer caching is why build order matters. -->

## Why this matters for k8s
<!-- k8s schedules containers; everything above [[Pod]] assumes this model. -->

---
## 🔗 Connections
- **Used by / relates to:** [[Kubernetes]] [[Pod]] [[Deployments & ReplicaSets]]

#kubernetes #review
