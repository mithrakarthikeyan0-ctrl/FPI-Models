# Model 1 — Evidence Verification

## Purpose
Model 1 evaluates extracted faculty evidence and predicts whether the evidence is verified, requires manual review, or is suspicious.

## Input
Exactly nine numeric features, in this precise order:
1. `has_identifier` (Binary 0/1): Does the evidence have a standard identifier (e.g., DOI, ISSN)?
2. `identifier_resolves` (Binary 0/1): Could the identifier be successfully resolved/verified externally?
3. `has_issuer` (Binary 0/1): Is there an issuing organization specified?
4. `has_recipient_name` (Binary 0/1): Is the faculty member's name clearly on the evidence?
5. `has_issue_date` (Binary 0/1): Is there a valid issue date?
6. `external_record_found` (Binary 0/1): Was an external validation record found online?
7. `title_match_score` (Score 0.0-1.0): Similarity score between claimed title and evidence title.
8. `name_match_score` (Score 0.0-1.0): Similarity score between faculty name and evidence name.
9. `organization_match_score` (Score 0.0-1.0): Similarity score between claimed organization and evidence organization.

The pickled artifact contains the trained pipeline and metadata, so feature order is fixed.

## Output
*   **VERIFIED**: Evidence can proceed to Model 2 scoring.
*   **SUSPICIOUS**: Evidence must not automatically receive credit.
*   **REQUIRES_REVIEW**: Evidence must be manually reviewed before credit is awarded.

## Python Inference Example

```python
import joblib

# Load the model
model_data = joblib.load("verification_model.pkl")
model = model_data["model"]

# Example feature vector (matches the order specified above)
# [has_identifier, identifier_resolves, has_issuer, has_recipient_name, has_issue_date, external_record_found, title_match_score, name_match_score, organization_match_score]
sample_features = [[1, 1, 1, 1, 1, 1, 1.0, 1.0, 1.0]]

# Predict
prediction = model.predict(sample_features)
probabilities = model.predict_proba(sample_features)

print(f"Prediction: {prediction[0]}")
print(f"Probabilities: {probabilities[0]}")
```
