# System Architecture

## Overview

```
┌─────────────────────────┐
│   HUGIN BALL            │
│   (Raspberry Pi Pico W) │
│   - MPU6050 IMU         │
│   - VL53L1X ToF         │
│   - WiFi Streaming      │
└───────────┬─────────────┘
            │ UDP/WiFi
            ▼
┌─────────────────────────┐
│   BASE STATION          │
│   (Jetson Orin Nano)    │
│   - Data Processing     │
│   - Sensor Fusion       │
│   - 3D Visualization    │
└─────────────────────────┘
```

## Data Flow

1. **Sensor Reading** (Pico W @ ~50-100Hz)
   - Read IMU (accelerometer, gyroscope)
   - Read ToF distance sensor

2. **Data Packaging** (Pico W)
   - Combine readings with timestamp
   - Serialize to JSON or binary

3. **Transmission** (Pico W → Jetson)
   - Send UDP packets over WiFi

4. **Processing** (Jetson)
   - Receive and parse packets
   - Apply sensor fusion
   - Calculate 3D point positions

5. **Visualization** (Jetson)
   - Update point cloud
   - Render in real-time

## Software Components

### Pico W Firmware (MicroPython)
- Sensor drivers (I2C communication)
- WiFi connection management
- UDP streaming

### Jetson Software (Python)
- UDP receiver
- Sensor fusion algorithms (quaternion-based)
- 3D visualization (Open3D)
- Future: SLAM implementation

## Performance Targets

- **Sensor sample rate:** 50 Hz (fixed)
- **Packet rate:** 50 packets/second
- **Expected latency:** <100ms end-to-end
- **Battery life:** 30+ minutes continuous operation (target), 2-5 hours possible with 1000mAh battery

## Future Enhancements

- Multiple ToF sensors for better coverage
- SLAM algorithm for better spatial accuracy
- Data logging for offline analysis
- Mobile app for visualization
