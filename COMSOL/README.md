## Objective
The objective of this project is to...

## COMSOL Multiphysics Setup
### Parameters
| Name                    | Expression   | Value | Description                      | Source         |
|-------------------------|--------------|-------|----------------------------------|----------------|
| W_chamber               |   117 um     |       | Width of the chamber             |                |
| L_chamber               |   800 um     |       | Length of the chamber            |                |
| H_chamber               |   117 um     |       | Height of the chamber            |                |
| W_restrictor            |   40  um     |       | Width of the restrictor          |                |
| L_restrictor            |   400 um     |       | Length of the restrictor         |                |
| H_nozzle                |   67  um     |       | Height of the nozzle             |                |
| D_nozzle_b              |   83  um     |       | Bottom diameter of the nozzle    |                |
| D_nozzle_t              |   50  um     |       | Top diameter of the nozzle       |                |
| Angle_nozzle            |   atan(((D_nozzle_b-D_nozzle_t)*0.5)/H_nozzle)     |       | Angle of the nozzle              |                |
| H_air                   |              |       | Height of the air column         |                |
| R_air                   |              |       | Radius of the air column         |                |
| rho_ag                  |              |       | Density of the agent             |                |
| mu_ag                   |              |       | Viscosity of the agent           |                |
| sigma_surface_ag        |              |       | Surface tension of the agent     |                |
| v_amp                   |              |       | Amplitude of the voltage         |                |
| re_in                   |              |       | Reynolds number                  |                |
| Int_thick               |              |       | Thickness of the interface       |                |
| Mesh_max_interface      |              |       | Maximum mesh size at interface   |                |
| Mesh_min_interface      |              |       | Minimum mesh size at interface   |                |

### Piezoelectric Function
...

### Geometry
...

### Materials
...

### Physics
...

### Mesh
...

### Solver
...

### Study
...

## AWS Cloud Computing Architecture
The AWS EC2 instance was of the r7i.4xlarge variety, running Windows, with 16vCPUs and 131GB of RAM. On average, the simulation made full use of the CPUs, but at most, it consumed 100GB of RAM, and took 8 hours to compute with the previously mentioned parameters. PARDISO was chosen precisely because of this cloud architecture, and the designer is encouraged to choose a solver that best suits their capabilities.
