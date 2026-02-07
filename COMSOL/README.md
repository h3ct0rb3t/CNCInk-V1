# Objective

The objective of this simulation is to model the microfluidic behaviour of a single nozzle from the Xaar 128, so as to allow the designer to 
predict the behaviour of any ink given their rheological properties. Any value not justified explicitly in this document must be assumed to 
have been reverse engineered to match the behaviour of the simulation to the datasheet's stated properties. 

# COMSOL Multiphysics Setup

## Parameters
- List all relevant parameters used in the model.

## Piezoelectric Function
- Describe the piezoelectric functions applied in the model.

## Geometry
- Outline the geometric structure and its significance in the analysis.

## Materials
- Specify the materials used and their properties.

## Physics
- Summarize the physical phenomena modeled in COMSOL.

## Mesh
- Discuss the meshing strategy and its importance in simulations.

## Solver

- XX

## Study
- Explain the study settings and types of analyses performed.

# AWS Cloud Computing Architecture

The AWS EC2 instance was of the r7i.4xlarge variety, running Windows, with 16vCPUs and 131GB of RAM. On average, the simulation made full use of the CPUs, but at most, it consumed 100GB of RAM, and took 8 hours to compute with the previously mentioned parameters. PARDISO was chosen precisely because of this cloud architecture, and the designer is encouraged to choose a solver that best suits their capabilities. 
