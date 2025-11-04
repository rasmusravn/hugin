# Communication Protocols

## WiFi Connection

**Network:** Home WiFi (2.4GHz)
**Protocol:** UDP
**Port:** 5000 (configurable)

### Connection Flow
1. Pico W powers on
2. Connects to configured SSID
3. Obtains IP via DHCP
4. Begins sending UDP packets to Jetson IP:PORT

---

## Data Packet Format

### JSON Format (Current)

```json
{
  "timestamp": 123456789,
  "accel": [ax, ay, az],
  "gyro": [gx, gy, gz],
  "distance": 150.5
}
```

**Field descriptions:**
- `timestamp`: Milliseconds since boot (from `time.ticks_ms()`)
- `accel`: [x, y, z] acceleration in m/s² (SI units)
- `gyro`: [x, y, z] rotation rate in rad/s (radians per second)
- `distance`: Distance reading in centimeters

**Packet size:** ~100-150 bytes

**Sample rate:** 50 Hz fixed (20ms between packets)

### Binary Format (Future Optimization - Phase 4)

To reduce bandwidth and processing:
```
struct SensorPacket {
  uint32_t timestamp;    // 4 bytes
  int16_t accel[3];      // 6 bytes (scale: /1000 for m/s²)
  int16_t gyro[3];       // 6 bytes (scale: /1000 for rad/s)
  uint16_t distance;     // 2 bytes (centimeters)
}                        // Total: 18 bytes
```

**Benefits:** ~6-8x smaller packets, faster parsing
**Note:** Deferred to Phase 4 - JSON is sufficient for development phases

---

## Error Handling

### Packet Loss
- UDP doesn't guarantee delivery
- Acceptable for real-time visualization
- Jetson should handle missing packets gracefully

### Connection Loss
- Pico W should attempt reconnection
- Buffer recent data if possible
- LED indicator for connection status

### Malformed Packets
- Jetson validates JSON/binary format
- Skip invalid packets, log error
- Continue processing next packet

---

## Configuration

### Pico W Settings
```python
SSID = "your_network_name"
PASSWORD = "your_password"
JETSON_IP = "192.168.1.xxx"
JETSON_PORT = 5000
SAMPLE_RATE_HZ = 50
```

### Jetson Settings
```python
LISTEN_PORT = 5000
BUFFER_SIZE = 1024
TIMEOUT_SECONDS = 5  # For connection loss detection
```

---

## Future Enhancements

- **Packet acknowledgment:** Optional TCP mode for critical data
- **Compression:** gzip for JSON or custom binary encoding
- **Multi-sensor support:** Array of sensor readings in single packet
- **Calibration data:** Separate channel for sending calibration parameters
- **Command channel:** Jetson → Pico W for control (start/stop, adjust sample rate)
