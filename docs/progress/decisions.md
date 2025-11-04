# Technical Decisions

## 2025-11-03 - Initial Architecture Choices

**Decision:** Use Raspberry Pi Pico W for sensor ball, Jetson Orin Nano for base station

**Rationale:** Pico W is cheap (~$6), has WiFi built-in, and is lightweight. Jetson provides powerful processing for future SLAM/ML work.

**Alternatives:**
- ESP32: Considered but Pico W has better documentation and I already own it
- Raspberry Pi Zero W: Too bulky and power-hungry for throwable ball
- Process on Pico itself: Not enough compute power for 3D visualization

---

## 2025-11-03 - Communication Protocol

**Decision:** UDP over WiFi for streaming sensor data

**Rationale:** Real-time visualization is priority, some packet loss acceptable. UDP is simpler and lower latency than TCP.

**Alternatives:**
- TCP: More reliable but adds latency and complexity for real-time streaming
- Bluetooth: Too short range, more complex pairing
- Store locally and download: Loses "wow factor" of real-time visualization

---

## 2025-11-03 - Technical Specifications Decided

### Sensor Units
**Decision:**
- Accelerometer: m/s² (SI units)
- Gyroscope: rad/s (radians per second)
- Distance: Centimeters

**Rationale:**
- m/s² and rad/s are standard for scientific/engineering work and work better with Python math libraries
- Centimeters provide good precision for room-scale measurements without excessive decimals
- Consistent SI-based approach (except distance for practical reasons)

### Rotation Representation
**Decision:** Quaternions

**Rationale:**
- No gimbal lock issues
- Industry standard for IMU sensor fusion
- Better mathematical properties for 3D transformations
- Worth the learning curve for long-term project quality

**Alternatives:**
- Euler angles: Easier to understand but suffer from gimbal lock

### Sample Rate
**Decision:** 50Hz fixed

**Rationale:**
- Good balance of temporal resolution and battery life
- Sufficient for human-speed throws
- Simpler implementation than adaptive rate
- 20ms between packets is manageable for WiFi

**Future:** May increase to 100Hz if battery life permits

### Data Protocol
**Decision:** JSON (for now)

**Rationale:**
- Human-readable for debugging during development
- Easier to develop and test
- WiFi bandwidth at 50Hz is sufficient
- Can migrate to binary later if needed

**Future:** Binary protocol is documented and ready for Phase 4 optimization

### Visualization Library
**Decision:** Open3D

**Rationale:**
- Professional-grade point cloud library
- Built specifically for 3D reconstruction and SLAM
- Will grow with the project as we add SLAM in Phase 4
- Jetson Orin Nano has plenty of power to handle it

### IMU Coordinate System
**Decision:** +X axis points in ToF measurement direction

**Rationale:**
- Standard robotics convention
- Simplifies transformation calculations
- Right-handed coordinate system

**Mounting orientation:**
- IMU +X: Forward (ToF pointing direction)
- IMU +Y: Left
- IMU +Z: Up (when ball is level)

---

