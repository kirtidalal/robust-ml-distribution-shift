
# Empirical Analysis of Distributionally Robust Optimization under Group and Distribution Shifts

This repository contains an empirical research project studying how different learning objectives behave under **distributional uncertainty** in tabular decision-making problems. The project compares **Empirical Risk Minimization (ERM)** with **Distributionally Robust Optimization (DRO)** and **Group-DRO**, focusing on robustness–accuracy trade-offs and optimization behavior.

The goal is not to propose new algorithms, but to **understand when and why robust objectives succeed or fail**  under realistic distribution shifts.



## Motivation

Machine learning models deployed in real decision systems often face conditions that differ from their training data. Population characteristics shift, subgroup proportions change, and errors are distributed unevenly across sub-populations. Models optimized for average-case performance may therefore perform poorly on vulnerable or underrepresented groups.

Distributionally robust learning frameworks attempt to address these issues by optimizing against worst-case losses. However, robust objectives can introduce trade-offs such as reduced average accuracy, slower convergence, or unstable optimization dynamics. This project empirically studies these effects in a controlled and reproducible setting.

---

## Research Objective

To empirically compare **ERM**, **DRO**, and **Group-DRO** on tabular credit-risk data under controlled distribution shifts, with emphasis on:

- worst-group versus average performance  
- robustness–accuracy trade-offs  
- convergence behavior of robust objectives  
- sensitivity to uncertainty set size  



## Datasets

- **Primary:** HELOC Credit Risk Dataset  
- **Secondary (stress-test):** German Credit Dataset  

Both datasets involve binary classification in decision-sensitive contexts and are suitable for subgroup robustness analysis.



## Model Choice

To isolate the effects of optimization objectives from architectural complexity, this project uses **logistic regression** as the base model. This allows clearer interpretation of convergence behavior and robustness effects.



## Learning Objectives

- **ERM:** Standard empirical risk minimization using binary cross-entropy  
- **DRO:** CVaR-style tail-risk minimization with uncertainty size controlled via a parameter `alpha`  
- **Group-DRO:** Worst-case loss minimization across predefined groups using adversarial reweighting  



## Group Construction

Groups are derived from interpretable sub-populations such as:

- income quantile buckets  
- employment length buckets  
- age buckets  

These groupings enable analysis of worst-case subgroup performance without framing the study as a fairness intervention.



## Distribution Shift Scenarios

The following shifts are introduced to simulate deployment mismatch:

1. **Temporal shift:** training on earlier samples and evaluating on later samples  
2. **Subpopulation shift:** downsampling one group during training while preserving natural proportions at test time  
3. **Label-noise shift (optional):** injecting asymmetric noise into one selected group  



## Evaluation Metrics

Reported metrics include:

- overall accuracy  
- worst-group accuracy  
- expected calibration error (ECE)  
- robustness gap (worst-group accuracy − average accuracy)  

Additional diagnostics include variance of group losses across training.



## Convergence Analysis

Optimization behavior is analyzed by tracking:

- training loss trajectories  
- worst-group loss over iterations  
- adversarial group weights in Group-DRO  
- sensitivity of convergence to the DRO uncertainty parameter  



## Repository Structure

robust-ml-credit/
├── data/
├── models/
├── objectives/
│ ├── erm.py
│ ├── dro.py
│ └── group_dro.py
├── experiments/
├── plots/
├── README.md
└── report.pdf




## Status

This repository is under active development. Core objective implementations and experimental scaffolding are in place, with ongoing work focused on systematic evaluation and analysis.

