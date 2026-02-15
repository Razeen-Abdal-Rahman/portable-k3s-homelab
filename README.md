# Home Kubernetes Platform on Raspberry Pi

![Kubernetes Badge](https://img.shields.io/badge/kubernetes-badge?style=for-the-badge&logo=Kubernetes&logoColor=%23326CE5&labelColor=%23000000&color=%23326CE5)
![k3s Badge](https://img.shields.io/badge/k3s-badge?style=for-the-badge&logo=K3s&logoColor=%23FFC61C&labelColor=%23000000&color=%23FFC61C)
![Raspberrypi Badge](https://img.shields.io/badge/raspberrypi-badge?style=for-the-badge&logo=raspberrypi&logoColor=%23A22846&labelColor=%23000000&color=%23A22846)
![Selfhosted Badge](https://img.shields.io/badge/Self--Hosted-Yes-informational?style=for-the-badge&labelColor=%23000000&color=008000)
![pihole Badge](https://img.shields.io/badge/pihole-badge?style=for-the-badge&logo=pihole&logoColor=%2396060C&labelColor=%23000000&color=%2396060C)

<div style="text-align: center;">

![Architecture Diagram](./diagrams/architecture.png)

</div>

This repository documents a real-world Kubernetes environment running on Raspberry Pi hardware.

It focuses on practical infrastructure design, operational decision-making, and security under resource and network constraints commonly found in residential environments.

This is not a tutorial repository.  
It is a documented system.

## What this is

- A single-node k3s cluster
- Running continuously on ARM hardware
- Hosting real services used daily
- Designed with security and maintainability in mind

All workloads are deployed using raw Kubernetes manifests.

## What this demonstrates

- Kubernetes fundamentals in constrained environments
- Network and DNS architecture decisions
- Security-first thinking without overengineering
- Trade-off analysis and operational judgement
- Incremental platform design

## Repository structure

- `docs/`  
  High-level system design and architecture

- `k3s/`  
  Cluster bootstrapping, node roles, and scaling plans

- `services/`  
  Service-specific documentation

- `examples/`  
  Reference Kubernetes manifests

- `lessons-learned/`  
  Mistakes, improvements, and future work

## Current status

- Single Raspberry Pi 3 B+ node
- k3s with reduced default components
- Pi-hole, Tailscale, and Linkding deployed
- No public ingress
- Remote access via encrypted overlay network

## Future plans

- Introduce Raspberry Pi 5
- Add external SSD-backed storage
- Expand to multi-node cluster
- Improve observability and backups

These plans are documented but intentionally not rushed.

## Audience

This repository is aimed at:

- DevOps engineers
- Platform engineers
- Hiring managers
- Anyone interested in pragmatic infrastructure design

It assumes prior familiarity with Kubernetes and Linux.
