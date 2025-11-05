# Session Notes

---

## 2025-11-05 - Hardware Ordering

### What I Did
- Ordered all Phase 1 hardware components from ardustore.dk:
  - Raspberry Pi Pico W (Pico 2 W not available)
  - MPU6050 IMU development board
  - VL53L1X ToF sensor development board
  - LiPo battery (150-200mAh range) + charging circuit

### Technical Details
#### Hardware Components
- All components ordered from ardustore.dk (Danish electronics webshop)
- Chose Pico W instead of Pico 2 W (availability constraint)
- Chose development boards (breakout boards) for initial prototype
- Development boards include I2C pull-up resistors and voltage regulators (easier to wire)

### What Worked
- Successfully found all required Phase 1 components at single webshop
- Pico W is sufficient for Phase 1 WiFi streaming proof of concept

### Issues Encountered
- Pico 2 W not available at ardustore.dk
- Solution: Ordered Pico W instead (original Pico W is fine for this project)

### Decisions Made
- **Using Pico W instead of Pico 2 W:** Availability constraint, but functionally equivalent for this project
- **Cost optimization deferred to future phase:** Development boards are more expensive than bare sensor chips but much easier to prototype with
- Documented future cost optimization opportunity in backlog
  - Current: Development boards (~$2-20 per sensor)
  - Future option: Bare chips with custom PCB (50-70% cost reduction)
  - Will offer both "Easy Build" and "Budget Build" options in final documentation

### Next Steps
- Wait for component delivery
- Once received: Set up Pico W development environment (Thonny or VS Code)
- Flash MicroPython firmware to Pico W
- Begin "Hul igennem"-test (proof of concept WiFi streaming)

---
## 2025-11-05 - Phase 0 Review and Completion

### What I Did
- Completed comprehensive Phase 0 review of all deliverables
- Enhanced hardware specifications with battery sizing rationale
- Added detailed I2C pull-up resistor documentation with technical explanation
- Implemented WiFi credential security with config.py template system
- Consolidated .gitignore patterns for clearer project standards
- Verified all Phase 0 success criteria are met

### Technical Additions

#### Battery Sizing
- Updated power budget with recommended 150-200mAh capacity
- Added safety margin calculations for WiFi spikes and LiPo discharge limits
- Ensures reliable 30+ minute operation

#### I2C Pull-Up Resistors
Added technical documentation explaining:
- **Why needed:** I2C open-drain architecture requires pull-ups to restore high voltage
- **Typical values:** 4.7kΩ (range 2.2kΩ - 10kΩ)
- **When to add:** Bare chips, long wires, multiple devices causing capacitance issues
- **When not needed:** Commercial breakout boards (already include pull-ups)
- **Risk of too many:** Multiple boards in parallel can create overly strong pull-ups

#### WiFi Security
- Created `pico/config.py.template` and `jetson/config.py.template`
- Consolidated .gitignore to use single `config.py` convention
- Updated setup-guide.md with configuration instructions
- Prevents accidental credential commits

### What Worked
- Phase 0 documentation is comprehensive and ready for implementation
- All technical decisions documented with clear rationale
- Hardware component selections validated against requirements
- No blocking gaps identified for Phase 1

### Issues Encountered
- None - Phase 0 review found no critical issues
- Minor observations (battery sizing, I2C pull-ups, WiFi security) addressed proactively

### Phase 0 Success Criteria - All Met ✅
- ✅ Project concept clearly defined
- ✅ Hardware components selected with rationale
- ✅ System architecture documented
- ✅ All critical technical decisions made and documented
- ✅ GitHub repository set up with license (Apache 2.0)
- ✅ Comprehensive documentation created
- ✅ Ready to begin hardware implementation

### Next Steps
- Mark Phase 0 as complete in todo.md
- Begin Phase 1: WiFi Streaming Foundation
- Set up Pico W development environment
- Order hardware components (MPU6050, VL53L1X, 150-200mAh LiPo battery)

---

## 2025-11-03 - Project Setup

### What I Did
- Created initial project documentation structure
- Set up docs folders (progress, technical, development)

### What Worked
- Documentation structure is clean and organized

### Issues Encountered
- None yet

### Next Steps
- Start Phase 1: WiFi streaming basics
- Set up Pico W development environment

---

## Session Note Template

Copy this template to start a new session:

```markdown
---

## YYYY-MM-DD - Brief Session Title

### What I Did
-
-
-

### Technical Details
#### Subsystem/Feature Name (if applicable)
-
-

### What Worked
-
-

### Issues Encountered
-
-

### Decisions Made
-
-

### Next Steps
-
-

---
```

