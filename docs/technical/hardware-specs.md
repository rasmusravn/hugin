# Hardware Specifications

## Bill of Materials

### Owned Components
- ✅ Raspberry Pi Pico W
- ✅ Jetson Orin Nano
- ✅ Raspberry Pi 4 (backup)

### To Purchase (Phase 1)
- ☐ MPU6050 IMU (~$2)
- ☐ VL53L1X ToF Distance Sensor (~$15)
- ☐ LiPo battery 150-200mAh + charging circuit (~$10-20)
- ☐ Breadboard/jumper wires
- ☐ (Optional) I2C pull-up resistors 4.7kΩ if not included on breakout boards

### Future Additions (Phase 4+)
- Multiple ToF sensors (4-6 units)
- 3D printed enclosure with compliant suspension (see `docs/technical/compliant-mechanisms.md`)
- **Impact protection:** TPU lattice cage + silicone pad hybrid suspension (target: <20 G peak acceleration at PCB)
- **Custom PCB with flex print lines:** Integrated circuit board design with flexible printed circuit (FPC) traces for sensor connections, reducing wiring complexity and improving reliability during impacts

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

### I2C Pull-Up Resistors

**Note:** Most I2C sensor breakout boards include built-in pull-up resistors. However, if you experience communication issues, you may need to add external pull-ups.

**Why Pull-Ups Are Needed:**
I2C uses an open-drain bus architecture where devices can only pull the signal lines (SDA/SCL) low, never high. Pull-up resistors are required to pull the lines back to high voltage (3.3V) when no device is actively pulling low. Without pull-ups, the bus lines would float at an undefined voltage, causing unreliable communication.

**Technical Details:**
- **Typical value:** 4.7kΩ (range: 2.2kΩ - 10kΩ)
- **Connection:** One resistor from SDA to 3.3V, one from SCL to 3.3V
- **Multiple devices:** All devices share the same pull-up resistors (I2C is a bus)
- **Too many pull-ups:** Multiple breakout boards with built-in resistors in parallel can create too-strong pull-ups (effective resistance too low), potentially causing signal issues

**When to add external pull-ups:**
- Using bare sensor chips without breakout boards
- Very long I2C wires (>30cm)
- Multiple devices causing bus capacitance issues
- Communication errors or unreliable readings

**When NOT needed:**
- Using commercial breakout boards (GY-521 for MPU6050, Adafruit/SparkFun modules) - they include pull-ups
- Standard breadboard prototyping with short wires

---

## Power Budget

| Component    | Voltage | Current  | Notes              |
|--------------|---------|----------|--------------------|
| Pico W       | 3.3V    | ~150mA   | WiFi transmitting  |
| MPU6050      | 3.3V    | ~3.5mA   | Continuous read    |
| VL53L1X      | 3.3V    | ~20mA    | Active ranging     |
| **Total**    |         | **~175mA** |                  |

**Battery life target:** 30 minutes continuous operation

**Battery sizing:**
- Continuous draw: ~175mA average
- Theoretical 30min runtime: 87.5mAh minimum
- **Recommended capacity: 150-200mAh**
  - Provides safety margin for WiFi transmission spikes
  - Accounts for safe LiPo discharge limit (80% DoD)
  - Ensures reliable 30+ minute operation
- Larger batteries provide longer runtime but add weight and size

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
- **Impact protection:** See `docs/technical/compliant-mechanisms.md` for detailed suspension design
- Easy access for charging/programming
- Balanced weight distribution
- Accessible mounting points for optional sensors

**Material options:**
- **Outer shell:** PLA (easy to print, rigid) or PETG (more durable, better impact resistance)
- **Impact suspension:** TPU lattice structure + silicone pads (recommended hybrid approach)
- **Alternative:** TPU flexible outer shell (less precise control than internal suspension)

**Custom PCB Design (Advanced Future Improvement):**
- Integrated PCB with Pico W footprint and sensor mounting
- Flexible printed circuit (FPC/flex PCB) traces for sensor connections
- Benefits:
  - Eliminates loose wires that can break during impacts
  - Reduces weight and volume compared to breadboard/jumper wires
  - More reliable connections during high-G throws
  - Professional appearance
  - Easier assembly and replication
- Considerations:
  - Requires PCB design skills (KiCad, Eagle, Altium)
  - Higher upfront cost (PCB manufacturing)
  - Less flexible for prototyping and modifications
  - Best suited for Phase 4+ after design is stable
