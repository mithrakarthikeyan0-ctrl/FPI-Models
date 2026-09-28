# FPI Models

This repository contains the AI/model layer of the Faculty Performance/Professional Information (FPI) project.

## Project Purpose
The FPI project automates the extraction, verification, and scoring of faculty evidence to provide standardized appraisal credit. This specific repository hosts the machine learning models responsible for these tasks.

## Current Status
*   **COMPLETED**: Model 1 (Evidence Verification) prototype is trained, evaluated, and saved.
*   **PLANNED**: Model 2 (Appraisal Scoring Engine) is planned but not implemented yet. Do not expect Model 2 to exist in this repository.

## Architecture
See [docs/MODEL_ARCHITECTURE.md](docs/MODEL_ARCHITECTURE.md) for a detailed diagram of the two-model flow.

## Repository Structure
```
FPI-Models/
├── model1/
│   ├── verification_model.pkl
│   ├── README.md
│   └── MODEL_CARD.md
├── model2/
│   └── README.md
├── docs/
│   └── MODEL_ARCHITECTURE.md
├── requirements.txt
├── .gitignore
└── README.md
```

## Installation
To load and run inference with Model 1, create a virtual environment and install the requirements:

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Inference Example (Model 1)
```python
import joblib

model_data = joblib.load("model1/verification_model.pkl")
model = model_data["model"]

# [has_identifier, identifier_resolves, has_issuer, has_recipient_name, has_issue_date, external_record_found, title_match_score, name_match_score, organization_match_score]
sample = [[1, 1, 1, 1, 1, 1, 1.0, 1.0, 1.0]]
print(model.predict(sample))
```

## Limitations
Model 1 is currently a prototype trained on a small, synthetic dataset. Its 100% prototype accuracy does not reflect real-world, production-level performance. External web verification is not fully integrated into the data generation pipeline. Real-world validation with a large, manually labelled dataset is required.

## Development Roadmap
1. Gather and label real-world faculty evidence dataset.
2. Retrain and evaluate Model 1 on real-world dataset.
3. Build and train Model 2 (Appraisal Scoring Engine).
