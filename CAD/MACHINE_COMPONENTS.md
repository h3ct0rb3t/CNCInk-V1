# CNCInk V1 Machine Components

This document describes the main subsystems of the CNCInk V1 printing machine. Each section includes a Bill of Materials (BOM) and a detailed explanation of the subsystem's function and design considerations.

<img width="782" height="788" alt="image" src="https://github.com/user-attachments/assets/403080dd-4cc4-45d7-b683-0158d8c6451f" />


---

## 1. XYZ Motion System

<img width="666" height="677" alt="image" src="https://github.com/user-attachments/assets/f19f9036-b1f3-40af-b4be-7ca718bd03e4" />

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

The XYZ motion system provides three-axis positioning for precise placement of the print substrate relative to the printhead. This subsystem enables the machine to scan the printhead across the X and Y axes while the Z axis controls the gap between the substrate and printhead, a crucial parameter that will be explored in the next section.

The system uses stepper motors with microstepping capability to achieve high positional accuracy, leveraging the ball-and-screw configuration. The Z-axis is particularly important as it maintains consistent standoff distance, preventing nozzle strikes while ensuring adequate ink droplet velocity and placement accuracy. The linear rails provide smooth, repeatable motion with minimal backlash, which is essential for registration accuracy across multiple print passes.

Homing is performed using limit switches at the negative (home) position on each axis. The control firmware stores these positions as reference points and calculates all subsequent moves relative to this zero position.

---

## 2. Printhead Carriage Assembly

<img width="611" height="571" alt="image" src="https://github.com/user-attachments/assets/740e0c14-3874-423f-b74c-df2ed9308329" />

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

The printhead carriage holds the Xaar 128 at the required angle (~79° according to the datasheet) for optimal printing, routes the tubing that transports the ink, and holds a custom piezoelectric sensor that always maintains the required gap between printhead and substrate (1mm per the datasheet). 

The Xaar 128 is a high-resolution 128-nozzle printer with nozzles spaced at 84 micrometers, allowing for high-density printing patterns. The carriage design isolates vibration from the motion system to prevent vibration-induced droplet placement errors. A damping accumulator smooths pressure pulses in the ink supply, while the pressure relief valve provides redundant overpressure protection to safeguard the printhead from pressure spikes.

The custom piezoelectric sensor consists of a piezoelectric disc, a shouldered rod, and a casing. The rod's shoulder rests on the casing, so that a part of it sits outside of the casing and can be pushed inwards a distance of exactly 1mm, at which point the piezoelectric disk is flexed, its signal amplified, and the Z-axis stopped. This sensor is cheaper than off-the-shelf alternatives, and can be easily removed from the collision path and stored on the printhead carriage.  

---

## 3. 3PK Heated Bed

<img width="847" height="661" alt="image" src="https://github.com/user-attachments/assets/ca3195e0-c04d-40d9-80d6-8693fb0fda4d" />


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

The 3-Point Kinematic heated bed, or 3PK heated bed, is a custom aluminum printing surface that follows a 3-point kinematic design in order to ensure smooth printing. Because the bed moves perpendicular to the Z-axis, proper construction and installation of the bed ensures its position never drifts overtime. Further, the marbles and springs ensure that thermal expansion and stress due to the heaters are spread evenly throughout the surface. For this reason, Z-axis callibration should happen after heating the bed at the target temperature.

The heating itself is accomplished with a 25x25cm, 110V, 450W flexible heating pad. It is backed with a silicone sheet that functions as a thermal insulator, capable of withstanding repeated cycling at high temperatures while being cheap and easily accesible. The aluminum overside functions as the bed, and the underside functions as the support and coupler to the axis.

---

## 4. Peltier-Cooled Ink Reservoir

<img width="462" height="662" alt="image" src="https://github.com/user-attachments/assets/4a764145-c166-4c8a-a009-c3c61e6f9d73" />


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

The Peltier-cooled ink reservoir maintains ink at a precisely controlled low temperature (typically 15-20°C) to preserve ink chemistry, prevent evaporation, and stabilize viscosity. This is particularly important for long print sessions where ambient temperature fluctuations could otherwise cause drift in drop formation characteristics. Ink itself is stored in a Falcon tube, which itself is held in a custom aluminum casing with a slit, so ink levels can be monitored, and a bore, for the temperature sensor. The Peltier module is backed by a heat sink and a fan, which help the precise regulation of ink temperature. 

Because conductive inks can be very expensive and sensitive to temperature changes, a dedicated PID controller is allocated just for this module, which can be directly controlled by the user and is isolated from the microcontroller. The temperature sensor itself is a PT100 RTD probe, which is both cheap to acquire and extremely precise.

Average laboratory conditions (25°C, 50% RH) give a dew point of ~13°C. While conductive inks are usually meant to be stored at temperatures much lower than this point (typically ~5°C), they usually have to be printed closer to room temperature. Therefore, condensation on the Peltier module should not be an issue in most applications, but the researcher is encouraged to keep this in mind for their own setup, as there's no filtration within the machine for condensation. 

---

## 5. UV Curing Chamber

<img width="927" height="712" alt="image" src="https://github.com/user-attachments/assets/a66976c9-33ab-4354-a1ea-acf72da07d54" />


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

The UV curing chamber enables post-print curing of UV-curable inks, which are essential for achieving fast ink cross-linking and high color saturation on many substrates. The chamber uses a 395nm UV-A lamp, bolted to a 


---

## 6. Enclosure and Supports

<img width="1143" height="772" alt="image" src="https://github.com/user-attachments/assets/f7e629ac-d2e4-4908-8b39-bb10883d477f" />

<img width="1127" height="612" alt="image" src="https://github.com/user-attachments/assets/5967380e-c0ce-4087-bf13-459e2a17900e" />


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

