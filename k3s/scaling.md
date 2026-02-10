# Scaling Strategy

This document explains how scaling is approached and why it is intentionally conservative.

## Current limitations

- Single node
- Single point of failure
- No workload redundancy

This is a known and accepted state.

## Scaling goals

Scaling is driven by:

- Storage requirements
- Performance bottlenecks
- Operational simplicity

Not by novelty.

## Horizontal scaling

Planned steps:

1. Add second node
2. Move workloads selectively
3. Avoid premature HA control plane

Each step will be validated before proceeding.

## Vertical scaling

Vertical scaling is prioritised initially:

- Better hardware
- External SSD
- Improved cooling

This provides immediate benefits with minimal complexity.

## What scaling is not

Scaling is not:

- Automatic
- Elastic
- Cloud-like

This environment prioritises predictability over abstraction.

## Long-term view

True high availability may be implemented later, but only when justified by actual usage patterns.
