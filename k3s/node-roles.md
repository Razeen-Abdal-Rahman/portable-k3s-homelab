# Node Roles and Responsibilities

This document outlines how node roles are handled now and how they are expected to evolve.

## Current state

- Single node
- Control plane and workloads run together
- No explicit node labels

This is appropriate for the current hardware.

## Workload placement

All workloads are scheduled on the same node.

Resource usage is controlled primarily by:

- Pod resource limits
- Application-level configuration
- Selective service deployment

## Planned roles

When a Raspberry Pi 5 is added:

- Existing Pi 3 B+ will retain control plane responsibilities
- Pi 5 will handle:
  - Stateful workloads
  - Storage-heavy services
  - User-facing applications

## Node labelling

Planned labels include:

- `node-role=control-plane`
- `node-role=worker`
- `storage=fast`

These will be used to control workload placement explicitly.

## Why roles matter

Separating responsibilities allows:

- Better resource utilisation
- Reduced blast radius
- Clearer operational reasoning
- Easier future scaling

Roles are deferred until they provide real value.
