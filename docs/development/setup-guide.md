# Development Environment Setup

## Pico W Setup

### 1. Install Dependencies (Ubuntu)

```bash
sudo apt update
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi \
  build-essential python3 python3-pip
```

### 2. Install Thonny IDE (Easiest option)

```bash
sudo apt install thonny
```

**Alternative:** Use VS Code with Pico-W-Go extension

### 3. Download MicroPython Firmware

1. Visit: https://micropython.org/download/RPI_PICO_W/
2. Download latest `.uf2` file for Pico W

### 4. Flash MicroPython to Pico W

1. Hold BOOTSEL button on Pico W
2. Plug into USB while holding button
3. Pico W appears as USB drive "RPI-RP2"
4. Drag and drop `.uf2` file to the drive
5. Pico W automatically reboots with MicroPython installed

### 5. Test Connection

Open Thonny:
1. Select "MicroPython (Raspberry Pi Pico)" from interpreter dropdown
2. Click "Stop/Restart backend" to connect
3. You should see MicroPython REPL prompt

**Test blink:**
```python
from machine import Pin
import time

led = Pin("LED", Pin.OUT)
for i in range(5):
    led.toggle()
    time.sleep(0.5)
```

---

## Jetson Orin Nano Setup

### 1. Install Python Dependencies

```bash
sudo apt update
sudo apt install python3-pip
pip3 install numpy matplotlib
```

### 2. (Future) Install 3D Visualization Libraries

```bash
pip3 install open3d
```

### 3. Network Configuration

Find Jetson IP address:
```bash
hostname -I
```

Update this IP in Pico W WiFi sender code.

---

## Project Structure

```
hugin/
├── pico/               # Pico W firmware
│   ├── main.py
│   ├── wifi_sender.py
│   └── sensors.py
├── jetson/             # Jetson software
│   ├── receiver.py
│   ├── visualizer.py
│   └── processor.py
├── docs/               # Documentation
└── tests/              # Test scripts
```

---

## Troubleshooting

### Pico W not detected
- Try different USB cable (some are charge-only)
- Hold BOOTSEL longer (5+ seconds)
- Check USB port works with other devices

### Cannot connect to Pico in Thonny
- Unplug and replug Pico W
- Click "Stop/Restart backend" in Thonny
- Try different USB port

### WiFi connection fails
- Verify SSID and password are correct
- Check 2.4GHz WiFi (Pico W doesn't support 5GHz)
- Ensure network allows new device connections

---

## Next Steps

After setup complete:
1. Test WiFi connection on Pico W
2. Create simple UDP sender
3. Create receiver on Jetson
4. Verify data streaming works
