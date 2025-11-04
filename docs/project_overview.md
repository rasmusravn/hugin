# Hugin - Open Hardware Room Scanner
## Project Overview Document

**Last Updated:** November 3, 2025  
**Project Status:** Planning & Initial Setup Phase

---

## 1. Project Concept

### What is Hugin?
Hugin is an open hardware spatial documentation tool designed as a throwable sensor ball that maps indoor spaces. Named after Odin's raven who scouts and reports back, Hugin captures spatial data during flight and streams it in real-time for visualization.

### Primary Use Cases
- Spatial documentation
- Home construction projects
- Interior design measurements
- Room mapping and floor plans

### Key Innovation
A ball you throw around a room that contains sensors, capturing 3D spatial data as it flies through the air and tumbles, with live streaming visualization.

---

## 2. Project Scope & Philosophy

### Version 1 Scope: Indoor Focus
- **Target environment:** Indoor rooms (homes, offices)
- **Approach:** Start cheap and easy, DIY kit format
- **Price target:** $50-150 DIY kit range
- **Development pace:** Nights and weekends hobby (few hours/week)
- **Timeline:** No fixed deadline - "done when it's done"

### Future Possibilities (Out of Scope for v1)
- Outdoor scanning (backyards, building exteriors)
- Long-distance throws with assisted launch
- Professional-grade accuracy
- Pre-assembled commercial product

### Design Principles
1. **Cheap:** Affordable components, expendable if broken
2. **Open:** Full documentation, community-driven improvements
3. **Educational:** Learning vehicle for embedded systems, computer vision, and software development
4. **Iterative:** Start with messy data, refine over time

---

## 3. System Architecture

### Hardware Overview

```
┌─────────────────────────────────────────────┐
│  HUGIN BALL (Throwable)                     │
│  ┌─────────────────────────────────────┐   │
│  │ Raspberry Pi Pico W                 │   │
│  │ - Reads sensors                     │   │
│  │ - WiFi streaming                    │   │
│  │ - Lightweight & cheap               │   │
│  └─────────────────────────────────────┘   │
│                                             │
│  ┌─────────────────┐  ┌─────────────────┐  │
│  │ MPU6050 IMU     │  │ VL53L1X ToF     │  │
│  │ - Acceleration  │  │ - Distance      │  │
│  │ - Gyroscope     │  │ - Single sensor │  │
│  │ - Orientation   │  │ - ~4m range     │  │
│  └─────────────────┘  └─────────────────┘  │
│                                             │
│  ┌─────────────────────────────────────┐   │
│  │ LiPo Battery + Charging Circuit     │   │
│  └─────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
                    │
                    │ WiFi Stream
                    ▼
┌─────────────────────────────────────────────┐
│  JETSON ORIN NANO (Base Station)            │
│  - Receives sensor data                     │
│  - 3D visualization                         │
│  - Point cloud processing                   │
│  - SLAM algorithms (future)                 │
│  - AI/ML capabilities (future)              │
└─────────────────────────────────────────────┘
```

### Component List

#### Already Owned
- ✅ Raspberry Pi Pico W (with WiFi)
- ✅ Jetson Orin Nano
- ✅ Raspberry Pi 4 (backup option)
- ✅ Basic electronics tools

#### To Purchase (Phase 1)
- ☐ MPU6050 IMU (~$2)
- ☐ VL53L1X ToF Distance Sensor (~$15)
- ☐ LiPo battery + charging circuit (~$10-20)
- ☐ Breadboard/jumper wires if needed

#### Future Additions (Phase 2+)
- Multiple ToF sensors (4-6 units for better coverage)
- Better battery management
- 3D printed enclosure
- Impact protection/padding

---

## 4. Milestones & Goals

### Proof of Life Milestone 🎯
**"Throw it and capture ANY spatial data, even if messy"**

This is the key achievement that validates the concept. Everything else is refinement.

### Phase 1: Foundation (Current)
**Goal:** Get Pico W streaming dummy data to Jetson over WiFi

**Tasks:**
1. Set up Pico W development environment on Ubuntu
2. Install MicroPython on Pico W
3. Write basic WiFi connection code
4. Create simple data streaming script (send dummy sensor readings)
5. Set up Jetson receiver script
6. Visualize incoming data stream

**Success criteria:** Can throw Pico W (gently!) and see data updating live on Jetson screen

### Phase 2: Real Sensors
**Goal:** Read actual IMU and ToF data

**Tasks:**
1. Wire MPU6050 to Pico W (I2C)
2. Read accelerometer/gyroscope data
3. Wire VL53L1X ToF sensor (I2C)
4. Read distance measurements
5. Stream combined sensor data to Jetson
6. Calibrate and filter noisy data

**Success criteria:** See real orientation and distance values updating during throw

### Phase 3: Spatial Visualization
**Goal:** Convert sensor stream into 3D points

**Tasks:**
1. Implement sensor fusion (combine IMU + ToF)
2. Calculate 3D position of distance measurements
3. Build point cloud from accumulated data
4. Create 3D visualization on Jetson
5. Render point cloud in real-time

**Success criteria:** Recognize room shape in the point cloud after a throw

### Phase 4: Refinement
**Goal:** Improve quality and usability

**Tasks:**
- Add more ToF sensors for better coverage
- Implement proper SLAM algorithm
- Create simple UI/controls
- Design and print ball enclosure
- Add impact protection
- Improve battery life
- Write comprehensive documentation

### Phase 5: Community Release
**Goal:** Enable others to build Hugin

**Tasks:**
- Clean up code and documentation
- Create build guide with photos
- Publish to GitHub
- Make demo videos
- Write blog posts
- Engage with maker community

---

## 5. Technical Details

### Communication Protocol
- **Method:** WiFi streaming (Pico W → Jetson)
- **Why:** Real-time visualization is the "wow factor"
- **Data format:** JSON packets (binary deferred to Phase 4)
- **Frequency:** 50Hz sensor readings fixed

### Coordinate System
- Need to establish consistent 3D coordinate frame
- IMU provides orientation relative to gravity
- ToF provides distance in sensor's facing direction
- Transform distance reading into 3D point using IMU orientation

### Power Considerations
- Pico W: ~100-150mA during WiFi transmission
- MPU6050: ~3.5mA
- VL53L1X: ~20mA
- Target: 30+ minutes of operation per charge

### Enclosure Design (Future)
- Spherical or near-spherical shape
- Sensor window for ToF (clear path)
- IMU mounted near center of mass
- Battery positioned for balance
- Impact absorption (foam, rubber bumpers)
- Easy access for charging/programming

---

## 6. Learning Goals

As an electronics engineer learning software, Hugin touches multiple areas:

### Embedded Systems
- MicroPython on Pico W
- I2C sensor communication
- Real-time data streaming
- Power management
- WiFi networking at embedded level

### Computer Vision / SLAM
- Sensor fusion algorithms
- 3D point cloud generation
- Coordinate transformations
- Kalman filtering (or similar)
- SLAM (Simultaneous Localization and Mapping)

### Software Development
- Python for Jetson processing
- Data visualization (matplotlib, Open3D, or similar)
- Network programming (sockets/UDP)
- Real-time systems
- Version control with Git

### Signal Processing
- IMU data filtering
- Noise reduction
- Sensor calibration
- Dead reckoning

---

## 7. Immediate Next Steps

### Step 1: Development Environment Setup (This Week)

#### Install Pico SDK and Tools
```bash
# Install dependencies
sudo apt update
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi \
  build-essential libstdc++-arm-none-eabi-newlib python3 python3-pip

# Install Thonny (easiest for beginners) or continue with VS Code
sudo apt install thonny

# For VS Code users: Install Pico-W-Go extension
```

#### Flash MicroPython to Pico W
1. Download latest MicroPython firmware for Pico W from:
   https://micropython.org/download/RPI_PICO_W/
2. Hold BOOTSEL button while plugging in Pico W
3. Drag and drop .uf2 file to RPI-RP2 drive
4. Pico W reboots with MicroPython installed

#### Test Basic Connection
```python
# test_blink.py - Verify Pico W is working
from machine import Pin
import time

led = Pin("LED", Pin.OUT)

while True:
    led.toggle()
    time.sleep(0.5)
```

### Step 2: WiFi Streaming Prototype (Next 1-2 Weeks)

#### On Pico W: Simple WiFi sender
```python
# wifi_sender.py - Send dummy sensor data
import network
import socket
import time
import json

# WiFi credentials
SSID = "your_network"
PASSWORD = "your_password"
JETSON_IP = "192.168.1.XXX"  # Find your Jetson's IP
JETSON_PORT = 5000

# Connect to WiFi
wlan = network.WLAN(network.STA_IF)
wlan.active(True)
wlan.connect(SSID, PASSWORD)

while not wlan.isconnected():
    time.sleep(0.1)

print(f"Connected! IP: {wlan.ifconfig()[0]}")

# Create UDP socket
sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# Send dummy data loop
counter = 0
while True:
    data = {
        "timestamp": time.ticks_ms(),
        "accel": [0.1, 0.2, 9.8],  # Dummy IMU
        "gyro": [0.0, 0.0, 0.0],   # Dummy IMU
        "distance": 150 + counter % 50  # Dummy ToF (cm)
    }
    
    message = json.dumps(data)
    sock.sendto(message.encode(), (JETSON_IP, JETSON_PORT))
    
    counter += 1
    time.sleep(0.02)  # 50Hz
```

#### On Jetson: Simple receiver
```python
# jetson_receiver.py - Receive and display data
import socket
import json

PORT = 5000

sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
sock.bind(("0.0.0.0", PORT))

print(f"Listening on port {PORT}...")

while True:
    data, addr = sock.recvfrom(1024)
    sensor_data = json.loads(data.decode())
    
    # Simple console output for now
    print(f"Distance: {sensor_data['distance']}cm | "
          f"Accel: {sensor_data['accel']}")
```

### Step 3: Order Components

**Shopping List:**
- MPU6050 IMU module (search: "MPU6050 GY-521")
- VL53L1X ToF sensor (search: "VL53L1X distance sensor")
- 3.7V LiPo battery (500-1000mAh)
- LiPo charging module (TP4056 or similar)
- Optional: small breadboard, jumper wires

**Recommended suppliers:**
- Adafruit
- SparkFun  
- Amazon (cheaper but verify quality)
- AliExpress (cheapest, longer shipping)

---

## 8. Resources & References

### Documentation
- **Raspberry Pi Pico W:** https://www.raspberrypi.com/documentation/microcontrollers/
- **MicroPython:** https://docs.micropython.org/
- **MPU6050:** https://invensense.tdk.com/products/motion-tracking/6-axis/mpu-6050/
- **VL53L1X:** https://www.st.com/en/imaging-and-photonics-solutions/vl53l1x.html

### Learning Resources
- **Pico W WiFi:** https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf
- **I2C on Pico:** https://docs.micropython.org/en/latest/library/machine.I2C.html
- **Python Point Clouds:** Open3D library (http://www.open3d.org/)

### Community
- **r/raspberry_pi** - Pico W help
- **r/embedded** - Embedded systems
- **r/computervision** - SLAM and 3D reconstruction
- **Adafruit Forums** - Hardware troubleshooting

---

## 9. Technical Decisions Status

### Decided (2025-11-03)
See `docs/progress/decisions.md` for full rationale:
- ✅ **Protocol:** UDP over WiFi, JSON format (binary deferred to Phase 4)
- ✅ **Sample rate:** 50 Hz fixed
- ✅ **Sensor units:** Accelerometer in m/s², Gyroscope in rad/s, Distance in cm
- ✅ **Rotation representation:** Quaternions (avoid gimbal lock)
- ✅ **Visualization library:** Open3D
- ✅ **Coordinate system:** +X forward (ToF direction), +Y left, +Z up

### Design Decisions (Deferred to Phase 4)
- [ ] Ball size/weight optimization
- [ ] Number of ToF sensors in final design (4-6 planned)
- [ ] Battery placement for balance
- [ ] Charging connector: USB-C, micro-USB, or wireless?
- [ ] Enclosure 3D print material (PLA, PETG, or TPU)
- [ ] SLAM algorithm choice (ORB-SLAM, Cartographer, or custom)

### Project Management (Deferred to Phase 5)
- [ ] GitHub repo structure
- [ ] License choice (likely MIT or Apache 2.0)
- [ ] Community contribution guidelines

---

## 10. Success Metrics

### Phase 1 Success (Foundation)
- ✅ Pico W connects to WiFi reliably
- ✅ Data streams to Jetson without dropouts
- ✅ Can see live updates on screen

### Phase 2 Success (Sensors)
- ✅ IMU reads acceleration and rotation
- ✅ ToF measures distances accurately (±5cm)
- ✅ Sensors work while in motion

### Phase 3 Success (Visualization)
- ✅ 3D point cloud appears on screen
- ✅ Room shape is recognizable
- ✅ Can identify walls, floor, ceiling

### Ultimate Success
- ✅ Someone else builds Hugin from documentation
- ✅ Community contributes improvements
- ✅ Actually use it for a real home project

---

## 11. Project Philosophy

**"Perfect is the enemy of done"**
- Start with something that barely works
- Iterate and improve
- Document the journey, not just the result
- Share failures and learning along the way

**"Build to learn"**
- This project is as much about learning as building
- Try things, break things, understand things
- No rush, no pressure, just curiosity

**"Open from day one"**
- Document decisions and rationale
- Share code early and often
- Make it easy for others to contribute
- Build in public

---

## Contact & Collaboration

**GitHub:** (To be created)  
**License:** (To be decided - likely MIT or Apache 2.0)  
**Status:** Planning phase - contributors welcome once Phase 1 complete

---

## Changelog

**2025-11-03:** Initial project definition and architecture planning
