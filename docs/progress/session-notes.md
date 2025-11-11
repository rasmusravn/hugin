# Session Notes

---

## 2025-11-08 - Compliant Mechanism Research

### What I Did
- Researched compliant mechanisms for impact protection of electronics in throwable applications
- Created comprehensive technical documentation: `docs/technical/compliant-mechanisms.md`
- Analyzed 5 main suspension concepts: TPU lattice, silicone pads, flexure beams, nested spherical shells, memory foam
- Documented hybrid approaches combining multiple concepts
- Updated hardware specs to reference compliant mechanism documentation

### Technical Details

#### Research Findings
**Academic Sources:**
- **MEMS shock protection:** Self-adaptive nonlinear stops reduced impact force by 89.4% and dissipated 22.7% of mechanical energy
- **TPU lattice optimization:** Optimized structures enhanced energy absorption by up to 20%
- **PCB vibration damping:** Extension housing with damping materials achieved 60% vibration reduction
- **Luxury watch anti-shock systems:** Incabloc/Kif mechanisms use compliant spring-loaded jewels (100+ years of refinement)

**Material Properties:**
- TPU (thermoplastic polyurethane): Shore hardness 85A-98A, density ~1.2 g/cm³, excellent shock absorption
- Silicone: Shore 30A-60A, wide frequency damping, readily available
- Memory foam: Slow recovery (reduces rebound), very cheap, good multi-axis protection

#### Five Main Concepts Evaluated

1. **TPU Lattice Suspension**
   - 3D-printed flexible cage with tunable lattice geometry (honeycomb, gyroid, spring struts)
   - Advantages: Single-print assembly, customizable stiffness, lightweight, rapid iteration
   - Challenges: TPU printing difficulty, stiffness prediction requires testing

2. **Silicone Pad Stack**
   - Electronics sandwiched between silicone layers with compression preload
   - Advantages: Simple assembly, excellent vibration damping, predictable behavior, readily available
   - Challenges: Cutting/sizing sheets, potential shifting, heavier than TPU

3. **Flexure Beam Suspension**
   - Cantilever beams connect electronics platform to shell, FEA-calculable stiffness
   - Advantages: Precise control, low part count, predictable deflection paths
   - Challenges: Fatigue risk at beam roots, difficult to achieve isotropic stiffness

4. **Nested Spherical Shells**
   - Inner sphere suspended inside outer sphere by flexible ligaments
   - Advantages: Isotropic protection, large energy absorption, self-centering, elegant
   - Challenges: Complex printing, difficult post-assembly access, higher part count

5. **Memory Foam Core**
   - Electronics embedded in memory foam block inside rigid shell
   - Advantages: Excellent shock absorption, extremely simple, cheap, multi-directional
   - Challenges: Difficult precise positioning, foam degradation, heat retention

#### Recommended Hybrid Approach
**TPU Lattice + Silicone Pads** (two-stage compliance):
- Primary: TPU lattice cage for structural support and large deflections
- Secondary: Thin silicone pads (2-3 mm) for high-frequency damping and rebound reduction
- Benefits: Lattice prevents bottoming out, silicone damps vibrations, easy tuning without reprinting

### Design Requirements Established
- **Target peak acceleration:** <20 G at PCB (protects solder joints and battery)
- **Component damage thresholds:** PCB 50-100 G, LiPo 40 G, MEMS 10,000 G, connectors 20-30 G
- **Measurement metrics:** Peak G reduction (>50% target), displacement travel (5-10 mm), rebound behavior (<3 bounces), resonant frequency (10-30 Hz)

### Test Methodology Defined
- Drop test rig with electromagnet release from 0.5 m, 1.0 m, 1.5 m heights
- IMU data logging at maximum sample rate during impact
- High-speed video (smartphone 240 fps) for deflection observation
- Python analysis script for peak G-force and FFT frequency content

### What Worked
- Web search yielded excellent academic and practical sources
- Found clear parallels between watch shock protection and Hugin requirements
- Identified actionable design parameters for Phase 4 implementation

### Decisions Made
- **Recommended primary concept:** TPU lattice + silicone pad hybrid
- **Design target:** <20 G peak acceleration at PCB
- **Testing approach:** Drop tests with IMU data analysis and high-speed video
- **Deferred to Phase 4:** Actual CAD design, prototyping, and testing

### Next Steps
- Document compliant mechanism research in Phase 4 task list
- When Phase 4 begins: CAD basic lattice structure, 3D print test samples, conduct drop tests
- Consider documenting alternative build options (simple vs. optimized suspension) for community

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

