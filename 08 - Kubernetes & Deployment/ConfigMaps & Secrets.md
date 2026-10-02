---
aliases: [ConfigMap, Secret]
---
# ConfigMaps & Secrets

> Same mechanism, two objects. Config out of the image so one image runs in every environment.

## ConfigMap
<!-- non-sensitive key/value config. Mount as env vars or as files. -->

## Secret
<!-- same shape, for sensitive values. base64 is encoding, not encryption — enable encryption at rest and RBAC or it is not a secret. -->

## Env var vs volume mount
<!-- env vars are fixed at pod start; mounted files can update live. Matters if you want config reload without a restart. -->

## Key trade-off
<!-- changing a ConfigMap does not restart pods by itself — you need a rollout or a reloader. -->

---
## 🔗 Connections
- **Prerequisite:** [[Pod]]
- **Used by / relates to:** [[Deployments & ReplicaSets]] [[Containers & Docker]] [[Authentication & Authorization]]

#kubernetes #review
