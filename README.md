
# Experimental Reproduction

This repository contains the Jupyter Notebook used to conduct the experiments and generate the results reported in the associated research paper.

## Repository Contents

```text
.
└── final.ipynb
```

## Requirements

- Python 3.9 or later
- Jupyter Notebook
- WESAD dataset
- A-WEAR EXAM Stress Dataset

### Install Dependencies

Run the following command to install the required Python libraries:

```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn imbalanced-learn jupyter
```

## Datasets

The experiments use two datasets:

1. **WESAD Dataset** – Used for physiological signal analysis and model development.
2. **A-WEAR EXAM Stress Dataset** – Used for cross-dataset evaluation and experimental analysis.

Download the datasets from their respective official sources. Access to the datasets may require accepting their terms of use.

Before executing the notebook, update the dataset directory paths in the notebook to match your local environment.

## Running the Experiments

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

Alternatively, install the dependencies using the command provided above.

### 3. Configure Dataset Paths

Open `final.ipynb` and locate the dataset configuration cells.

Update the paths for:
- WESAD dataset
- A-WEAR EXAM dataset

Ensure that the datasets are accessible from the configured directories.

### 4. Execute the Notebook

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open `final.ipynb` and execute all cells sequentially using **Run All**.

The notebook performs the data preprocessing, feature extraction, model training, evaluation, and experimental analysis.

## Reproducing Experimental Results

Executing the notebook sequentially regenerates the experimental results, including:

- Physiological signal preprocessing and feature extraction.
- Feature-level analysis and correlation visualization.
- Modality ablation experiments.
- Stress prevalence sensitivity analysis.
- Comparison of machine learning classifiers.
- Class imbalance handling using different sampling strategies.
- Model calibration and iterative self-training.
- Subject-independent evaluation.
- Nested cross-validation.
- ROC curve analysis and performance comparisons.
- Subject-level cluster bootstrap confidence intervals.

The experiments use a fixed random seed (`SEED = 42`) wherever configured in the notebook to support reproducibility.

## Generated Outputs

During execution, the notebook generates intermediate data files, evaluation results, and visualizations used in the experimental analysis.

These outputs are generated locally and are not included in this repository. Execute the notebook to reproduce them.

## Reproducibility Notes

- Use the specified datasets and ensure their directory structures are correctly configured.
- Execute notebook cells in their original sequence.
- Maintain the configured random seed when reproducing experiments.
- Ensure all required dependencies are installed.
- Results may vary slightly depending on library versions, hardware, and execution environment.

## Research Scope and Limitations

The experiments are intended for academic research and experimental evaluation. Predictions generated through pseudo-labeling should not be interpreted as independently verified ground-truth labels.

The findings should be interpreted within the limitations of the datasets, subject availability, and cross-domain differences.

## Citation

If you use this implementation or reproduce its experiments in your research, please cite the associated research paper.

**Note:** This repository provides the experimental implementation in the form of a Jupyter Notebook. Dataset files and generated experimental outputs are maintained separately.
