# Stress Detection

## Overview
This repository contains the data processing, feature extraction, and machine learning pipeline for detecting stress and affective states using Empatica E4 wristband data. The project utilized both a known labeled dataset (WESAD) and an unlabeled dataset (ExamStress) to build a robust semi-supervised classification model. 

The pipeline extracts physiological features (EDA, HR, ACC, TEMP) over sliding windows, clusters the data to discover inherent patterns, and utilizes a self-training (pseudo-labeling) methodology with Logistic Regression to classify Baseline vs. Stress states.

---

## File Structure

This repository is structured to be modular, reproducible, and easy to navigate. The core Jupyter notebooks are numbered to reflect their sequential order and primary functions in the pipeline.

### 1. `01_feature_extraction_pipeline.ipynb`
* **Description:** 
  * Validates dataset completeness by iterating through participant and exam folders.
  * Implements Empatica E4 CSV parsing pipeline.
  * Applies a sliding window approach (with customizable overlap) ensuring $\ge 95\%$ signal coverage.
  * Extracts 22 statistical and physiological features across EDA, HR, ACC, and TEMP signals (e.g., slopes, motion power, SCR counts, medians).
  * Performs K-Means clustering and Silhouette scoring to discover optimal grouping ($k=3$) within the unlabeled physiological data.

### 2. `02_self_training_stress_classifier.ipynb`
* **Description:** 
  * Loads the WESAD labeled feature set and the newly extracted ExamStress features.
  * Cleans and maps WESAD labels into binary states: `0` (Baseline) and `1` (Stress).
  * Splits WESAD into training and holdout (calibration/test) sets.
  * Standardizes features using `StandardScaler`.
  * Optimizes confidence thresholds using precision-recall curves.
  * Executes a Self-Training algorithm iteratively, applying high-confidence pseudo-labels to the ExamStress dataset.
  * Evaluates the final model using classification reports, macro/weighted averages, and visualizes the top 10 ROC curves.

---

## Methodology

### Feature Extraction
The extraction pipeline filters the raw physiological signals (e.g., using `scipy.signal.medfilt` for EDA) and computes the following feature sets:
* **EDA:** Mean, STD, Min, Max, Median, Linear Slope, Motion Power, and SCR Count.
* **HR / TEMP:** Basic statistics (Mean, STD, Min, Max, Median) and Linear Slope.
* **ACC:** Mean Magnitude, STD Magnitude, and ACC Energy.

### Machine Learning
Due to the lack of ground-truth labels in the ExamStress dataset, the modeling phase relies on **Self-Training**:
1. A base Logistic Regression model is trained on the WESAD dataset.
2. The model predicts probabilities on the unlabeled ExamStress data.
3. Unlabeled samples passing the high-confidence threshold are assigned pseudo-labels and appended to the training set.
4. The model is re-trained iteratively until no new high-confidence samples are found.

---

## Dependencies
Ensure you have the following Python packages installed to run the notebooks:
* `pandas`
* `numpy`
* `scipy`
* `scikit-learn`
* `matplotlib`

## How to Use
1. Run `01_feature_extraction_pipeline.ipynb` to generate the CSV files containing the 60-second windowed features.
2. Run `02_self_training_stress_classifier.ipynb` to execute the pseudo-labeling pipeline and view the final ROC/Classification metrics.
