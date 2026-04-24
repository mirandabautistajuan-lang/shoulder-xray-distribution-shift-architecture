# shoulder-xray-distribution-shift-architecture

**Cross-station generalization and multi-view information fusion strategies for detecting rotator cuff calcifications.**

This repository contains the source code and experimental pipeline used to evaluate hardware-related distribution shift and input fusion strategies for the detection of **calcific tendinopathy of the rotator cuff (CTRC)** on shoulder radiographs. The study systematically compares station-specific vs. station-agnostic models and analyzes the impact of Early and Late Fusion architectures on diagnostic performance and model explainability.

---

## Project summary

The research utilizes a VGG19-based CNN framework to address two critical questions in musculoskeletal AI:
1. **Hardware-related Distribution Shift:** How models trained on specific acquisition stations (CZC or RAD) perform when deployed on unseen hardware, and how pooled, station-agnostic training improves robustness.
2. **Information Fusion:** Evaluating the most effective way to integrate orthogonal views (External and Internal Rotation). We compare **Early Fusion** (multi-channel input) vs. **Late Fusion** (independent modeling with decision integration).

Our results demonstrate that **station-agnostic training** mitigates performance loss across heterogeneous environments and that **Late Fusion** provides superior diagnostic yield and more anatomically coherent Grad-CAM attention patterns.

---

## Repository structure

### Subfolders
- **Architecture/**: Definitions for VGG19-baseline, Early Fusion, and Late Fusion models.
- **Preprocessing/**: Scripts for DICOM normalization and standardized replication.
- **Models/**: Storage for trained weights (U-Net and VGG19 variants).

### Notebooks (Execution order)

1. **00_environment_setup.ipynb** Environment preparation, library checks, and global configuration.

2. **01_Unet_training_models.ipynb** Training of the U-Net architecture for automated humeral segmentation and ROI extraction.

3. **02_preprocess_dicom_luts.ipynb** DICOM standardization, LUT application, and intensity normalization.

4. **03_data_merge_dicom_clinical.ipynb** Integration of imaging data with associated clinical and demographic metadata.

5. **04_eda_dataset_statistics.ipynb** Exploratory data analysis and descriptive statistics of the study population.

6. **05. Create_subsets.ipynb** Logic for data partitioning, station-specific splits, and class balancing.

7. **06.1_train_CZC_baseline_model_example.ipynb** Training pipeline for the single-projection baseline model (CZC station).

8. **06.2_train_RAD_early_fusion_model_example.ipynb** Implementation and training of the multi-channel early fusion strategy.

9. **06.3_train_RAD_IR_late_fusion_model_example.ipynb** Development of independent projection sub-models for late fusion logic.

10. **07_eval_station_effect_distribution_shift.ipynb** Performance analysis and ROC comparison under cross-station distribution shift.

11. **08_eval_multichannel_input_strategies.ipynb** Comparative evaluation of fusion architectures and Grad-CAM explainability analysis.

---

## Ethics and Privacy
This repository provides **code and workflow only**. In compliance with institutional ethical standards and GDPR, **no patient data or original DICOM files are included**.

---

## Environment
- Python 3.10
- Key libraries: TensorFlow/Keras, Pydicom, Scikit-learn, OpenCV, Matplotlib.

---

## Acknowledgements
This work was supported by the **AI4EOSC project** (“Artificial Intelligence for the European Open Science Cloud”), which has received funding from the European Union’s Horizon Europe research and innovation programme under grant agreement No. 101058593.
