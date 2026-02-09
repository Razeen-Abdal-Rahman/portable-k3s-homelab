# Network Design

This document outlines the network topology and trust boundaries.

Exact addresses and identifiers are intentionally omitted.

## Physical topology

- ISP-provided router acts as the primary gateway
- Raspberry Pi connects via Ethernet
- Additional hardware operates in switch or access point mode only
- Wi-Fi is extended using mesh access points

There is no double NAT.

## Logical segmentation

The network is logically segmented into:

- Trusted network for personal devices
- Guest and IoT network for untrusted devices
- Isolated network for CCTV devices

Segmentation is enforced by the router and access points rather than explicit VLAN tagging.

## DNS architecture

- Router advertises Pi-hole as the DNS server
- Pi-hole handles queries for all networks
- DHCP remains managed by the router

This avoids guest network breakage caused by DHCP limitations on the router.

## Why DNS is central

Placing Pi-hole at the DNS layer provides:

- Visibility into network activity
- Centralised control
- Minimal client configuration
- Reduced attack surface compared to per-device agents

## Remote access

Remote access is provided via an encrypted mesh overlay:

- No exposed services
- No port forwarding
- No inbound firewall rules

Access is identity-based rather than network-based.

## Attack surface

Externally exposed surface is limited to:

- Outbound connections initiated by the node
- Encrypted overlay network traffic

There are no publicly reachable services.
