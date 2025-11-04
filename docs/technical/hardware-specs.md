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

**Battery life target:** 30 minutes continuous operation

**Battery sizing:** At ~175mA continuous draw, a 100mAh battery would provide ~30 minutes runtime. Larger batteries provide longer runtime but add weight and size.

---

## Wiring Diagrams

(To be added: photos and diagrams once hardware is assembled)

---

## Optional Sensor Mounting

**Vacant Mounts for Expansion**

The Hugin ball design includes vacant mounting points for optional sensors, enabling customization and experimentation.

**Mounting Requirements:**
- Standardized mounting holes for common sensor breakout boards
- I2C bus access (shared with existing sensors)
- Clear line-of-sight for optical sensors
- Secure mounting to withstand impacts during flight
- Easy removal and replacement for different sensors

**Potential Optional Sensors:**
- Additional ToF sensors (VL53L1X) for multi-directional ranging
- Color sensors for texture/material detection
- Light sensors for brightness mapping
- Temperature/humidity sensors for environmental data
- Magnetometer for compass heading
- Barometric pressure sensor for altitude
- Camera modules (future - requires different MCU)

**Design Philosophy:**
The vacant mounts support the "Use what you have" philosophy - builders can experiment with sensors they already own or add capabilities specific to their use case.

**Integration Notes:**
- Software must be modified to read additional sensors
- Power budget must be recalculated with additional sensors
- I2C address conflicts must be avoided (check sensor datasheets)
- Data streaming format may need extension for new sensor types

---

## Enclosure Design (Future)

**Requirements:**
- Spherical or near-spherical shape
- Clear window for ToF sensor(s)
- IMU mounted near center of mass
- Impact protection (foam padding)
- Easy access for charging/programming
- Balanced weight distribution
- Accessible mounting points for optional sensors

**Material options:**
- PLA: Easy to print, rigid
- PETG: More durable, better impact resistance
- TPU: Flexible, excellent impact absorption (consider for outer shell)
