# Compliant Mechanisms for Impact Protection

## Overview

Hugin requires a suspension system to protect the Pico W, IMU, ToF sensor, and battery from impact forces during throwing and landing. Traditional rigid mounting would expose electronics to destructive shock loads. This document explores **compliant mechanisms** - flexible structures that absorb and dissipate impact energy through elastic deformation rather than rigid joints.

## Design Requirements

### Impact Scenarios
- **Throwing acceleration:** ~5-10 G during hand release
- **Flight:** Minimal forces (free fall or projectile motion)
- **Landing impact:** 20-50+ G depending on surface hardness and throw velocity
- **Tumbling:** Repeated lower-energy impacts as ball rolls/bounces

### Protection Goals
1. **Reduce peak acceleration** transmitted to electronics (target: <20 G at PCB)
2. **Prevent component detachment** from PCB or mounting points
3. **Avoid electrical disconnections** (solder joints, connectors, battery contacts)
4. **Maintain sensor alignment** (especially ToF optical path and IMU orientation)
5. **Minimize rebound** to reduce secondary impacts

### Constraints
- **Size:** Ball diameter ~8-12 cm (target TBD in Phase 4)
- **Weight:** Minimize added mass (affects throw distance and battery life)
- **Cost:** Stay within DIY budget (<$10 for suspension materials)
- **Manufacturing:** 3D printable or readily available materials
- **Assembly:** Easy to build without specialized tools

---

## Compliant Mechanism Concepts

### 1. TPU Lattice Suspension

**Concept:** 3D-printed TPU (thermoplastic polyurethane) cage with lattice structure surrounds electronics, allowing flexure during impact.

**Design Elements:**
- **Inner rigid platform:** PLA/PETG mount for Pico W, sensors, battery
- **Outer TPU lattice:** Flexible frame connecting inner platform to ball shell
- **Lattice geometry:** Honeycomb, gyroid, or spring-like struts
- **Stiffness tuning:** Adjust lattice density, strut thickness, infill pattern

**Advantages:**
- Single-print assembly (inner platform can be separate or embedded)
- Customizable stiffness through lattice design
- Energy absorption up to 20% better with optimized lattices
- Lightweight (TPU density: ~1.2 g/cm³)
- Can be tested and iterated quickly

**Challenges:**
- TPU printing requires careful calibration (slow speeds, direct drive extruder)
- Difficult to predict exact stiffness without testing
- May allow excessive motion if too flexible (sensor misalignment)
- Potential for plastic fatigue after many impacts

**Tuning Parameters:**
- Lattice unit cell size (2-10 mm)
- Strut thickness (0.8-2.5 mm)
- Infill percentage (10-40%)
- TPU Shore hardness (85A soft, 95A medium, 98A firm)

**References:**
- TPU shock absorption: kingroon.com/blogs/3d-print-101/how-to-design-perfect-3d-printable-springs
- Lattice optimization: 20% energy absorption improvement through structure tuning

---

### 2. Silicone Pad Stack

**Concept:** Electronics mounted between layers of silicone pads/sheets, creating a compliant sandwich.

**Design Elements:**
- **Central rigid PCB mount:** Holds Pico W and sensors
- **Silicone pads:** 5-10 mm thick, Shore 30A-60A (soft to medium)
- **Compression preload:** Pads slightly compressed in assembly to prevent rattling
- **Retention posts:** 3D-printed posts through silicone holes, secured with screws

**Advantages:**
- Simple to assemble (no complex 3D printing)
- Excellent vibration damping across wide frequency range
- Silicone widely available (craft stores, electronics suppliers)
- Easy to tune stiffness by changing pad thickness or durometer
- Predictable behavior (material properties well-documented)

**Challenges:**
- Requires cutting/sizing silicone sheets
- Potential for pads to shift during impact (need retention features)
- May be heavier than TPU lattice
- Difficult to create precise mounting holes

**Material Options:**
- **Silicone sheet stock:** Available in various thicknesses and durometers
- **Silicone casting:** Pour liquid silicone into 3D-printed molds (advanced)
- **Off-the-shelf pads:** Anti-vibration pads for appliances (cheap but less customizable)

**Tuning Parameters:**
- Pad thickness (thicker = softer, more travel)
- Shore hardness (lower = softer, more damping)
- Number of layers (more layers = more compliance)
- Preload compression (adjust retention post spacing)

---

### 3. Flexure Beam Suspension

**Concept:** Thin flexible beams (cantilevers or compliant hinges) connect electronics platform to ball shell, allowing controlled deflection.

**Design Elements:**
- **Cantilever springs:** 3-6 beams radiating from center platform to shell
- **Beam geometry:** Tapered width for constant stress distribution
- **Material:** Flexible filament (TPU, PETG, or thin ABS/PLA at limit)
- **Integrated design:** Single-piece print or snap-together assembly

**Advantages:**
- Precise stiffness control through beam dimensions (FEA calculable)
- Low part count (can be single print)
- No assembly required if printed as one piece
- Predictable deflection paths (beams bend in designed directions)

**Challenges:**
- Risk of fatigue failure at beam roots (stress concentration)
- Requires careful FEA or testing to avoid over/under-designing
- Large deflections may cause beams to interfere with each other
- Difficult to achieve isotropic suspension (equal stiffness all directions)

**Design Equations (Cantilever Beam):**
```
Deflection: δ = (F * L³) / (3 * E * I)
Spring constant: k = (3 * E * I) / L³

Where:
F = applied force
L = beam length
E = material Young's modulus (TPU: ~26 MPa, PLA: ~3500 MPa)
I = second moment of area (for rectangular: b*h³/12)
b = beam width, h = beam thickness
```

**Tuning Parameters:**
- Beam length (longer = softer)
- Beam width and thickness (thinner = softer)
- Number of beams (more beams = stiffer overall)
- Material choice (TPU vs. PETG vs. PLA)

---

### 4. Nested Spherical Shells

**Concept:** Electronics mounted in inner sphere, suspended inside outer sphere by flexible connectors, similar to gimbal but compliant.

**Design Elements:**
- **Inner sphere:** Rigid shell containing all electronics
- **Outer sphere:** Main ball shell (contact surface)
- **Flexible connectors:** 6-8 TPU ligaments or membrane bridges
- **Multi-axis compliance:** Absorbs impacts from any direction

**Advantages:**
- Isotropic protection (equal in all directions)
- Large energy absorption capacity (inner sphere can move significantly)
- Self-centering behavior (ligaments pull inner sphere back to neutral)
- Aesthetically elegant

**Challenges:**
- Complex 3D printing (two spheres, precise alignment)
- Difficult to access electronics after assembly
- Higher part count and assembly time
- May require support material removal from both spheres
- Risk of inner sphere contacting outer sphere during large impacts

**Design Considerations:**
- Gap between spheres: 5-15 mm (enough travel without bottoming out)
- Ligament thickness: 1-3 mm (thin enough to flex, thick enough to not tear)
- Ligament count: 6-12 (more = stiffer, fewer = more compliant)
- Material combination: Outer shell in PLA/PETG, ligaments in TPU

---

### 5. Memory Foam Core

**Concept:** Electronics embedded in memory foam block inside rigid ball shell.

**Design Elements:**
- **Memory foam block:** 30-50 mm thick, surrounds electronics on all sides
- **Rigid shell:** PLA/PETG outer sphere
- **Component pockets:** Cut cavities in foam for precise component placement
- **Fabric wrap:** Optional cloth covering to contain foam crumbs

**Advantages:**
- Excellent shock absorption (memory foam recovers slowly, reducing rebound)
- Extremely simple assembly (cut foam, insert electronics)
- Cheap and readily available (craft stores, old pillows)
- Multi-directional protection without complex design

**Challenges:**
- Difficult to achieve precise component positioning
- Foam degradation over time (compression set)
- May retain heat (foam insulates electronics)
- Hard to waterproof or seal against dust
- Aesthetic concerns (less "engineered" appearance)

**Material Sources:**
- Memory foam mattress toppers (cut to size)
- Foam packaging inserts
- Polyurethane foam sheets (various densities)

**Tuning Parameters:**
- Foam density (lower = softer, more compression)
- Foam thickness (thicker = more energy absorption)
- Firmness rating (ILD: Indentation Load Deflection)

---

## Hybrid Approaches

### Recommended: TPU Lattice + Silicone Pads

Combine the best of both worlds:
1. **Primary suspension:** TPU lattice cage (3D printed) for structural support and large deflections
2. **Secondary damping:** Thin silicone pads (2-3 mm) between electronics and lattice platform
3. **Benefits:**
   - Lattice handles large impact forces, preventing bottoming out
   - Silicone pads damp high-frequency vibrations and reduce rebound
   - Two-stage compliance reduces peak acceleration more effectively
   - Easy to tune by swapping silicone pads without reprinting

### Alternative: Flexure Beams + Memory Foam

For minimal printing and cost:
1. **Primary suspension:** 4-6 PETG flexure beams (thin, long cantilevers)
2. **Secondary damping:** Memory foam packed around electronics
3. **Benefits:**
   - Beams provide controlled stiffness and predictable deflection
   - Foam fills gaps, prevents rattling, and adds multi-axis damping
   - Very low cost (foam is nearly free)

---

## Design Process

### Phase 4 Development Workflow

1. **Prototype Testing (Week 1-2)**
   - 3D print simple test fixtures for each concept
   - Drop test from 1 m onto hard surface (wood/concrete)
   - Measure peak acceleration with IMU (analyze recorded data)
   - Compare: rigid mount baseline vs. compliant designs

2. **Iteration (Week 3-4)**
   - Identify best-performing concept from tests
   - Tune parameters (lattice density, foam thickness, beam dimensions)
   - Refine fit with actual components (Pico W, battery, sensors)

3. **Integration (Week 5-6)**
   - Design final ball enclosure around chosen suspension
   - Ensure ToF sensor optical path is clear
   - Verify battery and Pico W don't shift excessively
   - Test full assembly with actual throws

4. **Documentation (Week 7)**
   - Document chosen design with STL files, material specs, assembly instructions
   - Provide tuning guidance for different throw intensities
   - Include FEA analysis or measured stiffness curves

---

## Measurement and Testing

### Key Metrics

1. **Peak Acceleration Reduction**
   - Measure: Record IMU data during drop tests
   - Baseline: Rigid mount (no suspension)
   - Target: >50% reduction in peak G-force

2. **Displacement Travel**
   - Measure: High-speed video (smartphone slow-mo)
   - Ensure: Inner platform doesn't contact outer shell (no bottoming out)
   - Target: 5-10 mm maximum deflection before contact

3. **Rebound Behavior**
   - Measure: Count bounces after first impact
   - Desired: Fewer bounces = better energy dissipation
   - Target: <3 bounces from 1 m drop

4. **Resonant Frequency**
   - Measure: Tap test with IMU FFT analysis
   - Desired: Natural frequency <50 Hz (below sensor sampling rate)
   - Target: 10-30 Hz (human-throwable objects typically in this range)

### Test Setup

**Drop Test Rig:**
```
1. Suspend ball from electromagnet or quick-release clip
2. Drop from measured height (0.5 m, 1.0 m, 1.5 m)
3. Land on test surface (wood, concrete, carpet)
4. Record IMU data at maximum sample rate
5. Analyze peak acceleration, duration, frequency content
6. Video record with smartphone (240 fps slow-mo) to observe deflection
```

**Data Analysis:**
```python
import numpy as np
import matplotlib.pyplot as plt

# Load IMU data (timestamp, accel_x, accel_y, accel_z)
data = np.loadtxt('drop_test.csv', delimiter=',')
t = data[:, 0]
accel_magnitude = np.sqrt(data[:, 1]**2 + data[:, 2]**2 + data[:, 3]**2)

# Find peak acceleration
peak_g = np.max(accel_magnitude) / 9.81  # Convert m/s² to G

# Plot impact event
plt.plot(t, accel_magnitude / 9.81)
plt.xlabel('Time (s)')
plt.ylabel('Acceleration (G)')
plt.title(f'Drop Test - Peak: {peak_g:.1f} G')
plt.show()
```

---

## Safety Considerations

### Component Damage Thresholds

- **PCB solder joints:** Typically survive 50-100 G, but fatigue occurs with repeated shocks
- **Lithium battery:** Should not exceed 40 G to avoid internal damage (dendrite formation)
- **MEMS sensors (MPU6050, VL53L1X):** Designed for 10,000 G shock survival, but accuracy degrades above 100 G
- **Connectors and wires:** Weakest link - can disconnect at 20-30 G if not strain-relieved

**Recommendation:** Design for <20 G peak acceleration at PCB to ensure long-term reliability.

### Watch Movement Inspiration

Luxury mechanical watches use compliant shock protection systems (e.g., Incabloc, Kif) to protect tiny jewel bearings during impacts. These systems:
- Use spring-loaded conical jewels that deflect and self-center
- Absorb shocks by allowing controlled movement of delicate parts
- Have been refined over 100+ years for reliability

**Hugin parallel:** Similar philosophy - allow electronics to "float" within protective cage, limit travel with soft stops, and self-center after impact.

Reference: Built to Endure: Anti-Shock Systems in Luxury Watches (reservoir-watch.com)

---

## Research References

### Academic Sources

1. **Compliant Mechanisms for MEMS Protection**
   - Self-adaptive nonlinear stops (SANS) reduced impact force by 89.4% and dissipated 22.7% of mechanical energy
   - Source: ResearchGate - "Shock-Protection Improvement Using Integrated Novel Shock-Protection Technologies"

2. **3D Printed TPU for Impact Absorption**
   - Optimized lattice structures enhanced energy absorption by up to 20%
   - TPU Shore hardness 85A-98A commonly used for shock absorption
   - Source: Kingroon, Make3D, UltiMaker TPU application guides

3. **Vibration Damping in PCB Assemblies**
   - Particle Impact Dampers (NASA): Tungsten balls in sealed housing dissipate vibratory energy
   - Fabric tape with dry friction damper: Most effective protection method
   - Extension housing with damping materials: 60% vibration reduction achieved
   - Source: MATEC Conferences - "Methods for Vibration Reduction in Enclosed Electronic Packages"

4. **Flexible PCB with Vibration Damping**
   - 14-layer flex PCB with integrated damping materials protects against mechanical shock
   - Choice of damping material crucial for energy absorption/dissipation
   - Source: Capel Flexible Circuits

### Design Tools

- **FEA Software:** Fusion 360 (free for hobbyists), SolidWorks Simulation, Ansys
- **Lattice Generators:** nTopology, Fusion 360 lattice tools, Grasshopper for Rhino
- **Spring Calculators:** engineersedge.com, efunda.com

---

## Next Steps for Implementation

### Immediate (Phase 4 - Enclosure Design)

1. Choose initial concept: **Recommend TPU lattice + silicone pads hybrid**
2. CAD design basic lattice structure (start with honeycomb pattern)
3. 3D print test samples with varying lattice densities
4. Conduct drop tests with IMU data logging
5. Iterate based on measured performance

### Future Enhancements (Post-Phase 5)

1. **Advanced lattice optimization:** Use topology optimization software (nTopology)
2. **Custom silicone molding:** Design 3D-printed molds for precise silicone geometry
3. **Flex PCB integration:** Combine compliant mechanism with flexible circuit traces (eliminates fragile wires)
4. **Multi-material printing:** Print rigid and flexible parts in single run (Prusa MMU, Bambu AMS with TPU)

---

## Community Contributions

When releasing Hugin as open hardware:
- Encourage builders to experiment with different suspension designs
- Document suspension performance in build logs (peak G measurements)
- Share STL files for suspension variants (soft, medium, stiff options)
- Create tuning guide for different use cases (gentle indoor throws vs. aggressive outdoor)

---

**Document Status:** Planning / Research Phase
**Last Updated:** 2025-11-08
**Next Review:** During Phase 4 (Enclosure Design)
