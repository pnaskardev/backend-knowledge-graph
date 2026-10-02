---
aliases: [Liveness Probe, Readiness Probe]
---
# Health Probes

> Two probes, two different questions. Confusing them is the classic k8s outage.

## Liveness Probe
<!-- "is this process wedged?" Fails → kubelet restarts the container. -->

## Readiness Probe
<!-- "can this pod serve traffic right now?" Fails → removed from the Service endpoints, not restarted. -->

## Startup Probe
<!-- for slow-booting apps, so liveness does not kill them before they finish starting. -->

## The classic mistake
<!-- pointing liveness at a dependency check. The dependency blips, every pod "fails" liveness, k8s restarts the whole fleet at once. Dependencies belong in readiness. -->

---
## 🔗 Connections
- **Prerequisite:** [[Pod]]
- **Used by / relates to:** [[Deployments & ReplicaSets]] [[Service & Ingress]] [[Load Balancer]] [[Resilience Patterns]]

#kubernetes #review
