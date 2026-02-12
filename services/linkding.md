# Linkding Service

Linkding is a self-hosted bookmark manager.

It represents a stateful, user-facing workload.

## Why Linkding

- Simple architecture
- Useful daily service
- Low operational complexity
- Requires persistent storage

It is well suited to constrained environments.

## Deployment challenges

On Raspberry Pi 3 B+:

- Django migrations were slow
- Memory pressure caused crashes
- Default uWSGI settings were too aggressive

These issues required tuning.

## Mitigations

- Reduced uWSGI worker and thread counts
- Explicit resource limits
- Re-enabled local storage

This stabilised the service.

## Persistence

Data is stored using a PersistentVolumeClaim.

This makes:

- Backups simpler
- Rebuilds predictable
- Failure modes clear

## Why this matters

Running Linkding surfaced real operational concerns that purely stateless services do not.

This was intentional.
