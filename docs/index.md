---
layout: default
title: Hugin Documentation
---

# Hugin Documentation

Welcome to the Hugin project documentation. Hugin is an open hardware throwable sensor ball for indoor spatial mapping.

> **"A useful toy for mapping your living room. Make it and throw it. If you missed a corner, then throw it again."**

---

## Getting Started

**New to Hugin?** Start here:

- [**Project Overview**](project_overview.md) - Comprehensive introduction, architecture, and philosophy
- [**README**](../README.md) - Quick introduction and getting started guide

---

## Development Documentation

### Setup & Planning
- [**Development TODO**](development/todo.md) - **Single source of truth** for project tasks and phases
- [**Setup Guide**](development/setup-guide.md) - Environment setup for Pico W and Jetson
- [**Testing Notes**](development/testing-notes.md) - Testing procedures and calibration templates

### Technical Specifications
- [**Architecture**](technical/architecture.md) - System architecture and data flow
- [**Hardware Specs**](technical/hardware-specs.md) - Components, pinouts, power budget, and optional sensors
- [**Communication Protocols**](technical/protocols.md) - WiFi/UDP protocol and data packet format
- [**Coordinate Systems**](technical/coordinate-systems.md) - 3D coordinate frames and transformations

### Project Progress
- [**Technical Decisions**](progress/decisions.md) - Architectural decisions and rationale
- [**Session Notes**](progress/session-notes.md) - Development session logs
- [**Issues**](progress/issues.md) - Known problems and blockers

---

## Project Status

**Current Phase:** Phase 1 - WiFi Streaming Foundation (Planning)

**Progress:**
- ✅ Project planning and documentation
- ✅ Technical decisions finalized
- ⏭️ Hardware setup and WiFi streaming implementation

See [Development TODO](development/todo.md) for detailed task breakdown.

---

## Quick Reference

### Hardware Components
- **Ball:** Raspberry Pi Pico W + MPU6050 IMU + VL53L1X ToF sensor
- **Base Station:** Jetson Orin Nano (or Raspberry Pi 4)
- **Optional Sensors:** Vacant mounts for expansion

### Key Specifications
- **Communication:** UDP over WiFi (2.4GHz), port 5000
- **Sample Rate:** 50 Hz fixed
- **Data Format:** JSON (binary planned for Phase 4)
- **Battery Target:** 30 minutes continuous operation
- **Coordinate System:** +X forward, +Y left, +Z up (right-handed)

### Development Phases
1. **Phase 1:** WiFi streaming with dummy data (current)
2. **Phase 2:** Real sensor integration
3. **Phase 3:** 3D visualization and point clouds
4. **Phase 4:** Refinement and optimization
5. **Phase 5:** Community release

---

## Project Philosophy

- **"Use what you have"** - Designed for available components, encourages substitutions
- **Build to learn** - Educational journey through embedded systems, computer vision, and SLAM
- **Open from day one** - Apache 2.0 licensed, built in public
- **Perfect is the enemy of done** - Iterate and improve over time

---

## Resources

- **GitHub Repository:** [rasmusravn/hugin](https://github.com/rasmusravn/hugin) (currently private)
- **License:** Apache 2.0
- **Community:** Public release planned for Phase 5

---

*Last updated: 2025-11-04*
