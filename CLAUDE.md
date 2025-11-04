# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugin is an open hardware throwable sensor ball for indoor spatial mapping. The ball contains a Raspberry Pi Pico W with IMU (MPU6050) and ToF distance sensor (VL53L1X) that streams data via WiFi to a Jetson Orin Nano base station for real-time 3D visualization and point cloud generation.

**Current Phase:** Phase 0 - Planning & Documentation (Completed)
**Next Phase:** Phase 1 - WiFi Streaming Foundation
**License:** Apache 2.0
**Repository:** https://github.com/rasmusravn/hugin (private)

## Documentation Structure

Phase 0 (Planning & Documentation) is complete. No code implementation exists yet. All project information lives in `/docs/`:

- **`docs/project_overview.md`** - Comprehensive project definition, architecture, milestones, and philosophy
- **`docs/development/todo.md`** - **Single source of truth** for all tasks and project phases
- **`docs/development/setup-guide.md`** - Environment setup for Pico W and Jetson
- **`docs/technical/`** - Technical specifications, protocols, hardware specs, coordinate systems
- **`docs/progress/`** - Technical decisions, session notes, and issues

**Always read `docs/development/todo.md` first** to understand current project phase and next steps.

## Architecture (Planned)

### Hardware Components
- **Ball (Throwable):** Raspberry Pi Pico W + MPU6050 IMU + VL53L1X ToF sensor + LiPo battery
- **Base Station:** Jetson Orin Nano (or Raspberry Pi 4 as alternative)

### Software Stack (To Be Implemented)
```
Pico W (MicroPython)          →  WiFi/UDP  →     Jetson (Python)
├─ Sensor drivers (I2C)                           ├─ UDP receiver
├─ WiFi connection mgmt                           ├─ Sensor fusion (quaternion-based)
└─ UDP streaming (JSON)                           ├─ 3D point cloud generation
                                                  └─ Visualization (Open3D)
```

### Communication Protocol
- **Transport:** UDP over WiFi (2.4GHz)
- **Port:** 5000 (configurable)
- **Format:** JSON (binary format documented for Phase 4)
- **Rate:** 50 Hz fixed
- **Packet Structure:**
```json
{
  "timestamp": 123456789,
  "accel": [ax, ay, az],    // m/s²
  "gyro": [gx, gy, gz],     // rad/s
  "distance": 150.5         // cm
}
```

## Critical Technical Decisions

These are **fixed architectural decisions** (see `docs/progress/decisions.md` for rationale):

1. **Coordinate System:** Right-handed, +X forward (ToF direction), +Y left, +Z up
2. **Rotation Representation:** Quaternions (avoid gimbal lock)
3. **Units:** Accelerometer in m/s², gyroscope in rad/s, distance in cm
4. **Sample Rate:** 50 Hz fixed
5. **Visualization:** Open3D library
6. **Battery Target:** 30 minutes continuous operation

## Development Workflow

### When Starting New Work
1. Read `docs/development/todo.md` to find current phase and next tasks
2. Check `docs/progress/session-notes.md` for latest progress
3. Refer to `docs/technical/` for implementation specifications

### Future Code Structure (Not Yet Created)
```
hugin/
├── pico/               # Pico W firmware (MicroPython)
│   ├── main.py
│   ├── wifi_sender.py
│   └── sensors.py
├── jetson/             # Base station software (Python)
│   ├── receiver.py
│   ├── visualizer.py
│   └── processor.py
└── tests/              # Test scripts
```

### Pico W Development (Phase 1)
- **IDE:** Thonny (recommended) or VS Code with Pico-W-Go extension
- **Firmware:** MicroPython (download from https://micropython.org/download/RPI_PICO_W/)
- **Flashing:** Hold BOOTSEL, plug in USB, drag .uf2 file to RPI-RP2 drive

### Hardware I2C Wiring (Phase 2)
- **MPU6050 IMU:** I2C0 on GP4 (SDA), GP5 (SCL)
- **VL53L1X ToF:** I2C1 on GP6 (SDA), GP7 (SCL)
- Avoid I2C address conflicts when adding optional sensors

## Project Philosophy

### "Use What You Have"
The default design uses Pico W + Jetson Orin Nano because that's what the creator had available. The project encourages substitutions:
- Alternative MCUs (ESP32, Arduino Nano 33 IoT)
- Alternative base stations (Raspberry Pi 4, laptop)
- Optional sensors via vacant mounting points (additional ToF, environmental sensors, magnetometer, etc.)

### Timeline Expectations
- **README.md** is written for **future makers** (Phase 5 release) promising "weekend project"
- **docs/** reflects **current development reality**: nights-and-weekends hobby, no fixed deadline
- Don't treat the "weekend" promise as current project timeline

### Documentation Audience Split
- **README.md** = Marketing/onboarding for future community builders
- **docs/** = Developer's current working documentation and technical specs
- Scripts like `getting_started.sh` and `next_step.sh` are **future Phase 5 features**, not current reality

## Optional Sensor Support

The ball design includes vacant mounting points for expansion sensors. When adding optional sensors:
- Use I2C bus (shared with existing sensors)
- Check for I2C address conflicts
- Recalculate power budget (target: 30 min battery life)
- Extend data streaming format if needed
- Update software to read new sensor types

## Important Notes

- **No code exists yet** - project is in planning/documentation phase
- Follow phase-based development: don't jump ahead to SLAM/ML work
- Proof of life milestone: "Throw it and capture ANY spatial data, even if messy"
- Prioritize real-time visualization "wow factor" over accuracy in early phases
- Build in public, document everything, iterate and improve
