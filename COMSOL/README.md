## Objective
The objective of this project is to...

## COMSOL Multiphysics Setup
### Parameters
| Name                    | Expression   | Description                      | Source         |
|-------------------------|--------------|----------------------------------|----------------|
| W_chamber               |   117 um     | Width of the chamber             |                |
| L_chamber               |   800 um     | Length of the chamber            |                |
| H_chamber               |   117 um     | Height of the chamber            |                |
| W_restrictor            |   40  um     | Width of the restrictor          |                |
| L_restrictor            |   400 um     | Length of the restrictor         |                |
| H_nozzle                |   67  um     | Height of the nozzle             |                |
| D_nozzle_b              |   83  um     | Bottom diameter of the nozzle    |                |
| D_nozzle_t              |   50  um     | Top diameter of the nozzle       |                |
| Angle_nozzle            |   atan(((D_nozzle_b-D_nozzle_t)*0.5)/H_nozzle)     | Angle of the nozzle              |                |
| H_air                   |   1500 um    | Height of the air column         |                |
| R_air                   |     60 um    | Radius of the air column         |                |
| rho_ag                  | 1427 kg/m^3  | Density of the agent             |                |
| mu_ag                   |  0.014 Pa*s  | Viscosity of the agent           |                |
| sigma_surface_ag        |  0.03 N/m    | Surface tension of the agent     |                |
| v_amp                   |   30 m/s     | Amplitude of the voltage         |                |
| re_in                   |  2 m/s       | Reynolds number                  |                |
| Int_thick               |1.5*Mesh_min_interface        | Thickness of the interface       |                |
| Mesh_max_interface      |      5 um    | Maximum mesh size at interface   |                |
| Mesh_min_interface      |      3 um    | Minimum mesh size at interface   |                |

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
