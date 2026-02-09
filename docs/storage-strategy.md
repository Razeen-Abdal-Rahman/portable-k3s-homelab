# Storage Strategy

This document describes how data is stored, persisted, and recovered.

## Current state

- OS and Kubernetes state reside on SD card
- Persistent volumes use local storage
- Stateful services are limited due to hardware constraints

This reflects the current hardware reality.

## Persistent data

Data requiring persistence includes:

- Pi-hole configuration
- Linkding application data
- Future NAS and media workloads

Each service declares its own storage requirements.

## Backup approach

Backups focus on:

- Service configuration
- Application data
- Kubernetes manifests

Full node rebuild is preferred over in-place repair.

## Disaster recovery

In the event of node failure:

- Reinstall OS
- Reinstall k3s
- Reapply manifests
- Restore application data

This process is documented in the private repository.

## Planned evolution

- External SSD via M.2 HAT on Raspberry Pi 5
- Migration of storage-heavy workloads
- Clear separation of compute and data
- Improved backup automation

Distributed storage is deferred until multiple nodes exist.

## Trade-offs

Local storage is chosen for:

- Predictability
- Simplicity
- Performance on limited hardware

Redundancy is traded for operational clarity.
