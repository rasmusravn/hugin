# Hardware Specifications

## Bill of Materials

### Owned Components
- ✅ Raspberry Pi Pico W
- ✅ Jetson Orin Nano
- ✅ Raspberry Pi 4 (backup)

### To Purchase (Phase 1)
- ☐ MPU6050 IMU (~$2)
- ☐ VL53L1X ToF Distance Sensor (~$15)
- ☐ LiPo battery + charging circuit (~$10-20)
- ☐ Breadboard/jumper wires

### Future Additions
- Multiple ToF sensors (4-6 units)
- 3D printed enclosure
- Impact protection/padding

---

## Component Details

### Raspberry Pi Pico W
- **Microcontroller:** RP2040 dual-core ARM Cortex-M0+ @ 133MHz
- **Memory:** 264KB SRAM
- **Storage:** 2MB Flash
- **WiFi:** 2.4GHz 802.11n
- **GPIO:** 26 pins
- **I2C:** 2 controllers
- **Power:** 1.8-5.5V input
- **Cost:** ~$6

### MPU6050 IMU
- **Sensors:** 3-axis accelerometer + 3-axis gyroscope
- **Interface:** I2C
- **Voltage:** 3.3V or 5V
- **Sample rate:** Up to 8kHz
- **Current draw:** ~3.5mA
- **Cost:** ~$2

### VL53L1X Time-of-Flight Sensor
- **Range:** Up to 4 meters
- **Accuracy:** ±5cm typical
- **Interface:** I2C
- **Voltage:** 2.6-3.5V
- **Current draw:** ~20mA active
- **FOV:** 27°
- **Cost:** ~$15

---

## Pinout Assignments

### Pico W Connections

#### MPU6050 (I2C0)
```
MPU6050    Pico W
VCC    ->  3.3V (Pin 36)
GND    ->  GND  (Pin 38)
SCL    ->  GP5  (Pin 7)
SDA    ->  GP4  (Pin 6)
```

#### VL53L1X (I2C1)
```
VL53L1X    Pico W
VCC    ->  3.3V (Pin 36)
GND    ->  GND  (Pin 38)
SCL    ->  GP7  (Pin 10)
SDA    ->  GP6  (Pin 9)
```

#### Power
```
LiPo Battery -> VSYS (Pin 39)
GND          -> GND  (Pin 38)
```

---

## Power Budget

| Component    | Voltage | Current  | Notes              |
|--------------|---------|----------|--------------------|
| Pico W       | 3.3V    | ~150mA   | WiFi transmitting  |
| MPU6050      | 3.3V    | ~3.5mA   | Continuous read    |
| VL53L1X      | 3.3V    | ~20mA    | Active ranging     |
| **Total**    |         | **~175mA** |                  |

**Battery options:**
- 500mAh: ~2.8 hours runtime
- 1000mAh: ~5.7 hours runtime

**Target battery:** 1000mAh LiPo for good balance of size/runtime

---

## Wiring Diagrams

(To be added: photos and diagrams once hardware is assembled)

---

## Enclosure Design (Future)

**Requirements:**
- Spherical or near-spherical shape
- Clear window for ToF sensor
- IMU mounted near center of mass
- Impact protection (foam padding)
- Easy access for charging/programming
- Balanced weight distribution

**Material options:**
- PLA: Easy to print, rigid
- PETG: More durable, better impact resistance
- TPU: Flexible, excellent impact absorption (consider for outer shell)
