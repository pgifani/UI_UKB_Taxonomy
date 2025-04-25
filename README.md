# 📊 Interactive Visualization and Personalized Risk Estimation Tool

We developed an interactive web-based application using the **Shiny** framework in **R** to visualize patient similarity and perform individualized cardiovascular risk predictions. This app is designed to aid both researchers and clinicians in exploring complex phenotypic data and estimating future cardiovascular risk trajectories for individual patients.

---
## 🧠 Short description

Our training phenomapping model was incorporated into a Shiny App (R version 4.3.3), developed as a tool to aid the communication of patients' personalised profiles. We used age, sex, and the tree’s phenotypic input features to fit Fine-Gray models for incident cardiovascular events (myocardial infarction, atrial fibrillation, stroke, and major adverse cardiovascular event (MACE)), with death as a competing risk. Individual predicted probabilities of an event were then overlaid on the tree. The performance of these models was assessed using 5-fold cross-validation, and the ROC AUC at 5 years was reported for each outcome.
A screenshot of the Shiny App interface is shown in Figure X, illustrating the interactive phenotypic map, user-adjustable input sliders, and real-time risk prediction plots.
We developed an interactive web-based application using the Shiny framework in R to visualize patient similarity and perform individualized cardiovascular risk predictions. The tool allows users to explore a low-dimensional embedding of high-dimensional cardiac imaging and clinical data, generated via the DDRTree algorithm from the monocle package.

A scatter plot visualizes each sample as a point on a 2D map. By clicking on any point, the nearest actual patient record from the dataset is identified using Euclidean distance. Once selected, the patient's feature values are dynamically loaded into the user interface, where multiple sliders allow modification of key clinical variables (e.g., age, blood pressure, left ventricular ejection fraction). Additional clinical and imaging features can be added interactively.

The selected or edited sample is then standardized and adjusted for covariates using a polynomial regression model, which corrects for demographic influences such as age, sex, and ethnicity. The adjusted data is passed through a trained random forest model, scaler, and PCA transformer (pre-trained using scikit-learn in Python, accessed via the reticulate package in R) to predict a new low-dimensional position on the scatter plot.

For each cardiovascular outcome of interest—Heart Failure, Atrial Fibrillation, and Major Adverse Cardiovascular Events (MACE)—we use pre-traine
## 🧠 Key Features

- **2D Phenotypic Mapping**: A scatter plot generated via the **DDRTree** algorithm from the `monocle` package displays a low-dimensional embedding of patient phenotypes. Users can click on any sample to retrieve the nearest actual patient record based on Euclidean distance.

- **Dynamic Feature Control**: The UI automatically loads the selected sample's feature values into interactive sliders. Users can adjust essential and extended clinical/imaging features in real time.

- **Live Reprojection**: Once adjusted, the data is:
  - Standardized and corrected for covariates (age, sex, ethnicity).
  - Passed through a **trained Random Forest + Scaler + PCA pipeline** (in Python via `reticulate`).
  - Projected back into phenotypic space to update the sample's location.

- **Survival Risk Prediction**: Fine-Gray competing risk models are used to predict:
  - **Atrial Fibrillation (AF)**
  - **Heart Failure (HF)**
  - **Major Adverse Cardiovascular Events (MACE)**


  Each risk is shown as:
  - Cumulative incidence plots over time
  - Real-time **5-year probability estimates**

- **Model Performance**: Models were trained on phenotypic inputs, age, and sex. Their performance was validated using 5-fold cross-validation, with 5-year AUCs reported per outcome.

---

## 🖼️ UI Screenshot 
![UI Screenshot Placeholder](./Figure8.bmp)

> *Figure: Screenshot of the interactive Shiny App used for phenotypic mapping and personalized cardiovascular risk prediction. The interface includes: (1) a central 2D scatterplot representing the phenotypic continuum, where users can click to select a representative patient sample; (2) dynamic sliders on the left for modifying clinical and imaging-based variables; and (3) three cumulative incidence plots on the right estimating individual risk trajectories over time for atrial fibrillation (AF), heart failure (HF), and major adverse cardiovascular events (MACE). Risk scores for 5-year prediction are displayed beneath each plot. Adjusted sample positions and updated risk outputs are computed in real-time using the trained phenomapping and survival models.*

---

## 📦 Technical Stack

- **R Shiny** (frontend + reactive logic)
- **Python (scikit-learn)** for model inference via `reticulate`
- **ggplot2** for plotting
- **Fine-Gray survival models** for risk estimation

---
### Shiny App Directory (internal only)

All source files for the interactive Shiny App are located in the following shared drive:
```
Z:\pi514\input_for_ddrtree_ukbb\ukbb_inputs_final\UKB_taxonomy_UI
```
This includes:
- `ui_app.r`: Main file for launching the Shiny application
- `__functions.R`: Supporting functions for data adjustment and modeling
- `models/`: Contains all pre-trained models and min/max scaling references
- `synthetic_dataset_500_samples.csv`: synthetic data file used for demonstration and model input (you can change witn real_data_all.csv or real_data_5000_samples.csv)

---
## 🧪 Authors & Contributions
This UI was developed as part of the UK Biobank phenomapping framework.

Feel free to open an issue or contribute via pull request!
