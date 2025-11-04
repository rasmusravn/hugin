# Testing Notes

## Test Results Log

### Template
```
## YYYY-MM-DD - Test Name

**Objective:** What you're testing

**Setup:**
- Hardware configuration
- Software version
- Environment conditions

**Procedure:**
1. Step 1
2. Step 2

**Results:**
- Expected: X
- Actual: Y

**Conclusion:** Pass/Fail, observations

**Data/Logs:**
```

---

## Calibration Data

### IMU Calibration

**Accelerometer offsets:**
```
X: [TBD]
Y: [TBD]
Z: [TBD]
```

**Gyroscope offsets:**
```
X: [TBD]
Y: [TBD]
Z: [TBD]
```

**Calibration procedure:**
1. Place sensor flat and stationary
2. Record 1000 samples
3. Calculate mean offset for each axis
4. Subtract offsets in code

---

### ToF Sensor Calibration

**Distance accuracy test:**

| Actual Distance | Measured Distance | Error |
|-----------------|-------------------|-------|
| 50 cm           | [TBD]            | [TBD] |
| 100 cm          | [TBD]            | [TBD] |
| 150 cm          | [TBD]            | [TBD] |
| 200 cm          | [TBD]            | [TBD] |

**Calibration notes:**
- Test against different surface types (white wall, dark wall, wood, etc.)
- Note any systematic bias
- Check performance at different angles

---

## Performance Benchmarks

### WiFi Streaming

**Packet delivery rate:**
- Expected: [TBD]
- Actual: [TBD]

**Latency:**
- Expected: <100ms
- Actual: [TBD]

**Packet loss:**
- Expected: <5%
- Actual: [TBD]

---

## Known Issues

(Link to issues.md for detailed problem tracking)

---

## Test Environments

**Indoor room 1:** Living room, ~4m x 5m
**Indoor room 2:** [TBD]

**Surface materials tested:**
- White drywall
- Wood floor
- [Add more as tested]
