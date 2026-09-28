# Model Card: Evidence Verification Model (Model 1)

## Model Purpose
Evaluates extracted features from faculty evidence to determine if the evidence is verified, requires manual review, or is suspicious.

## Model Type
Classification Model (Scikit-learn pipeline/classifier).

## Input Features
Exactly nine numeric features, in this precise order:
1. `has_identifier` (0/1)
2. `identifier_resolves` (0/1)
3. `has_issuer` (0/1)
4. `has_recipient_name` (0/1)
5. `has_issue_date` (0/1)
6. `external_record_found` (0/1)
7. `title_match_score` (0.0 - 1.0)
8. `name_match_score` (0.0 - 1.0)
9. `organization_match_score` (0.0 - 1.0)

## Output Labels
*   `VERIFIED` (0)
*   `SUSPICIOUS` (1)
*   `REQUIRES_REVIEW` (2)

## Training Dataset Description
Trained on a small, synthetic/prototype dataset mimicking extracted structural metadata of faculty documents. 

## Current Prototype Accuracy
100.00% accuracy on the current prototype dataset.

## Limitations
*   The current training data is small and synthetic.
*   100% prototype accuracy does not establish production-ready performance.
*   Real-world validation with a larger labelled dataset is absolutely required.
*   Model 1 should not be treated as a final autonomous document-verification system.

## Known Prototype Defaults
Prototype defaults currently exist for unavailable external-verification features, as external web verification is not fully implemented in the parser yet.

## Known Risks
Without large-scale real-world data, the model may overfit to the synthetic structural patterns of the prototype dataset. Relying on it autonomously in production could lead to false positives (awarding credit for suspicious evidence) or false negatives (flagging valid evidence).

## Intended Use
To act as a gatekeeper in the Faculty Performance/Professional Information pipeline, determining if parsed evidence is structurally sound enough to be scored by Model 2.

## Non-Intended Use
Not intended for autonomous, unreviewed academic credit attribution in a production environment without further training and validation.

## Reproducibility Information
Trained with scikit-learn 1.6.1. The `verification_model.pkl` artifact contains all necessary preprocessing pipelines and the trained estimator.
