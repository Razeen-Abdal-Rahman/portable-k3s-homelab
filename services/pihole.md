# Pi-hole Service

Pi-hole provides DNS-based ad blocking and network visibility.

It is a critical infrastructure component.

## Why Pi-hole

- Centralised DNS control
- Minimal client configuration
- Proven reliability
- Low resource usage

It integrates well with Kubernetes.

## Deployment model

- Deployed as a Kubernetes Deployment
- Exposed internally via a Service
- No public ingress

All configuration is stored declaratively where possible.

## DHCP decision

Pi-hole does not manage DHCP.

This decision was made after discovering:

- Guest network breakage
- Router limitations
- Poor interoperability

DNS-only mode provides the best balance.

## Resource constraints

Running Pi-hole in Kubernetes adds overhead.

Limits are configured to prevent:

- Memory exhaustion
- Pod eviction
- Node instability

## Lessons reinforced

Prior experience with Pi-hole outside Kubernetes significantly reduced troubleshooting time.

Documentation matters.
