# Tailscale Service

Tailscale provides secure remote access to the cluster.

It replaces traditional VPN and port forwarding.

## Why Tailscale

- No inbound ports
- Identity-based access
- Encrypted by default
- Simple operational model

It aligns well with a zero-trust approach.

## Deployment model

- Deployed as a DaemonSet
- Runs on the node host network
- Uses Kubernetes RBAC

This allows cluster-wide access when scaled.

## Security posture

- No services are publicly exposed
- Access requires authenticated identity
- Network trust is not assumed

The local network remains private.

## Operational benefits

- Easy remote administration
- No firewall changes
- No router configuration

This significantly reduces attack surface.

## Trade-offs

- Dependency on a third-party service
- Requires external coordination

These risks are accepted.
