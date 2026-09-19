# Evaluating the Effect of Uncertainty in Pressure Boundary Condition on Patient-Specific Modeling of Coronary Hemodynamics

**Author:** Nishanth Panda  
**Institution:** Odisha University of Technology and Research (OUTR), Bhubaneswar  
**Department:** Biotechnology  
**Date:** May 2025  

## 📌 Project Overview
This project focuses on computational simulations of blood flow to realistically quantify coronary flow and pressure, aiding in the understanding of hemodynamics in coronary artery disease. Using a combination of 0-D lumped parameter models (Windkessel models) and 3-D Computational Fluid Dynamics (CFD), the study evaluates how uncertainties in pressure boundary conditions affect patient-specific models of coronary hemodynamics. 

## 🎯 Objectives
*   Reconstruct patient-specific 3D coronary artery geometries from medical imaging data.
*   Simulate blood flow using CFD under realistic physiological conditions.
*   Implement 3-element Windkessel models as outlet boundary conditions to account for microvascular resistance and compliance.
*   Perform Uncertainty Quantification (UQ) and Sensitivity Analysis on boundary parameters (Resistance and Compliance) using Monte Carlo simulations.
*   Evaluate Wall Shear Stress (WSS), pressure distributions, and velocity fields to identify potential regions of atherosclerotic risk.

## 🛠️ Technologies & Software Used
*   **SimVascular:** 3D model reconstruction from CT imaging, segmentation, mesh generation (via TetGen), and CFD flow simulations.
*   **ParaView:** Post-processing and visualization of 3D hemodynamic parameters (Pressure, WSS, Velocity).
*   **MATLAB:** 0-D mathematical modeling, solving Ordinary Differential Equations (ODEs) for 2-, 3-, and 4-element Windkessel models, and executing Monte Carlo simulations for sensitivity analysis.
*   **Plot Digitizer:** Extraction of aortic inflow waveform data from literature.

## 🔬 Methodology

### 1. 0-D Modeling (MATLAB)
The systemic circulation and downstream resistance were mathematically modeled using the Windkessel (WK) effect. The governing equation for the optimal 3-Element Windkessel model is:
$$ \left(1 + \frac{R_1}{R_2}\right) I(t) + C R_1 \frac{dI(t)}{dt} = \frac{P(t)}{R_2} + C \frac{dP(t)}{dt} $$
Where:
*   $R_1$ = Characteristic Impedance (Proximal Resistance)
*   $R_2$ = Peripheral Resistance
*   $C$ = Compliance
*   $I(t)$ = Inflow rate
*   $P(t)$ = Pressure

**Uncertainty & Sensitivity Analysis:** Monte Carlo simulations (1000 trials) were run introducing standard deviations (0%, 3%, 6%, 12%) to the parameters ($R_1, R_2, C$) to observe the resulting variance in the pressure waveform output.

### 2. 3-D Patient-Specific CFD (SimVascular)
*   **Governing Equations:** 3D incompressible Navier-Stokes equations governing mass and momentum conservation.
    *   $\nabla \cdot \mathbf{v} = 0$
    *   $\rho \left( \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla)\mathbf{v} \right) = -\nabla p + \mu \nabla^2 \mathbf{v} + \mathbf{f}$
*   **Boundary Conditions:** Time-dependent inflow waveform applied at the aorta. RCR (3-element Windkessel) boundary conditions applied at each distal coronary outlet.
*   **Meshing:** High-quality tetrahedral meshing (~300,000 elements) generated to capture boundary layer effects.

## 📊 Key Results
1.  **Model Efficacy:** The 3-element Windkessel model proved the most reliable in replicating physiological pressure decay and wave reflections compared to 2-element and 4-element models.
2.  **Sensitivity Analysis:** Variations in distal resistance ($R_2$) had the most significant impact on the mean and peak pressure waveforms. Increased inflow globally elevated the pressure gradient.
3.  **3-D Hemodynamics:** Low Wall Shear Stress (WSS) zones were identified in proximal segments and curvatures (indicating potential atherogenic risk), while moderate-to-high WSS was observed at distal bifurcations. 

## 📁 Repository Contents (Appendix Scripts)
If replicating the MATLAB numerical simulations, the following scripts are referenced in the project:
*   `dXdT_2WK.m`: Solves the 2-Element Windkessel ODE.
*   `dXdT_3WK.m`: Solves the 3-Element Windkessel ODE (Primary model).
*   `dXdT_4WK.m`: Solves the 4-Element Windkessel ODE including inertance ($L$).
*   `MonteCarlo_UQ.m`: Executes the Monte Carlo uncertainty quantification.
*   `Sensitivity_R1_R2_C.m`: Iteratively perturbs $R_1$, $R_2$, and $C$ by specific percentages to calculate $\Delta P$.

*Note: The CSV file `Aortic Inflow data 1.csv` is required for the MATLAB scripts to run.*
