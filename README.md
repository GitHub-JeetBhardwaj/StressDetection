# Preventing academic breakdown: A semi-supervised multimodal transfer learning framework for cross-domain early arousal detection

## Description
This repository contains the data processing, feature extraction, and machine learning pipeline for detecting stress and affective states using Empatica E4 wristband data. It utilized both a known labeled dataset (WESAD) and an unlabeled dataset (ExamStress) to build a robust semi-supervised classification model. The pipeline extracts physiological features over sliding windows, clusters the data to discover inherent patterns, and utilizes a self-training methodology with Logistic Regression to classify Baseline vs. Stress states.

## Dataset Information
The models in this repository process multimodal physiological data (EDA, HR, ACC, TEMP). It utilizes two distinct datasets:
* **WESAD (Wearable Stress and Affect Dataset):** Used as the primary labeled dataset for initial model training. Available at: https://www.kaggle.com/datasets/mohamedasem318/wesad-full-dataset
* **Wearable Exam Stress Dataset:** Used as the unlabeled cross-domain target dataset for the semi-supervised learning pipeline. Available at: https://physionet.org/content/wearable-exam-stress/1.0.0/

## Code Information
This repository is modular and relies on two primary Jupyter Notebooks executed sequentially:
1. `01_feature_extraction_pipeline.ipynb`: Validates the raw Empatica E4 dataset structure, implements a robust CSV parsing pipeline, and extracts 22 statistical and physiological features using a 60-second sliding window approach. It also performs K-Means clustering.
2. `02_self_training_stress_classifier.ipynb`: Loads the extracted features, maps WESAD labels into binary states, standardizes features, and executes the Self-Training algorithm to iteratively apply high-confidence pseudo-labels to the ExamStress dataset.

## Usage Instructions
1. Clone this repository to your local machine.
2. Download the datasets from the links provided above.
3. Place your raw Empatica E4 data inside a `data/` directory following the structure: `Participant_ID/Exam_Name/`.
4. Run `01_feature_extraction_pipeline.ipynb` to generate the CSV files containing the 60-second windowed features.
5. Run `02_self_training_stress_classifier.ipynb` to execute the pseudo-labeling pipeline and evaluate the final model.

## Requirements
To execute this code, the following Python libraries are required:
* `pandas`
* `numpy`
* `scipy`
* `scikit-learn`
* `matplotlib`

## Methodology
The methodology relies on a semi-supervised transfer learning framework:
1. **Feature Extraction:** Extracts 22 physiological features across EDA, HR, ACC, and TEMP signals using 60-second sliding windows (ensuring >= 95% signal coverage). Filters are applied (e.g., median filtering for EDA) prior to extraction.
2. **Self-Training (Pseudo-labeling):** A base Logistic Regression model is trained on the labeled WESAD dataset and predicts probabilities on the unlabeled ExamStress data. Optimal thresholds for Class 0 and Class 1 are calibrated dynamically. Unlabeled samples passing the high-confidence threshold are assigned pseudo-labels and appended to the training set. This loops iteratively.

## Citations
If you utilize this code or methodology in your research, please cite the associated article and the source datasets:
* WESAD Dataset: https://www.kaggle.com/datasets/mohamedasem318/wesad-full-dataset
* Wearable Exam Stress Dataset: https://physionet.org/content/wearable-exam-stress/1.0.0/
* Repository: https://github.com/GitHub-JeetBhardwaj/StressDetection

## Contribution Guidelines
This project is provided for academic and research purposes. Pull requests and collaborative improvements are appreciated.
