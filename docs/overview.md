# Project Overview

This repository documents a portable, security-focused Kubernetes environment built on Raspberry Pi hardware.

The goal of the project is to demonstrate practical infrastructure design, operational decision-making, and security awareness under real-world constraints.

This is a real, running system, not a theoretical design or tutorial.

## Why this exists

I wanted a personal infrastructure environment that:

- Runs continuously in a residential setting
- Prioritises security and privacy by default
- Can be relocated without redesigning the system
- Uses production-grade tools in a constrained environment

At the same time, this project serves as a professional demonstration of my approach to DevOps and platform engineering.

## Core goals

- Secure by default, minimal attack surface
- Clear trust boundaries between devices
- Predictable and observable behaviour
- Extensible design for future growth
- Operational simplicity over cleverness

## Non-goals

- High availability at this stage
- Enterprise-scale performance
- Step-by-step tutorials
- Fully automated GitOps workflows

Those are deliberate exclusions, not oversights.

## Current state

- Single-node k3s cluster on Raspberry Pi 3 B+
- Raspberry Pi OS Lite, headless
- All services deployed as Kubernetes workloads
- No services exposed directly to the internet
- Remote access via encrypted mesh networking

The cluster is resource constrained and intentionally simple.

## Real-world constraints

This system operates within typical residential limitations:

- Consumer ISP-provided router
- Mixed trusted and untrusted devices
- Limited power and cooling
- ARM hardware with 1 GB of RAM

Design decisions are shaped by these constraints.

## Intended audience

This documentation is written for engineers and hiring managers who want to understand:

- How infrastructure decisions are made
- How trade-offs are evaluated
- How systems behave under constraint

It is not intended as a beginner guide.
