# Development TODO
**Authoritative task list - Last updated: 2025-11-03**

> **Note:** This is the single source of truth for project tasks.

---

## Current Focus: Phase 1 - WiFi Streaming Foundation

### In Progress
- [ ]

### Up Next
- [ ] Set up Pico W development environment
- [ ] Flash MicroPython to Pico W
- [ ] Test basic WiFi connection
- [ ] Create UDP sender on Pico W (dummy data)
- [ ] Create UDP receiver on Jetson
- [ ] Verify live data streaming works

---

## Phase 1: Foundation - WiFi Streaming
**Goal:** Get Pico W streaming dummy data to Jetson over WiFi
**Success Criteria:** See dummy sensor data streaming live on Jetson screen (no throwing needed yet)

- [ ] Set up Pico W development environment (see `setup-guide.md`)
- [ ] Flash MicroPython to Pico W
- [ ] Test basic WiFi connection
- [ ] Create UDP sender on Pico W (dummy sensor data)
- [ ] Create UDP receiver on Jetson
- [ ] Test data streaming with dummy values
- [ ] Verify live updates work on screen

---

## Phase 2: Real Sensors
**Goal:** Read actual IMU and ToF data
**Success Criteria:** Can throw Pico W and see real orientation and distance values updating live during flight

### Hardware Acquisition
- [ ] Order MPU6050 IMU (~$2)
- [ ] Order VL53L1X ToF sensor (~$15)
- [ ] Order LiPo battery + charging circuit (~$10-20)

### Integration
- [ ] Wire MPU6050 to Pico W (I2C0: GP4/GP5 - see `../technical/hardware-specs.md`)
- [ ] Install MPU6050 MicroPython library
- [ ] Read and validate accelerometer/gyroscope data
- [ ] Wire VL53L1X to Pico W (I2C1: GP6/GP7)
- [ ] Install VL53L1X MicroPython library
- [ ] Read and validate distance measurements
- [ ] Stream combined real sensor data to Jetson
- [ ] Implement sensor calibration routines
- [ ] Apply noise filtering to sensor data
- [ ] Test by throwing the Pico W and observing sensor data

---

## Phase 3: Spatial Visualization
**Goal:** Convert sensor stream into 3D points
**Success Criteria:** Throw the ball and recognize room shape in the resulting point cloud

- [ ] Decide on coordinate system conventions (see Undecided Questions below)
- [ ] Implement sensor fusion algorithm (combine IMU + ToF)
- [ ] Calculate 3D point positions from orientation + distance
- [ ] Build point cloud data structure on Jetson
- [ ] Install 3D visualization library (Open3D or matplotlib)
- [ ] Create real-time 3D visualization
- [ ] Test with actual room throw
- [ ] Validate: Can we identify walls, floor, ceiling?

---

## Phase 4: Refinement
**Goal:** Improve quality and usability

- [ ] Add multiple ToF sensors (4-6 units for better coverage)
- [ ] Implement proper SLAM algorithm (research: ORB-SLAM, Cartographer, or custom)
- [ ] Create simple UI/controls for Jetson
- [ ] Design ball enclosure (CAD model)
- [ ] 3D print enclosure prototype
- [ ] Add impact protection (foam, rubber bumpers)
- [ ] Optimize battery life and power management
- [ ] Write comprehensive user documentation

---

## Phase 5: Community Release
**Goal:** Enable others to build Hugin

- [ ] Clean up and comment code
- [ ] Write detailed build guide with photos
- [ ] Create public GitHub repository
- [ ] Choose open source license (likely MIT or Apache 2.0)
- [ ] Make demo video showing throw and visualization
- [ ] Write blog post about project and learnings
- [ ] Share with maker community (r/raspberry_pi, r/embedded, Adafruit forums)

---

## Backlog / Future Ideas
- Support for multiple sensors in parallel
- Mobile app for visualization
- Data logging and replay functionality
- Offline SLAM processing
- Export point clouds to CAD formats (STL, PLY)
- Web interface for visualization
- Outdoor scanning support (future version)
- GPS integration for outdoor use

### Advanced Future Concepts
- **Edge AI/ML Point Cloud Reconstruction:** Integrate edge TPU (Google Coral, etc.) for AI-powered gap filling and denoising
  - Use ML models to interpolate between sparse measurements
  - Generate complete 3D models/images from partial scans
  - Real-time or post-processing enhancement of point clouds
  - Trained models for indoor geometry reconstruction
- **Standalone Ball Mode:** Self-contained operation without base station
  - Add more powerful compute module to ball (Raspberry Pi Zero 2 W, Jetson Nano module, etc.)
  - Onboard data processing and storage
  - Download mapping results after throws via USB or WiFi
  - Battery-powered visualization on small OLED display
  - Reduces setup complexity - just throw and retrieve

---

## Blocked / Waiting
- **Phase 2 start:** Waiting for component delivery (not yet ordered)

---

## Technical Specifications (Decided 2025-11-03)
**See `../progress/decisions.md` for full details:**

- ✅ **Accelerometer units:** m/s² (SI units)
- ✅ **Gyroscope units:** rad/s (radians per second)
- ✅ **Angle representation:** Quaternions
- ✅ **Distance units:** Centimeters
- ✅ **Target sample rate:** 50Hz fixed
- ✅ **Data protocol:** JSON (binary deferred to Phase 4)
- ✅ **Coordinate system:** +X forward (ToF direction), +Y left, +Z up
- ✅ **3D visualization library:** Open3D
- ⏭️ **SLAM algorithm:** Choice deferred to Phase 4
