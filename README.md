# Reconstructing-Mitochondrial-Proton-Motive-Force-with-Physics-Informed-Neural-Networks-PINNs-

**Mark I.R. Petalcorin**\
*AAIDEA, U.K.*\
*mark.petalcorin@a-aidea.com*

This study demonstrates that combining physics-informed neural networks with explainable AI enables accurate and interpretable reconstruction of the mitochondrial proton motive force, offering a novel tool for advancing mitochondrial physiology, disease research, and therapeutic discovery.
This repository contains the code, data, and analyses for the paper: *Petalcorin M.I.R (2025) Reconstructing the Mitochondrial Proton Motive Force Using Physics-Informed Neural Networks and Surrogate Bioenergetic Signals (bioRxiv)*

## Overview

The **proton motive force (PMF)** is the electrochemical gradient across the mitochondrial inner membrane that powers ATP synthesis, metabolite transport, and redox signaling. Measuring PMF directly is challenging due to probe limitations, calibration drift, and perturbation of mitochondrial function.

We present a **physics-informed neural network (PINN)** that reconstructs PMF from surrogate **bioenergetic signals (NADH, O₂, electron flux, proton leak, and ROS)**. The model integrates the chemiosmotic equation as a physics constraint, applies SHAP interpretability to uncover context-dependent determinants of PMF, and extends to time-resolved hypoxia–reoxygenation dynamics via recurrent PINNs (rPINNs).

## Aims and Significance
	•	Provide a non-invasive computational framework to reconstruct PMF.
	•	Combine ML + physics constraints for biologically plausible predictions.
	•	Apply explainable AI (SHAP) to identify feature contributions under normoxia vs hypoxia.
	•	Extend to time-series modeling of hypoxia–reoxygenation cycles.
	•	Enable future applications in mitochondrial physiology, disease modeling, and drug discovery.

 ## Repository Structure
<img width="869" height="269" alt="image" src="https://github.com/user-attachments/assets/39ae3eb4-3911-403c-9954-966b1077054a" />

## Dependencies: 
torch, numpy, pandas, matplotlib, seaborn, shap, scipy

## Key Results
	•	R² > 0.99, RMSE < 1 mV across training and validation.
	•	SHAP analysis identified flux + NADH as key under normoxia, and oxygen + ROS under hypoxia.
	•	rPINN captured dynamic PMF decline and recovery during hypoxia–reoxygenation cycles.

 ## Citation
 If you use this code, please cite:

Petalcorin M.I.R (2025) Reconstructing the Mitochondrial Proton Motive Force Using Physics-Informed Neural Networks and Surrogate Bioenergetic Signals (bioRxiv) (in preparation).
DATASHEET.md

 # Datasheet for Synthetic Dataset: 
 pmf_synthetic_curriculum.csv

 ## Motivation
This dataset was generated to simulate mitochondrial bioenergetics under normoxia and hypoxia, supporting the training and validation of PINNs for PMF reconstruction.

 ## Composition
	•	Inputs:
	•	NADH concentration
	•	Oxygen availability (% O₂)
	•	ETC flux
	•	Proton leak
	•	ROS levels
	•	Outputs:
	•	Δψ (membrane potential)
	•	ΔpH (proton gradient)
	•	PMF (calculated via chemiosmotic equation)

Ranges were based on experimental literature (Nicholls & Ferguson, 2013; Murphy, 2009; Brand & Nicholls, 2011). Gaussian noise was added to mimic biological variability.

 ## Collection Process
Synthetic values sampled across physiological ranges for normoxia (O₂ > 40%) and hypoxia (O₂ ≤ 40%). Data generated via controlled random sampling in Python, ensuring coverage across realistic parameter space.

 ## Preprocessing
	•	Normalization of input features
	•	Train/validation/test splits (80/10/10)
	•	Noise injection to simulate measurement error

 ## Uses
	•	Training PINNs to reconstruct PMF
	•	SHAP analysis of feature contributions
	•	Benchmarking recurrent models for time-series PMF

 ## Limitations
	•	Simulated data, not directly measured biological PMF
	•	Assumes steady-state ranges based on literature, may not capture rare pathophysiological extremes

 ## Maintenance
Dataset is static and publicly available in this repository.

# MODEL CARD
Physics-Informed Neural Network for PMF Reconstruction

 ## Model Details
	•	Architecture: Fully connected PINN with 3 hidden layers (64 units, ReLU activation)
	•	Input: NADH, O₂, flux, leak, ROS
	•	Output: PMF prediction
	•	Framework: PyTorch 2.0

 ## Intended Use
	•	Non-invasive reconstruction of PMF from surrogate bioenergetic features
	•	Research applications in mitochondrial physiology, disease modeling, drug screening
	•	Proof-of-concept for integrating physics-informed ML with explainability

 ## Performance
	•	Static data: R² > 0.99, RMSE < 1 mV
	•	Cross-validation: R² = 0.991–0.994
	•	Dynamic rPINN: Accurately tracked PMF during hypoxia–reoxygenation

 ## Interpretability
	•	SHAP feature attribution:
	•	Normoxia: flux + NADH most important
	•	Hypoxia: oxygen + ROS most important
	•	Interaction SHAP: revealed nonlinear dependencies

 ## Ethical Considerations
	•	Simulated dataset limits immediate clinical applicability
	•	Model may not generalize to in vivo human data without retraining on experimental datasets

 ## Limitations
	•	Synthetic-only training may bias generalization
	•	Does not yet integrate multi-omics or spatial heterogeneity of mitochondria

