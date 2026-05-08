# CNCInk V1 Machine Components

This document describes the main subsystems of the CNCInk V1 printing machine. Each section includes a Bill of Materials (BOM) and a detailed explanation of the subsystem's function and design considerations.

---

## 1. XYZ Motion System

### Bill of Materials

| Item Name | Quantity | Sourcing Link | Notes |
|-----------|----------|---------------|-------|
| NEMA 23 Stepper Motor | 3 | [Automation Direct](https://www.automationdirect.com) | One each for X, Y, Z axes |
| Linear Rail 20mm (1m length) | 6 | [Misumi](https://us.misumi-ec.com) | Rails for X, Y, Z motion (2 per axis) |
| Ball Screw 16mm dia. (500mm) | 3 | [Misumi](https://us.misumi-ec.com) | Drive screws for X, Y, Z |
| Flexible Coupling 8mm | 3 | [McMaster-Carr](https://www.mcmaster.com) | Motor-to-screw coupling |
| Linear Bearing Blocks | 12 | [Misumi](https://us.misumi-ec.com) | Support blocks for rails (4 per axis) |
| Stepper Driver Module (3A) | 3 | [Pololu](https://www.pololu.com) | DRV8825 or equivalent |
| End Stop Switches | 6 | [Amazon](https://www.amazon.com) | Limit switches for min/max travel per axis |

### Functional Overview

The XYZ motion system provides three-axis positioning for precise placement of the print substrate relative to the printhead. This subsystem enables the machine to scan the printhead across the X and Y axes while the Z axis controls the gap between the substrate and printhead—a critical parameter for inkjet printing quality and nozzle-substrate interaction.

The system uses stepper motors with microstepping capability to achieve high positional accuracy (typically 0.01-0.05mm per step depending on mechanical reduction). The Z-axis is particularly important as it maintains consistent standoff distance, preventing nozzle strikes while ensuring adequate ink droplet velocity and placement accuracy. The linear rails provide smooth, repeatable motion with minimal backlash, which is essential for registration accuracy across multiple print passes.

Homing is performed using limit switches at the negative (home) position on each axis. The control firmware stores these positions as reference points and calculates all subsequent moves relative to this zero position.

---

## 2. Printhead Carriage Assembly

### Bill of Materials

| Item Name | Quantity | Sourcing Link | Notes |
|-----------|----------|---------------|-------|
| Xaar 128 Printhead | 1 | [Xaar](https://www.xaar.com) | 128 nozzles @ 84 µm pitch, 10 pL drops |
| Carriage Bracket (Aluminum) | 1 | Custom fabrication | Mounts printhead to Z-carriage |
| High-Voltage Connector | 1 | [TE Connectivity](https://www.te.com) | 40-pin connector for printhead signals |
| Ink Supply Tubing (Tygon) | 2 | [Cole-Parmer](https://www.coleparmer.com) | 1.6mm ID for ink inlet and return |
| Pressure Relief Valve | 1 | [Gem](https://www.gemsen.com) | Redundant overpressure protection |
| Damping Accumulator (10mL) | 1 | [Gem](https://www.gemsen.com) | Isolates printhead from system pressure ripple |
| Thermal Sensor (PT100) | 1 | [Omega Engineering](https://www.omega.com) | Temperature monitoring for printhead |

### Functional Overview

The printhead carriage is the primary positioning stage that holds the Xaar 128 inkjet printhead and moves it across the XY plane. The carriage mounts to the Z-axis for vertical positioning control. Precise alignment of the printhead is critical for achieving uniform dot placement and preventing nozzle damage.

The Xaar 128 is a high-resolution 128-nozzle printer with nozzles spaced at 84 micrometers, allowing for high-density printing patterns. The carriage design isolates vibration from the motion system to prevent vibration-induced droplet placement errors. A damping accumulator smooths pressure pulses in the ink supply, while the pressure relief valve provides redundant overpressure protection to safeguard the printhead from pressure spikes.

The carriage must be carefully balanced and aligned to the XYZ axes to ensure perpendicular print surfaces and consistent ink delivery across all nozzles. The thermal sensor allows real-time temperature monitoring, as printhead viscosity is temperature-dependent and affects drop formation.

---

## 3. 3PK Heated Bed

### Bill of Materials

| Item Name | Quantity | Sourcing Link | Notes |
|-----------|----------|---------------|-------|
| Aluminum Heating Plate (300x300mm) | 1 | Custom fabrication | 6061-T6 aluminum with embedded cartridge heaters |
| Cartridge Heater (500W, 12mm dia) | 3 | [Omega Engineering](https://www.omega.com) | Three heating elements for uniform temperature |
| Thermistor or RTD Sensor | 2 | [Omega Engineering](https://www.omega.com) | Temperature feedback for control loop |
| Insulation Layer (Cork/Ceramic) | 1 | [McMaster-Carr](https://www.mcmaster.com) | 50mm thick insulation layer |
| Heating Plate Mounting Hardware | 1 | [McMaster-Carr](https://www.mcmaster.com) | Thermally isolated mounts |
| PID Temperature Controller | 1 | [Omega Engineering](https://www.omega.com) | Digital temperature regulation |
| Substrate Clamp System | 4 | Custom fabrication | Pneumatic or magnetic clamps for substrate hold-down |

### Functional Overview

The 3PK heated bed maintains substrate temperature, which is critical for controlling ink viscosity, surface wetting characteristics, and curing behavior post-printing. The "3PK" designation refers to three cartridge heaters providing redundancy and uniform thermal distribution across the bed surface.

Temperature control is essential because most inks have viscosity specifications at a reference temperature (typically 25°C). By heating the substrate to an elevated temperature (typically 40-80°C depending on ink type), the system can optimize ink flow to nozzles, reduce nozzle clogging, and improve wetting on certain substrates. The thermal sensors provide feedback for a PID control loop that maintains setpoint temperature within ±2°C.

The insulation layer beneath the bed minimizes heat loss and improves energy efficiency. The heated bed also serves as the XY motion stage, with the printhead carriage positioned above it. Care must be taken to ensure thermal stability—excessive temperature gradients can cause non-uniform expansion of the substrate, leading to registration errors.

---

## 4. Peltier-Cooled Ink Reservoir

### Bill of Materials

| Item Name | Quantity | Sourcing Link | Notes |
|-----------|----------|---------------|-------|
| Ink Reservoir Tank (PTFE, 500mL) | 1 | [Cole-Parmer](https://www.coleparmer.com) | Chemical-resistant container for ink storage |
| Peltier Thermoelectric Module (TEC) | 2 | [Adafruit](https://www.adafruit.com) | TEC1-12706 or equivalent, 60W cooling capacity |
| Aluminum Cold Plate | 1 | Custom fabrication | Thermal interface for Peltier module |
| Heatsink and Fan Assembly | 1 | [Noctua](https://noctua.at) | Heat rejection from hot side of Peltier |
| Temperature Sensor (Thermistor) | 2 | [Omega Engineering](https://www.omega.com) | Monitor hot and cold side temperatures |
| Peltier Driver Circuit | 1 | [LM2596](https://www.ti.com) | PWM buck converter for power regulation |
| Ink Filter (10µm sintered bronze) | 1 | [Gem](https://www.gemsen.com) | Pre-chamber filtration for particle removal |
| Insulated Tubing (Foam wrap) | 1 | [McMaster-Carr](https://www.mcmaster.com) | Minimize heat leak during transport |

### Functional Overview

The Peltier-cooled ink reservoir maintains ink at a precisely controlled low temperature (typically 15-20°C) to preserve ink chemistry, prevent evaporation, and stabilize viscosity. This is particularly important for long print sessions where ambient temperature fluctuations could otherwise cause drift in drop formation characteristics.

The Peltier thermoelectric cooler (TEC) operates by pumping heat from the cold side (in contact with the reservoir) to the hot side (dissipated to ambient via a heatsink and fan). A dual-sensor temperature monitoring system allows for closed-loop control: one sensor monitors the ink temperature in the reservoir, while a second monitors the hot-side temperature to prevent thermal runaway or condensation on the cold side.

The redundant Peltier modules provide cooling capacity margin and allow graceful degradation—if one module fails, the system continues to function at reduced cooling capacity. The in-line filter removes particles that could clog printhead nozzles. Insulated tubing on supply lines minimizes parasitic heat transfer between the cool reservoir and the warm heated bed system.

---

## 5. UV Curing Chamber

### Bill of Materials

| Item Name | Quantity | Sourcing Link | Notes |
|-----------|----------|---------------|-------|
| UV LED Array (365nm, 100W) | 4 | [Thorlabs](https://www.thorlabs.com) | Positioned around chamber for uniform exposure |
| Aluminum Reflective Chamber | 1 | Custom fabrication | Anodized aluminum with high reflectivity |
| Safety Interlocks (Microswitch) | 2 | [Omron](https://www.omron.com) | Disable UV when door/cover is open |
| UV Light Control Board | 1 | [Arduino](https://www.arduino.cc) | PWM dimming and intensity control |
| Quartz Window | 1 | Custom order | UV-transparent optical access |
| Exhaust Fan (200CFM) | 1 | [Noctua](https://noctua.at) | Remove ozone and volatile organic compounds |
| Activated Carbon Filter | 1 | [Grainger](https://www.grainger.com) | Post-fan VOC scrubbing |
| Thermal Control Thermostat | 1 | [Omega Engineering](https://www.omega.com) | Chamber temperature regulation during curing |

### Functional Overview

The UV curing chamber enables post-print curing of UV-curable inks, which are essential for achieving fast ink cross-linking and high color saturation on many substrates. The chamber uses 365nm UV LEDs rather than mercury lamps, providing safer operation, lower power consumption, and longer service life.

The reflective aluminum chamber design ensures efficient use of UV photons by bouncing scattered light back onto the substrate. Uniform curing across the entire print area is achieved through strategic positioning of four UV LED arrays around the chamber. The safety interlocks prevent accidental UV exposure to operators—the LEDs automatically disable when the chamber door or access cover is opened.

Temperature control is important because UV curing is an exothermic chemical reaction; excessive heat buildup can cause substrate warping or ink over-cure (hardening so rapidly that the ink becomes brittle). The exhaust system removes ozone (a byproduct of UV-oxygen reactions) and volatile organic compounds that may be released during curing, maintaining a safe work environment.

Exposure time and UV intensity are controlled via PWM dimming, allowing recipes to be optimized for different ink types and substrate thicknesses.

---

## 6. Enclosure and Supports

### Bill of Materials

| Item Name | Quantity | Sourcing Link | Notes |
|-----------|----------|---------------|-------|
| Aluminum Frame Extrusion (40x40mm) | 20m | [80/20 Inc.](https://www.8020.net) | Structural frame for machine assembly |
| Polycarbonate Panels (10mm) | 8 sheets | [McMaster-Carr](https://www.mcmaster.com) | Transparent enclosure walls and access doors |
| Hinged Door Assembly | 2 | Custom fabrication | Access to printhead and substrate areas |
| Cable Trays and Conduit | 1 | [Grainger](https://www.grainger.com) | Route power and signal cables |
| Vibration Isolation Feet (Rubber) | 12 | [TRELLEBORG](https://www.trelleborg.com) | Decouple machine from external vibration |
| Emergency Stop Button | 1 | [Omron](https://www.omron.com) | Red mushroom button for safe shutdown |
| Power Distribution Panel | 1 | [Eaton](https://www.eaton.com) | Main breaker and outlet distribution |
| Fume Extraction Port (4" diameter) | 1 | Custom fabrication | Connection to external ventilation system |

### Functional Overview

The enclosure and support structure serves multiple critical functions: it provides mechanical rigidity to maintain XYZ alignment tolerances, isolates the precision printing environment from external vibration, protects operators from moving machinery and UV exposure, and organizes the complex electrical and fluid systems required for printing.

The aluminum extrusion frame provides an excellent balance of strength, stiffness, and modularity—components can be repositioned without structural modification. The polycarbonate panels are transparent, allowing observation of print operations while providing some acoustic damping. Hinged doors provide safe access to the printhead carriage for cleaning and maintenance without full disassembly.

Vibration isolation feet decouple the machine from floor vibration, which is critical for achieving high positional accuracy. Even small vibrations during the dwell time before ink firing can cause droplet placement errors. The emergency stop button provides a single-action failsafe for rapid shutdown in case of any anomaly.

Cable management is organized in trays to prevent interference with moving parts and to simplify troubleshooting. The fume extraction port connects to a house exhaust system, drawing vapors and ozone away from the operator during printing and curing operations. Proper ventilation is essential for operator safety and print quality (humidity control).

