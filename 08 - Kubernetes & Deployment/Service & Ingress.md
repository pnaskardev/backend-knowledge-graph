---
aliases: [Service, Ingress]
---
# Service & Ingress

> Service gets traffic to a pod inside the cluster. Ingress gets traffic into the cluster. Two layers of the same path.

## Service
<!-- stable virtual IP + DNS name in front of a changing set of pods. Pods die and get new IPs; the Service does not. -->

## Service types
<!-- ClusterIP (internal), NodePort, LoadBalancer (cloud LB). Pick by who needs to reach it. -->

## Ingress
<!-- HTTP routing at the edge: host/path rules, TLS termination, one LB for many services. -->

## Ingress controller
<!-- Ingress is just a spec — nginx/traefik does the work. Nothing happens without a controller installed. -->

---
## 🔗 Connections
- **Prerequisite:** [[Pod]] [[Deployments & ReplicaSets]]
- **Used by / relates to:** [[Load Balancer]] [[API Gateway & BFF]] [[Health Probes]]

#kubernetes #review
