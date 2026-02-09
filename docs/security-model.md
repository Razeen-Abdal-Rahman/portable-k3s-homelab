# Security Model

This document describes the threat model and security posture of the system.

The focus is on realistic risks rather than exhaustive defence.

## Scope

This model applies to:

- Network-level attacks
- Untrusted local devices
- Accidental misconfiguration
- Data exposure through services

It does not attempt to defend against all possible threats.

## Trust boundaries

- Trusted devices on the main network
- Untrusted devices on guest and IoT networks
- External access via encrypted overlay only

No implicit trust is granted based on network location alone.

## Threats addressed

- Compromised IoT devices scanning the LAN
- DNS abuse or misconfiguration
- Accidental exposure of services
- Credential reuse across services

## Threats not addressed

- Physical access to hardware
- Malicious ISP behaviour
- Nation-state level attackers
- Zero-day kernel exploits

These are out of scope by design.

## Security controls

- Network segmentation
- No inbound ports
- Encrypted remote access
- Centralised DNS control
- Minimal host surface area

Controls favour simplicity and reliability.

## Residual risks

- Single-node cluster is a single point of failure
- SD card storage is less reliable than SSD
- Dependence on third-party overlay network

These risks are accepted consciously.
