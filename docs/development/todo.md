# Development TODO
**Authoritative task list - Last updated: 2025-11-04**

> **Note:** This is the single source of truth for project tasks.

---

## Current Focus: Phase 0 - Planning & Documentation

### Completed
- [x] Project concept definition
- [x] Architecture planning
- [x] Technical decisions (coordinate systems, units, protocols)
- [x] Hardware component selection
- [x] Documentation structure
- [x] GitHub repository setup
- [x] License selection (Apache 2.0)
- [x] README and project overview

### In Progress
- [ ] Review Phase 0 deliverables
  - [ ] Review all technical decisions for completeness
  - [ ] Verify documentation accuracy and consistency
  - [ ] Check for missing specifications
  - [ ] Validate hardware component choices
  - [ ] Ensure all Phase 0 success criteria are met

### Up Next
- [ ] Complete Phase 0 review and close phase
- [ ] Order hardware components (MPU6050, VL53L1X, battery)
- [ ] Begin Phase 1: WiFi Streaming Foundation

---

## Phase 0: Planning & Documentation
**Goal:** Define project scope, architecture, and technical specifications
**Success Criteria:** Complete documentation and technical decisions finalized

- [x] Define project concept and goals
  - [x] Define primary use cases (spatial documentation, home construction, interior design)
  - [x] Establish key innovation (throwable sensor ball with live streaming)
  - [x] Set version 1 scope (indoor focus, DIY kit, $50-150 price target)
  - [x] Define design principles (cheap, open, educational, iterative)
  - [x] Identify "Proof of Life" milestone
- [x] Research and select hardware components
  - [x] Select MCU: Raspberry Pi Pico W (WiFi, lightweight, cheap)
  - [x] Select IMU: MPU6050 (accelerometer + gyroscope)
  - [x] Select distance sensor: VL53L1X ToF (~4m range)
  - [x] Select base station: Jetson Orin Nano (powerful for future SLAM/ML)
  - [x] Plan battery: LiPo with 30-minute runtime target
  - [x] Document component rationale and alternatives
  - [x] Calculate power budget (~175mA total)
- [x] Plan system architecture (Pico W + Jetson)
  - [x] Design two-component system (ball + base station)
  - [x] Define data flow (sensors → Pico W → WiFi → Jetson → visualization)
  - [x] Plan software components (MicroPython firmware, Python receiver)
  - [x] Document hardware I2C wiring (I2C0: MPU6050, I2C1: VL53L1X)
  - [x] Design for optional sensor expansion (vacant mounts)
- [x] Decide on communication protocol (UDP/WiFi)
  - [x] Choose UDP over TCP (lower latency, acceptable packet loss)
  - [x] Define port: 5000 (configurable)
  - [x] Select data format: JSON (binary deferred to Phase 4)
  - [x] Set sample rate: 50 Hz fixed
  - [x] Document packet structure with field descriptions
- [x] Define coordinate system and sensor units
  - [x] Choose right-handed coordinate system (+X forward, +Y left, +Z up)
  - [x] Set accelerometer units: m/s² (SI standard)
  - [x] Set gyroscope units: rad/s (radians per second)
  - [x] Set distance units: centimeters (practical precision)
  - [x] Choose quaternions for rotation representation (avoid gimbal lock)
  - [x] Document IMU mounting orientation
- [x] Document all technical decisions with rationale
  - [x] Create decisions.md with all architectural choices
  - [x] Document alternatives considered for each decision
  - [x] Explain rationale for hardware selections
  - [x] Record decisions on protocols, units, and algorithms
  - [x] Mark future decisions to be deferred
- [x] Create comprehensive project documentation
  - [x] Write project_overview.md (concept, architecture, milestones, philosophy)
  - [x] Create technical documentation (architecture, hardware specs, protocols, coordinate systems)
  - [x] Write development documentation (setup guide, todo list, testing notes)
  - [x] Document progress (decisions, session notes, issues)
  - [x] Create documentation navigation structure
- [x] Set up GitHub repository
  - [x] Initialize git repository
  - [x] Create .gitignore for Python, MicroPython, embedded systems
  - [x] Create private GitHub repository
  - [x] Set up remote and push initial commit
  - [x] Add future ideas (edge AI/ML, standalone mode)
- [x] Choose open source license
  - [x] Decide on Apache 2.0 license
  - [x] Create LICENSE file with copyright
  - [x] Update all documentation with license choice
- [x] Write README for future makers
  - [x] Write welcoming introduction with project concept
  - [x] Explain "Use what you have" philosophy
  - [x] Add getting started instructions (for future Phase 5)
  - [x] Include git clone URL
  - [x] Style with markdown formatting and emojis
- [x] Set up GitHub Pages for documentation
  - [x] Create docs/index.md navigation hub
  - [x] Configure Jekyll with Cayman theme
  - [x] Set up _config.yml for GitHub Pages
  - [x] Create docs/README.md as alternative entry point
  - [x] Focus Pages on development documentation only
- [x] Create CLAUDE.md for future AI instances
  - [x] Document project overview and current phase
  - [x] Explain documentation structure
  - [x] Define critical technical decisions
  - [x] Document planned architecture
  - [x] Explain project philosophy and audience split
- [ ] Review Phase 0 deliverables
  - [ ] Review all technical decisions for completeness
  - [ ] Verify documentation accuracy and consistency
  - [ ] Check for missing specifications or undocumented choices
  - [ ] Validate hardware component selections against requirements
  - [ ] Ensure all Phase 0 success criteria are met
  - [ ] Identify any gaps before moving to Phase 1

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
