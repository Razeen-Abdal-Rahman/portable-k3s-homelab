# Mistakes and Missteps

This document captures mistakes made during the project.

They are documented deliberately.

## Outdated OS image

Using an old Raspberry Pi OS image caused:

- Broken package updates
- Wasted troubleshooting time
- Unnecessary reinstallation

Lesson: always start from a known-good base.

## Overestimating hardware

Initial assumptions underestimated:

- Memory pressure
- Storage latency
- Kubernetes overhead

Lesson: validate assumptions early.

## DHCP via Pi-hole

Attempting to move DHCP to Pi-hole caused:

- Guest network failure
- Router incompatibility
- Unexpected downtime

Lesson: consumer hardware has hard limits.

## Lack of prior documentation

Previous Pi-hole experience was undocumented.

This increased setup time significantly.

Lesson: write things down while they are fresh.
