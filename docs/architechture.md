# Architecture

This document describes the high-level architecture of the system and how its components interact.

It focuses on structure and intent rather than configuration detail.

## High-level view

The system consists of:

- A single Raspberry Pi running k3s
- Kubernetes-managed workloads
- Router-enforced network segmentation
- An encrypted overlay network for remote access

All application logic runs inside Kubernetes.

## Kubernetes architecture

- Single-node k3s cluster
- Control plane and workloads run on the same node
- Embedded datastore
- Default components removed where unnecessary to reduce overhead

Removed components include:

- Ingress controller
- Service load balancer
- Metrics server

This improves responsiveness on constrained hardware.

## Workload patterns

Services are deployed using:

- Deployments for long-running services
- Services for internal networking
- Persistent volumes for stateful data

All manifests are applied directly using `kubectl`.

No Helm or GitOps tooling is used at this stage.

## Data flow example: DNS

1. Client device sends DNS query
2. Router forwards DNS to Pi-hole
3. Pi-hole resolves or forwards upstream
4. Response is returned to the client

This places DNS at a central control point.

## Remote access flow

- No inbound ports are opened
- The node joins an encrypted mesh network
- Administrative access occurs over this overlay

The local network remains inaccessible from the public internet.

## Future architecture

Planned changes include:

- Adding a Raspberry Pi 5 as a second node
- Migrating storage-heavy workloads to the Pi 5
- Introducing node labels and workload pinning
- Moving persistent data to external SSD storage

Multi-node control plane is a possible future step, not a current requirement.
