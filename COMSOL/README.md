## Objective

### Zenodo DOI

The working file can be downloaded using the following DOI: https://doi.org/10.5281/zenodo.18512589

## COMSOL Multiphysics Setup
### Parameters

The following list constitutes the entirety of the used parameters in the COMSOL simulation, which is formatted as:

- Name: Assigned name to the variable
- Expression: Value of the variable
- Description: What the value is referencing
- Source: Where the value was derived from

The justification for the values that need it can be found in their respective section.


| Name                    | Expression   | Description                      | Source         |
|-------------------------|--------------|----------------------------------|----------------|
| W_chamber               |   117 um     | Width of the chamber             |   Datasheet    |
| L_chamber               |   800 um     | Length of the chamber            |   Datasheet    |
| H_chamber               |   117 um     | Height of the chamber            |   Datasheet    |
| W_restrictor            |   40  um     | Width of the restrictor          |   Calibrated   |
| L_restrictor            |   400 um     | Length of the restrictor         |   Calibrated             |
| H_nozzle                |   67  um     | Height of the nozzle             |   Calibrated    |
| D_nozzle_b              |   83  um     | Bottom diameter of the nozzle    |   Calibrated   |
| D_nozzle_t              |   50  um     | Top diameter of the nozzle       |     Datasheet     |
| Angle_nozzle            |   atan(((D_nozzle_b-D_nozzle_t)*0.5)/H_nozzle)     | Angle of the nozzle |    Calibrated   |
| H_air                   |   1500 um    | Height of the air column         |   Project Scope   |
| R_air                   |     60 um    | Radius of the air column         |   Project Scope   |
| rho_ag                  | 1427 kg/m^3  | Density of Ag Ink             |  Datasheet    |
| mu_ag                   |  0.014 Pa*s  | Viscosity of Ag Ink          |    Datasheet   |
| sigma_surface_ag        |  0.03 N/m    | Surface tension of Ag Ink     |    Datasheet   |
| v_amp                   |   30 m/s     | Velocity Amplification Factor         |    Calibrated  |
| re_in                   |  2 m/s       | Level Set Reinitilization Parameter                  |   Calibrated    |
| Int_thick               |1.5*Mesh_min_interface        | Level Set Interface Thickness       |  Calculated   |
| Mesh_max_interface      |      5 um    | Maximum mesh size at interface   |    Calibrated  |
| Mesh_min_interface      |      3 um    | Minimum mesh size at interface   |    Calibrated  |



### Piezoelectric Function

A simple multiphysics piezoelectric simulation (not included in the repo) was performed to obtain a general function for driving force of droplet formation. This function was copied directly into a COMSOL interpolation, and then tweaked manually to achieve the desired droplet behaviour. 

<img width="1035" height="344" alt="image" src="https://github.com/user-attachments/assets/eabda06e-0714-43a8-b17e-8348dd91f138" />

The peak corresponds to the "pull back" behaviour of inkjet droplets, while the troph corresponds to the "push out" or "ejection" behaviour. Both are required to achieve satellite free formation of droplets (Suh & Son, 2019). The designer is encouraged to observe the droplet formation in their own laboratory, and calibrate this function accordingly. 

### Geometry

The geometry is composed of 5 main components:

1. Chamber
2. Restrictor
3. Nozzle
4. Air (fine mesh)
5. Air (regular mesh)

Height is in the Z-plane. The height of the restrictor is the same as the chamber. The nozzle geometry itself is derived partially from the literautre (Xiao et. al, 2018), as XAAR does not
disclose this information. Therefore, some of the parameters had to be calibrated to match expected behaviour from the technical datasheet, mainly droplet volume and speed, and are not meant to be taken as literal values representative of the XAAR 128 printhead. Those parameters are clearly labeled in the "Parameters" section as "Calibrated". 

<img width="582" height="302" alt="image" src="https://github.com/user-attachments/assets/cb3f3574-12ea-45c9-926b-0112ac34ae35" />

<img width="489" height="295" alt="image" src="https://github.com/user-attachments/assets/68ddc01e-4d32-4984-918e-1cf6cc249499" />


### Materials

The six domains (2 for each half of the chamber, 1 for the restrictor, and 1 for each remaining component), are all a Multiphase Material of silver ink and air, with the volume fraction determined by the Level Set function, and with air as the Constrained Phase. 


### Physics

The simulation has 2 Physics Interfaces, Laminar Flow (spf) and Level Set (ls), which interact via the Multiphysics coupling Two-Phase Flow (tpf). 

Laminar Flow: All domains are encompassed by spf. The initial values are 0. All chamber and restrictor walls operate under a no slip condition. Gravity is applied in the z-axis. The bottom of the air cylinder is defined as the outlet. The chamber wall opposite to nozzle has a velocity in the z-axis, defined as the piezoelectric function times the amplification variable v_amp, with a value determined empirically to balance the "pull back" and the "push out" behaviour. 

Level Set: All domains are encompassed by ls. Ink occupies the chamber, the restrictor, and the nozzle. Air occupies the rest. The bottom of the air cylinder is defined as the outlet.

Two-Phase flow: All domains are encompassed by tpf. The air and the nozzle have wetted wall behaviour, with the contact angle defined as pi/2+Angle_nozzle. 

### Mesh

The chamber has a fixed mesh size of 10-15x10^6 m, the refined air has a fixed mesh size of 75% of min. and max. values from parameters, and the mesh size at the nozzle and air are defined in the parameters. 

### Study

A time dependent study was used, with both the Stationary Solver and the Time Dependent Solver using PARDISO. 

## AWS Cloud Computing Architecture
The AWS EC2 instance was of the r7i.4xlarge variety, running Windows, with 16vCPUs and 131GB of RAM. On average, the simulation made full use of the CPUs, but at most, it consumed 100GB of RAM, and took 8 hours to compute with the previously mentioned parameters. PARDISO was chosen precisely because of this cloud architecture, and the designer is encouraged to choose a solver that best suits their capabilities.
