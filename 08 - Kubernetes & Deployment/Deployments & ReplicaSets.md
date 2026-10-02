---
aliases: [Deployment, ReplicaSet]
---
# Deployments & ReplicaSets

> You write a Deployment; it manages ReplicaSets; they manage Pods. One chain, learn it as one.

## ReplicaSet
<!-- keeps N identical pods running. That is its entire job. -->

## Deployment
<!-- manages ReplicaSets so you can change the pod spec safely. You almost never create a ReplicaSet directly. -->

## Rolling update
<!-- a new ReplicaSet scales up as the old one scales down. maxSurge / maxUnavailable control the pace. -->

## Rollback
<!-- the old ReplicaSet is kept, so a rollback is just scaling it back up. -->

## Why readiness matters here
<!-- a rolling update only works if [[Health Probes]] tell k8s when a new pod is actually serving. -->

---
## 🔗 Connections
- **Prerequisite:** [[Pod]] [[Kubernetes]]
- **Used by / relates to:** [[Health Probes]] [[Horizontal Pod Autoscaler]] [[Service & Ingress]]

#kubernetes #review
