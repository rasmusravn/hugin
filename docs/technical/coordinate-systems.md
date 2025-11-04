# Coordinate Systems

## Overview

Handling 3D positioning requires consistent coordinate frames and transformations between sensor readings and world space.

---

## World Coordinate System

**Convention:** Right-handed coordinate system

```
     Z (up)
     |
     |
     |_______ Y
    /
   /
  X
```

- **X:** Forward/backward
- **Y:** Left/right
- **Z:** Up/down (gravity aligned)

**Reference:** Z-axis aligned with gravity (down = negative Z)

---

## IMU Coordinate System (MPU6050)

**Local sensor frame:**
```
Sensor orientation when mounted in ball:
- X: Forward (points in ToF measurement direction)
- Y: Left
- Z: Up (when ball is level)
```

**Readings:**
- **Accelerometer:** Linear acceleration in m/s² (SI units)
- **Gyroscope:** Angular velocity in rad/s (radians per second)

**Gravity reference:** When stationary, accelerometer reads ~9.8 m/s² pointing up (positive Z)

---

## ToF Sensor Coordinate System

**Measurement:** Distance along sensor's pointing direction

```
Sensor --> [distance] --> Surface
```

**To convert to 3D point:**
1. Get distance `d` from ToF
2. Get orientation (roll, pitch, yaw) from IMU
3. Calculate pointing direction vector
4. Position = sensor_position + d * direction_vector

---

## Coordinate Transformations

### Sensor Fusion Process

1. **Read IMU orientation**
   - Use accelerometer to determine gravity direction
   - Use gyroscope to track rotation
   - Apply complementary filter or Kalman filter

2. **Calculate sensor orientation matrix**
   - Roll, pitch, yaw → rotation matrix
   - Or use quaternions to avoid gimbal lock

3. **Transform ToF reading to world space**
   ```
   world_point = sensor_position + distance * rotation_matrix * [1, 0, 0]
   ```
   (Assuming ToF points along local X-axis)

4. **Update sensor position**
   - Integrate accelerometer readings (double integration)
   - Apply drift correction (future: SLAM)

---

## Decided Conventions

- ✅ **Accelerometer units:** m/s² (SI standard)
- ✅ **Gyroscope units:** rad/s (radians per second)
- ✅ **Angle representation:** Quaternions (avoid gimbal lock)
- ✅ **Distance units:** Centimeters (good room-scale precision)
- ✅ **IMU forward axis:** +X points in ToF direction

**See:** `docs/progress/decisions.md` for rationale

---

## Future: SLAM Coordinate Frame

When implementing SLAM:
- **Map frame:** Fixed world coordinates
- **Odom frame:** Dead reckoning from start position
- **Sensor frame:** Current sensor orientation/position

SLAM algorithm corrects drift between odom and map frames.

---

## References

- **Sensor orientation:** Document actual mounting orientation with photos
- **Rotation math:** Look into scipy.spatial.transform.Rotation for Python
- **Quaternions:** Consider using for gimbal-lock-free orientation tracking
