# k3s Bootstrap Process

This document describes how the k3s cluster was installed and stabilised.

The process was iterative and influenced heavily by hardware constraints.

## Initial setup

- Raspberry Pi OS Lite installed via Raspberry Pi Imager
- Headless configuration
- SSH-only access
- System updates applied immediately

An early mistake was attempting to use an outdated OS image which could not be upgraded reliably.

## k3s installation

k3s was selected due to:

- Low resource footprint
- Simple installation
- Bundled components
- Strong ARM support

The cluster is installed using the default installer with custom flags.

## Disabled components

Several default components were removed to improve performance:

- Traefik
- ServiceLB
- Metrics Server
- Default local storage (initially)

These components introduced unnecessary overhead on the Pi 3 B+.

## Performance tuning

After initial deployment:

- Response times were inconsistent
- Pod scheduling was slow
- Memory pressure caused instability

Removing non-essential components significantly improved responsiveness.

## Storage reintroduction

Local storage was later re-enabled to support stateful workloads such as Linkding.

This was done deliberately and with awareness of the trade-offs.

## Outcome

The resulting cluster:

- Is responsive and stable
- Uses minimal resources
- Supports essential workloads
- Avoids unnecessary abstraction

This process reinforced the importance of incremental validation.
