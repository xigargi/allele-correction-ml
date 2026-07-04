# Allele Correction ML

[![Python 3.11](https://img.shields.io/badge/python-3.11-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Code style: ruff](https://img.shields.io/badge/code%20style-ruff-000000.svg)](https://github.com/astral-sh/ruff)

A two-stage machine learning pipeline to detect and correct erroneous allele values from DNA sequencer output, applied to canine genetic identification.

This project was developed as part of a Master's Thesis (TFM), addressing the reliability of genetic identification data by automatically detecting and correcting numerical errors introduced during the sequencing process.

---

## Table of Contents

- [Problem Statement](#problem-statement)
- [Workflow](#workflow)
- [Objectives](#objectives)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Results](#results)
- [Tech Stack](#tech-stack)
- [License](#license)

---

## Problem Statement

DNA sequencers used for canine genetic identification can return erroneous numerical values for certain alleles due to technical artifacts introduced during the sequencing process. These errors can compromise the reliability of the resulting genetic profile and the downstream database used for identification purposes.

This project implements a **two-stage machine learning pipeline** that:

1. **Detects** which allele values are likely to be erroneous — *classification model*
2. **Corrects** the detected erroneous values to their expected value — *regression model*

## Workflow

![Pipeline workflow](reports/figures/pipeline_workflow_en.svg)

*Proposed workflow to achieve the project's objectives — from raw sequencer output to a corrected, genotyped database.*

| Stage | Description |
|---|---|
| **Sequencer** | Raw genetic data acquisition |
| **Change Detector** | Classification model flags alleles likely to be erroneous |
| **Corrector** | Regression model corrects the flagged values |
| **Corrected Samples** | Output of the correction stage |
| **Genotyping** | Genotype assignment based on corrected data |
| **Database** | Final storage of validated genetic profiles |

## Objectives

The main objective of this project is to develop a machine learning model capable of detecting and correcting erroneous numerical values returned by the sequencer used in the context of canine genetic identification.

To achieve this, the following tasks were carried out:

- **Exploratory Data Analysis (EDA)** to determine the most suitable preprocessing strategies
- **Feature extraction and selection** of the most determinant characteristics
- **Training and comparison of multiple ML techniques** for detecting incorrect data (detection model)
- **Training and comparison of multiple ML techniques** for correcting the data (correction model)
- **Exploration of hyperparameter tuning methods** for both models

## Project Structure

```
allele-correction-ml/
│
├── data/
│   ├── raw/                  <- Original, immutable sequencer data
│   ├── interim/               <- Intermediate transformed data
│   ├── processed/             <- Final data used for modeling
│   └── external/              <- Data from third-party sources
│
├── notebooks/                 <- Jupyter notebooks for exploration and prototyping
│
├── allele_correction_ml/      <- Source code
│   ├── config.py                 <- Paths and configuration variables
│   ├── dataset.py                <- Data loading and cleaning
│   ├── features.py               <- Feature engineering
│   ├── plots.py                   <- Visualization utilities
│   └── modeling/
│       ├── train.py               <- Training of classifier and regressor
│       └── predict.py             <- Inference pipeline (classifier → regressor)
│
├── models/                    <- Trained and serialized models
├── reports/
│   └── figures/                <- Generated plots and figures
├── docs/                       <- Project documentation (MkDocs)
├── tests/                      <- Unit tests
│
├── requirements.txt
├── pyproject.toml
└── README.md
```

## Installation

Clone the repository:

```bash
git clone https://github.com/xigargi/allele-correction-ml.git
cd allele-correction-ml
```

Create and activate a virtual environment:

```bash
python -m venv venv
venv\Scripts\activate      # Windows
source venv/bin/activate   # macOS/Linux
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Usage

> This section will be updated as the training and inference scripts are finalized.

```bash
# Train the classifier (detection model)
python -m allele_correction_ml.modeling.train --model classifier

# Train the regressor (correction model)
python -m allele_correction_ml.modeling.train --model regressor

# Run the full inference pipeline
python -m allele_correction_ml.modeling.predict
```

## Results

> To be completed with final metrics and comparison tables between the different models evaluated for the detection and correction stages.

## Tech Stack

- **Python 3.11**
- **scikit-learn** — baseline classification and regression models
- **pandas / numpy** — data manipulation
- **matplotlib / seaborn** — visualization
- **pytest** — testing
- **ruff** — linting and formatting

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

*Developed as part of a Master's Thesis in Bioinformatics, applied to canine genetic identification.*
