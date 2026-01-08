
# Particle Physics–Inspired Anomaly Detection

This project implements an **unsupervised anomaly detection pipeline inspired by particle physics (ATLAS/CMS)** using the Higgs Boson dataset.  
The goal is to identify rare or anomalous events **without using labels during training**, mimicking real-world searches for new physics at the LHC.

---

## Project Motivation

In high-energy physics, new phenomena often appear as **subtle deviations** from known Standard Model processes.  
Because labels for new physics are unavailable, **unsupervised anomaly detection** is a critical tool.

This project demonstrates:
- Physics-aware data preprocessing
- Unsupervised learning on background-only data
- Physics-inspired feature engineering
- Quantitative evaluation using held-out labels

---

##  Dataset

- **Source:** Kaggle Higgs Boson Challenge
- **Events:** ~250,000 proton–proton collision events
- **Features:** Kinematic and derived physics variables
- **Labels:**  
  - `b` → background (normal events)  
  - `s` → signal (Higgs events, used *only* for evaluation)

>  Labels are **never used during training**.

---

##  Methodology

###  Preprocessing (Physics-Aware)
- Replace missing-value marker `-999` with NaN
- Median imputation (background-only)
- Standard scaling (background-only)
- Log-transform of high-dynamic-range features (`pt`, `mass`, `met`)
- Strict avoidance of label leakage

---

###  Physics-Inspired Feature Engineering
Additional features motivated by ATLAS analyses:
- Transverse momentum ratios
- Mass-to-momentum ratios
- Event balance variables
- Jet activity normalization
- Angular correlation compressions

These features improve scale invariance and anomaly sensitivity.

---

###  Anomaly Detection Model
- **Model:** Fully connected Autoencoder (PyTorch)
- **Training data:** Background events only
- **Bottleneck:** Strong compression to enforce manifold learning
- **Loss:** Reconstruction error (MSE / Huber)
- **Anomaly score:** Per-event reconstruction error

---

###  Evaluation
- ROC–AUC using labels (evaluation only)
- Comparison before/after physics-inspired improvements
- Typical AUC achieved: **~0.60–0.70** (expected for this task)

---

##  Results (Summary)

| Model Variant | ROC AUC |
|--------------|--------|
| Baseline Autoencoder | ~0.58 |
| Tight bottleneck AE | ~0.63 |
| + Physics-inspired features | No significant AUC gain |

This behavior is expected due to the highly engineered nature of the dataset.

---

## Repository Structure

```text
├── Predictive_modelling.ipynb   # Main analysis notebook
├── README.md                    # Project documentation
├── figures/                     # Plots and visualizations



