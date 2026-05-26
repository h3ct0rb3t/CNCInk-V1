# Project Overview

<img width="1020" height="752" alt="image" src="https://github.com/user-attachments/assets/9f618cc1-ba6b-481c-a625-4cb8d3f88f25" />

The CNCInk is an open-source custom inkjet platform, designed for printing conductive inks on polymeric substrates to create integrated biological sensors. The current design includes a Peltier module-based cooling system for the conductive ink, a gantry system for positioning and printing, and both a heated bed and a UV curing chamber to cure the ink as necessary. The printhead itself is a Xaar XJ128, which is piezoelectric, and while it was selected for its accesibility and compatibility with conductive inks, any researcher can swap it for whichever is more appropriate for their application.

The controls are performed by an STM32F446RET for the precise printing and motion of the CNCInk, in conjunction with a Raspberry Pi 4 for HMI interaction and direct peripheric control of cooling fans. The Peltier module is connected to an independent PID controller, in order to ensure independence of STM32 operation. The HMI itself was designed using Python.

The following chapters explain broadly what each subsection contains.

## Folders

### CAD
Contains the explanation and BOM for each subsystem of the CNCInk, so any implementation and modification can be made with intention. The CAD files themselves are in a ZIP file under the "Releases" section, on the right hand side. They were designed using SolidWorks 2022, so any version can open them, and saved in their original format to preserve their properties.  

### Schematics
Includes the circuit schematics.

### Code
Houses the source code for the CNC Ink application.

### COMSOL
The COMSOL folder includes simulation files related to the project. These simulations provide insights into the physical processes modeled within the CNC Ink system.

---

**Note:** Make sure to update your local copy with the latest changes.
Progress video update: https://youtu.be/DczCuBlnv0s
