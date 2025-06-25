# Unveiling Band Gaps in Perovskite Oxides for Next-Gen Electronics

## Project Overview

This repository contains the code, models, and documentation for predicting the band gaps of perovskite oxides using advanced machine learning (ML) techniques. The project aims to accelerate the discovery of new materials for applications in solar cells, LEDs, and semiconductors by enabling rapid and accurate band gap predictions, overcoming the limitations of traditional computational approaches like Density Functional Theory (DFT).

## Problem Statement

Perovskite oxides are a versatile class of materials with tunable electronic properties. The band gap (Eg) is a key property that determines whether a material acts as an insulator, semiconductor, or conductor. Traditional DFT-based methods for band gap prediction are computationally expensive and time-consuming (often taking 48+ hours per material).

**Project Goals:**
- **Classification**: Identify materials as insulators (Eg ≥ 0.5 eV) or non-insulators (Eg < 0.5 eV).
- **Regression**: Accurately predict the band gap value (Eg) for insulators.

## Dataset Description

- **Source**: Provided by the EXCAVATE challenge.
- **Size**: 5,152 unique perovskite compositions.
- **Features**:
  - **Compositional**: A-site/B-site cations, oxidation states, chemical formula.
  - **Electronic/Atomic**: HOMO/LUMO levels, ionization energy, electronegativity, electron affinity, Zunger’s pseudopotential radius.
  - **Structural/Geometric**: Tolerance factor, octahedral factor, mismatch factor.
  - **Target**: PBE Band Gap (Eg in eV).

## Feature Engineering

- **Magpie Library**: Added 132 elemental property and statistical features to enhance the dataset.
- **Feature Selection**: Used correlation analysis and Ridge Regression to retain the most relevant features (reduced from 304 to top 25).
- **Data Cleaning**: Handled missing values, removed outliers, and standardized features.

## Methodology

1. **Exploratory Data Analysis (EDA)**:  
   - Analyzed feature distributions, correlations, and class imbalance.
   - Visualized band gap distributions and feature importance.

2. **Preprocessing**:  
   - Addressed data imbalance (more non-insulators than insulators).
   - Split data: 80% training, 20% testing (stratified).

3. **Two-Stage ML Pipeline**:  
   - **Stage 1**: Classification to filter insulators.
   - **Stage 2**: Regression to predict Eg for insulators.

4. **Model Interpretability**:  
   - Used SHAP and feature importance analysis to understand model decisions.

## Machine Learning Models

### Classification
- **Model**: HistGradientBoostingClassifier
- **Purpose**: Classify materials as insulators or non-insulators.
- **Key Features**: HOMO/LUMO, electronegativity, atomic properties, tolerance factor, melting temperature.

### Regression
- **Model**: Stacking Regressor
  - **Base Learners**: Random Forest, XGBoost, LightGBM, CatBoost, Gradient Boosting, Histogram-based Gradient Boosting, Extra Trees.
  - **Meta-Learner**: Ridge Regression.
- **Purpose**: Predict the exact band gap for insulators.
- **Key Features**: Atomic number, Magpie features, electronegativity, ionization energy, oxidation state, valence electrons, melting temperature.

## Results & Insights

- **Classification**:  
  - High accuracy and ROC-AUC in distinguishing insulators from non-insulators.
  - Feature engineering (Magpie) significantly improved performance.

- **Regression**:  
  - Stacking Regressor outperformed individual models, providing robust and accurate Eg predictions.
  - Identified key features: ionization energy, electronegativity, d-band center, valence electron count, lattice constant.

- **Model Interpretability**:  
  - Feature importance analysis provided insights into the physical drivers of band gap formation.

## Limitations

- **Data Imbalance**: More non-insulators than insulators may bias the classifier.
- **High-Dimensional Feature Space**: Risk of overfitting; mitigated via feature selection.
- **Complex Structure-Property Relationships**: Perovskite chemistry is intricate; some relationships may not be fully captured.
- **Model Interpretability**: Ensemble models are complex; addressed with SHAP and feature analysis.
- **Generalizability**: Current pipeline is tailored to perovskites; extension to other material systems is future work.

## Future Work

- **Data Augmentation**: Use SMOTE or cost-sensitive learning to balance classes.
- **3D Structural Descriptors**: Incorporate crystal structure features using pymatgen or JARVIS-DFT.
- **Advanced ML Architectures**: Explore Graph Neural Networks and Transformers.
- **Hybrid ML-DFT Pipeline**: Use ML for rapid screening, followed by DFT validation.
- **Expand Scope**: Apply methodology to other material classes beyond perovskites.

## Usage Instructions

1. **Clone the Repository**
   ```bash
   git clone https://github.com/abhik1711/Material-Classification-and-Energy-Band-Prediction.git
   cd Material-Classification-and-Energy-Band-Prediction
   ```

2. **Install Dependencies**

3. **Run the Notebook**
   - Open `Mischmetal_Excavate.ipynb` in Jupyter or Google Colab.
   - Follow the notebook sections for EDA, preprocessing, model training, and evaluation.

4. **Dataset**
   - Ensure `dataset_excavate.xlsx` is in the repository directory.


## Repository Structure

```
├── dataset_excavate.xlsx         # Main dataset
├── Mischmetal_Excavate.ipynb     # Jupyter notebook with code
├── README.md                     # This file
```

## Contributors

- Abhinav Karade
- Dishant Bothra
- Priyadarshi Kumar

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

## Contact

For questions, suggestions, or collaborations, please contact:  
**Email:** [abhi.karade10@gmail.com](mailto:abhi.karade10@gmail.com)

**Acknowledgement:**  
This project was developed for the EXCAVATE Challenge, COMPOSIT 2025.

