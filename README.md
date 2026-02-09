# portable-k3s-homelab

A  production-minded Kubernetes homelab demonstrating infrastructure design, security architecture, and operational discipline at personal scale.

Built on Raspberry Pi hardware, this project showcases practical implementation of container orchestration, network security, and infrastructure-as-code principles in a resource-constrained environment.

---

## Project Overview

This repository documents a working Kubernetes cluster deployment that balances security, portability, and operational simplicity. It demonstrates:

- **Infrastructure design:** Architectural decisions with clear rationale and trade-offs
- **Security implementation:** Network segmentation, zero-trust access, and defence in depth
- **Operational discipline:** GitOps principles(planned), documentation standards, and disaster recovery planning
- **Technical breadth:** Kubernetes, networking, DNS, containerisation, and Linux system administration

The cluster runs real services in production use, not demo applications.

---

## Technical Stack

### Compute

- **Orchestration:** k3s (lightweight Kubernetes)
- **Hardware:** Raspberry Pi 3 B+ (1GB RAM, ARM64)
- **Host OS:** Raspberry Pi OS 64-bit (Debian-based), headless
- **Architecture:** Single-node cluster (control plane + workloads)

### Networking

- **Segmentation:** VLAN-based isolation (trusted/guest networks)
- **DNS:** Pi-hole (network-wide DNS filtering and monitoring)
- **Recursive DNS:** Unbound (planned)
- **Remote Access:** Tailscale (WireGuard-based mesh VPN)
- **Security Posture:** Zero exposed ports, no port forwarding

### Services (Kubernetes-native)

- **Pi-hole:** DNS-level ad blocking and network monitoring
- **Tailscale:** Authenticated remote access mesh network
- **Linkding:** Bookmark management and URL archiving
- **NAS:** Planned (SMB/NFS file sharing)
- **Immich:** Planned (self-hosted photo management)

### Storage

- **System:** MicroSD (OS and k3s state)
- **Persistent Data:** Local storage (external USB, future expansion planned)
- **Strategy:** Local-first, with planned migration to distributed storage as cluster grows

---

## Architecture principles

### Security and privacy

- No public internet exposure (zero port forwarding)
- Network segmentation via VLANs and firewall rules
- DNS-level monitoring and control (Pi-hole)
- Encrypted remote access only (Tailscale/WireGuard)
- Principle of least privilege across all services

### Portability

- All services containerised in Kubernetes
- Infrastructure-as-code (declarative manifests)
- Hardware abstraction for future migration
- Designed for physical relocation without service interruption

### Operational simplicity

- Single-node deployment (deliberate complexity management)
- Minimal host-level configuration
- GitOps-ready workflow
- Clear disaster recovery procedures

### Real-world constraints

- Consumer-grade networking equipment
- Residential internet connection
- Mixed trusted/untrusted device environment
- No datacenter power, cooling, or redundancy

---

## Repository Structure

```text
.
├── README.md                    # This file
├── docs/                        # Architecture and design documentation
│   ├── architecture.md          # System architecture and component relationships
│   ├── network-design.md        # Network topology, VLANs, and security boundaries
│   ├── overview.md              # High-level project overview and context
│   ├── security-model.md        # Threat model and security implementation
│   └── storage-strategy.md      # Storage architecture and data management
├── examples/                    # Reference Kubernetes manifests
│   ├── pihole/                  # Pi-hole DNS deployment
│   ├── tailscale/               # Tailscale mesh VPN
│   └── linkding/                # Bookmark management (planned)
├── k3s/                         # Kubernetes cluster documentation
│   ├── bootstrap.md             # Initial cluster setup and configuration
│   ├── node-roles.md            # Node responsibilities and future scaling
│   └── scaling.md               # Multi-node expansion strategy
├── lessons-learned/             # Post-mortems and reflections
│   ├── improvements.md          # Planned enhancements and iterations
│   └── mistakes.md              # What didn't work and why
└── services/                    # Service-specific documentation
    ├── pihole.md                # Pi-hole deployment and configuration
    ├── tailscale.md             # Tailscale setup and usage
    └── linkding.md              # Linkding deployment
```

---

## Key Technical Decisions

### Why Kubernetes at Personal Scale?

**Not for scalability.** For discipline and future-proofing.

Kubernetes enforces:

- Declarative configuration (infrastructure-as-code)
- Clear service boundaries and separation of concerns
- Portable workloads (hardware-agnostic deployment)
- Proven operational patterns (health checks, rolling updates, resource management)

The overhead is significant at single-node scale, but the investment pays off in:

- Simplified service addition and migration
- Consistent deployment patterns across all workloads
- Easier physical relocation (cluster manifest portability)
- Foundation for future multi-node expansion

**Trade-off accepted:** Higher resource usage and operational complexity in exchange for long-term flexibility and professional-grade tooling experience.

### Why Single-Node Initially?

High availability is not a requirement for personal infrastructure. Downtime is measured in hours, not minutes.

A single-node cluster:

- Reduces operational complexity (no distributed state management)
- Lowers hardware cost and power consumption
- Simplifies debugging and troubleshooting
- Still provides full Kubernetes API and workflow benefits

Multi-node expansion is planned and architecturally supported, but deferred until workload or redundancy requirements justify the complexity.

### Why Raspberry Pi OS?

Stability over cutting-edge features.

- Reference platform for Raspberry Pi hardware (best driver/firmware support)
- Debian-based (familiar package ecosystem, stable release cycle)
- Minimal attack surface (headless, no desktop environment)
- Extensive community documentation

Alternative considered: Ubuntu Server (more enterprise-familiar, occasionally hardware compatibility issues on ARM).

### Why Local Storage?

At 1-3 node scale, distributed storage (Ceph, Longhorn, Rook) adds complexity disproportionate to benefit.

Local storage provides:

- Better performance (no network overhead)
- Simpler failure modes (restore from backup vs distributed consensus issues)
- Lower resource overhead (no replication coordination)

**Migration path:** If cluster scales beyond 3 nodes or redundancy requirements change, transition to distributed storage is architecturally supported.

### Why Tailscale Over Self-Hosted VPN?

Operational simplicity and attack surface reduction.

**Tailscale advantages:**

- Zero port forwarding required (no exposed attack surface)
- No static IP or dynamic DNS needed
- WireGuard protocol (modern, performant, audited)
- Cross-platform clients (Linux, macOS, Windows, iOS, Android)
- Keys remain local (coordination server cannot decrypt traffic)

**Trade-off:** Dependency on Tailscale's coordination service. Accepted because the security and operational benefits outweigh the risk. Fallback: local network access remains available if Tailscale is down.

### Why Pi-hole as Infrastructure DNS?

DNS is foundational infrastructure, not an optional add-on.

**Pi-hole provides:**

- Network-wide visibility (all DNS queries logged and queryable)
- Granular control (block unwanted domains at DNS layer)
- Client-agnostic (affects all devices without per-device configuration)
- Upstream flexibility (configurable forwarders: Cloudflare, Quad9, etc.)

**Not just ad-blocking:** This is about network hygiene, monitoring, and control.

**Failure consideration:** Pi-hole is a single point of failure for DNS. Mitigation: rapid recovery procedures documented, monitored uptime, future redundancy via multi-node deployment.

---

## What This Demonstrates

### Infrastructure Engineering

- Architectural decision-making with documented trade-offs
- Security-first design (defence in depth, zero trust access)
- Operational discipline (disaster recovery, documentation standards)
- Capacity planning and resource constraint management

### Kubernetes Expertise

- k3s deployment and configuration
- Service deployment patterns (Deployments, DaemonSets, StatefulSets)
- Networking (Services, Ingress planning, CNI awareness)
- Storage management (PersistentVolumes, local vs distributed storage)
- Resource management (requests/limits in constrained environment)

### Security Implementation

- Network segmentation (VLANs, firewall rules, trust boundaries)
- Zero-trust remote access (Tailscale/WireGuard)
- Attack surface minimisation (no exposed ports, minimal host services)
- Threat modelling and risk acceptance (documented in security-model.md)

### Linux Systems Administration

- Debian/Raspberry Pi OS system hardening
- Service management and monitoring
- Network configuration and troubleshooting
- Storage and filesystem management

### Documentation and Communication

- Clear technical writing for varied audiences
- Architecture documentation with diagrams
- Operational runbooks and procedures
- Honest reflection on mistakes and improvements

---

## Current Status and Roadmap

### Operational (Production Use)

- ✅ Pi-hole (DNS filtering and monitoring)
- ✅ Tailscale (remote access mesh)
- ✅ Linkding (bookmark management)

### Planned (Near Term)

- 🔄 Unbound (recursive DNS resolver)
- 🔄 NAS (SMB/NFS file sharing with external storage)
- 🔄 Immich (photo management and backup)
- 🔄 Raspberry Pi 5 as second node (workload distribution testing)

### Planned (Medium Term)

- Monitoring and observability (Prometheus/Grafana or lightweight alternative)
- Automated backup pipeline (local + offsite replication)
- Service mesh evaluation (Linkerd or Cilium for encrypted inter-service communication)
- ISP router replacement (dedicated firewall/router hardware)

### Long Term

- Multi-node high availability (3+ node cluster)
- Physical relocation support (cluster migration procedures)
- Advanced storage (distributed storage layer as cluster grows)

---

## Skills Demonstrated

| Category | Technologies/Concepts |
| ---------- | ---------------------- |
| **Container Orchestration** | Kubernetes (k3s), Docker, container networking, resource management |
| **Networking** | TCP/IP, DNS (Pi-hole, Unbound), VLANs, VPN (WireGuard/Tailscale), firewall configuration |
| **Linux Systems** | Debian/Raspberry Pi OS, systemd, shell scripting, package management |
| **Security** | Network segmentation, zero-trust architecture, threat modelling, encryption (WireGuard) |
| **Infrastructure as Code** | Declarative Kubernetes manifests, GitOps principles, version-controlled configuration |
| **Documentation** | Technical writing, architecture diagrams, operational runbooks, decision records |
| **Problem Solving** | Constraint-based design, trade-off analysis, debugging in resource-limited environments |

---

## Why This Matters

This isn't a tutorial project or a lab exercise. This is production infrastructure serving real use cases under real constraints.

**It demonstrates:**

- Ability to design and implement complex systems from first principles
- Understanding of security, networking, and operational best practices
- Discipline to document decisions, learn from failures, and iterate
- Practical application of enterprise-grade tools in non-enterprise environments
- Balancing ideal solutions with real-world constraints (budget, power, complexity)

Personal infrastructure built with the same rigor as professional infrastructure.

---

## Contact

For questions about this project, technical discussions, or opportunities:

- **LinkedIn:** [Razeen Abdal-Rahman](https://www.linkedin.com/in/razeen-abdal-rahman/)
- **GitHub:** [@Razeen-Abdal-Rahman](https://github.com/Razeen-Abdal-Rahman)
- **Email:** [Razeen.Abdal-Rahman@outlook.com](mailto:Razeen.Abdal-Rahman@outlook.com?subject=Nice%20homelab%20Proejct!)
