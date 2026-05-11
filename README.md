# Trace Wing Agent v0.2

Trace Wing Agent v0.2 is a protocol-driven provenance inference agent for Multi-Wing systems.  
It infers structural lineage, proposes attribution, and emits trace claims for downstream review, dispute, and value-routing layers.  
A trace claim is a structured inference artifact, not a legal verdict.

---

## Overview

**Trace Wing** is an agent designed to analyze the structural lineage of documents, posts, specifications, and logs.

Instead of focusing only on surface wording, it compares:

- semantic patterns
- structural composition
- cyclical logic
- protocol-like design motifs

Its primary purpose is to generate a **trace claim**: a structured output describing likely origin candidates, lineage type, confidence, evidence bundle, and policy outcome.

This repository defines the minimum portable specification for that behavior.

---

## What this repository contains

This repository currently includes:

- the core agent specification for Trace Wing
- a JSON Schema for validating the agent spec itself
- two JSON Schemas for validating emitted trace claim artifacts
- example trace claim artifacts for both v0.1 and v0.2
- a GitHub Actions workflow for automated validation

---

## Design goals

Trace Wing is designed around the following principles:

- **Structure over surface**  
  The system should compare structural composition, not just wording.

- **Inference before enforcement**  
  Trace Wing proposes lineage and attribution; it does not directly punish, accuse, or execute sanctions.

- **Evidence before assertion**  
  Every claim should be backed by observable fields and score breakdowns.

- **Human review for high-impact outcomes**  
  High-confidence or high-impact cases should pass through review.

- **Separation of inference and value execution**  
  Attribution inference, royalty calculation, dispute handling, and legal interpretation belong to different layers.

---

## Non-goals

This repository does **not** define:

- automatic legal infringement judgment
- automatic truth verification
- automatic public accusation
- automatic penalty execution
- full payment logic for Royalty OS

Trace Wing is an inference layer, not a sovereign judge.

---

## Repository Structure

```text
.
├─ spec/
│  └─ trace-wing-agent-v0.1.yaml
├─ schemas/
│  ├─ trace-wing-agent-v0.1.schema.json
│  ├─ trace-claim-v0.1.schema.json
│  └─ trace-claim-v0.2.schema.json
├─ examples/
│  ├─ trace-claim.sample.yaml
│  └─ trace-claim-v0.2.sample.yaml
└─ .github/
   └─ workflows/
      └─ validate-specs.yml
```

### Structure notes

- `spec/trace-wing-agent-v0.1.yaml`  
  Core agent specification for Trace Wing.

- `schemas/trace-wing-agent-v0.1.schema.json`  
  Schema used to validate the Trace Wing spec itself.

- `schemas/trace-claim-v0.1.schema.json`  
  Baseline schema for the original trace claim output contract.

- `schemas/trace-claim-v0.2.schema.json`  
  Extended trace claim schema introducing `claim_scope` for operational scope clarity.

- `examples/trace-claim.sample.yaml`  
  Example artifact for `trace-claim-v0.1`.

- `examples/trace-claim-v0.2.sample.yaml`  
  Example artifact for `trace-claim-v0.2`.

- `.github/workflows/validate-specs.yml`  
  Validation workflow for the spec and both trace claim versions.

---

## Start Here

Read the files in this order:

1. **`spec/trace-wing-agent-v0.1.yaml`**  
   The main protocol specification for the Trace Wing agent.

2. **`schemas/trace-wing-agent-v0.1.schema.json`**  
   The schema used to validate the spec file itself.

3. **`schemas/trace-claim-v0.1.schema.json`**  
   The baseline output schema for the original trace claim contract.

4. **`examples/trace-claim.sample.yaml`**  
   A minimal example of a valid `trace-claim-v0.1` artifact.

5. **`schemas/trace-claim-v0.2.schema.json`**  
   The extended output schema introducing `claim_scope`.

6. **`examples/trace-claim-v0.2.sample.yaml`**  
   A valid example of `trace-claim-v0.2`, showing how operational scope is expressed.

7. **`.github/workflows/validate-specs.yml`**  
   Automated validation for the spec and both trace claim versions.

Suggested reading path:

- start with the agent spec
- confirm the spec shape through its schema
- read the baseline claim contract
- compare the extended claim contract in v0.2
- inspect the examples
- check CI validation last

---

## Core files

### `spec/trace-wing-agent-v0.1.yaml`

Defines the Trace Wing agent itself, including:

- identity
- runtime assumptions
- input model
- processing pipeline
- fingerprint model
- lineage model
- policy thresholds
- Multi-Wing integration points
- observability and safeguards

This is the conceptual and operational center of the repository.

---

### `schemas/trace-wing-agent-v0.1.schema.json`

Validates the structure of the spec file.

This ensures that the Trace Wing specification remains machine-checkable and stable across revisions.

It verifies, among other things:

- required top-level sections
- allowed enums and object shapes
- scoring model structure
- policy threshold fields
- integration definitions

---

### `schemas/trace-claim-v0.1.schema.json`

Validates the **baseline trace claim** artifact emitted by the agent.

A valid `trace-claim-v0.1` includes fields such as:

- `claim_id`
- `generated_at`
- `engine`
- `target_artifact`
- `classification`
- `confidence`
- `origin_candidate`
- `evidence`
- `policy_result`
- `review`
- `audit`

This schema defines the original minimal output contract for downstream systems.

---

### `examples/trace-claim.sample.yaml`

Provides a concrete example of a valid `trace-claim-v0.1`.

It demonstrates:

- how lineage classification is represented
- how evidence fields are structured
- how policy outputs are encoded
- how review and audit metadata are attached

This file is validated in CI against `schemas/trace-claim-v0.1.schema.json`.

---

### `schemas/trace-claim-v0.2.schema.json`

Validates the **extended trace claim** artifact emitted by the agent.

`trace-claim-v0.2` preserves the baseline structure while introducing:

- `claim_scope`

This field clarifies the operational scope of a trace claim, such as whether it is limited to lineage inference, attribution suggestion, royalty assessment readiness, or dispute preparation.

This schema is intended for downstream systems that require more explicit governance semantics.

---

### `examples/trace-claim-v0.2.sample.yaml`

Provides a concrete example of a valid `trace-claim-v0.2`.

It demonstrates:

- all baseline fields from v0.1
- explicit `claim_scope`
- clearer downstream routing intent
- a more governance-aware output contract

This file is validated in CI against `schemas/trace-claim-v0.2.schema.json`.

---

## Processing model

Trace Wing operates as a staged provenance inference pipeline.

Typical state progression:

```text
OBSERVED
→ NORMALIZED
→ PARSED
→ FINGERPRINTED
→ CANDIDATE_LINKED
→ SCORED
→ CLASSIFIED
→ ATTRIBUTION_SUGGESTED / HUMAN_REVIEW / ROYALTY_ELIGIBLE / DISPUTED / ARCHIVED
```

The agent is designed to emit **structured claims**, not rhetorical conclusions.

---

## Multi-Wing integration

Trace Wing is intended to run inside a broader Multi-Wing architecture.

Typical integration targets:

- **Log-Wing**  
  For observation records, snapshots, and timestamped evidence.

- **Logic-Wing**  
  For policy interpretation, classification review, and high-risk reasoning.

- **Royalty-Wing**  
  For contribution routing and royalty assessment requests.

- **Dispute Registry**  
  For objections, re-evaluation, and audit history.

- **Existence Proof / provenance layer**  
  For author, publication, and timing attestation.

Trace Wing should be understood as a **lineage inference wing**, not a standalone civilization stack.

---

## Schema Usage

This repository currently uses:

- **1 agent specification**
- **1 spec schema**
- **2 trace claim schemas**
- **2 example trace claim artifacts**

The repository validates both the Trace Wing spec and the emitted trace claim formats across versioned output contracts.

---

### 1. Validate the Trace Wing specification

The file:

- `spec/trace-wing-agent-v0.1.yaml`

is validated against:

- `schemas/trace-wing-agent-v0.1.schema.json`

This ensures that the Trace Wing agent specification remains machine-checkable and structurally stable.

---

### 2. Validate the original trace claim contract

The file:

- `examples/trace-claim.sample.yaml`

is validated against:

- `schemas/trace-claim-v0.1.schema.json`

This preserves the minimal baseline output contract for Trace Wing claims.

`trace-claim-v0.1` is the original schema version and does **not** include `claim_scope`.

---

### 3. Validate the extended trace claim contract

The file:

- `examples/trace-claim-v0.2.sample.yaml`

is validated against:

- `schemas/trace-claim-v0.2.schema.json`

This extended contract introduces:

- `claim_scope`

The purpose of `claim_scope` is to clarify the operational scope of a trace claim, such as whether it is limited to lineage inference, attribution suggestion, royalty assessment readiness, or dispute preparation.

---

### Version positioning

- **`trace-claim-v0.1`**  
  Minimal baseline trace claim contract.

- **`trace-claim-v0.2`**  
  Extended trace claim contract with `claim_scope` added to clarify downstream operational meaning.

This preserves backward clarity while allowing governance-oriented expansion.

---

### Local validation example

Install dependencies:

```bash
pip install pyyaml jsonschema
```

Validate the spec, both schemas, and both example artifacts locally:

```bash
python - <<'PY'
import json
from pathlib import Path
import yaml
from jsonschema import Draft202012Validator

spec_path = Path("spec/trace-wing-agent-v0.1.yaml")
spec_schema_path = Path("schemas/trace-wing-agent-v0.1.schema.json")

claim_v01_schema_path = Path("schemas/trace-claim-v0.1.schema.json")
claim_v02_schema_path = Path("schemas/trace-claim-v0.2.schema.json")

sample_v01_path = Path("examples/trace-claim.sample.yaml")
sample_v02_path = Path("examples/trace-claim-v0.2.sample.yaml")

with spec_schema_path.open("r", encoding="utf-8") as f:
    spec_schema = json.load(f)

with claim_v01_schema_path.open("r", encoding="utf-8") as f:
    claim_v01_schema = json.load(f)

with claim_v02_schema_path.open("r", encoding="utf-8") as f:
    claim_v02_schema = json.load(f)

with spec_path.open("r", encoding="utf-8") as f:
    spec_data = yaml.safe_load(f)

with sample_v01_path.open("r", encoding="utf-8") as f:
    sample_v01_data = yaml.safe_load(f)

with sample_v02_path.open("r", encoding="utf-8") as f:
    sample_v02_data = yaml.safe_load(f)

Draft202012Validator.check_schema(spec_schema)
Draft202012Validator.check_schema(claim_v01_schema)
Draft202012Validator.check_schema(claim_v02_schema)

Draft202012Validator(spec_schema).validate(spec_data)
Draft202012Validator(claim_v01_schema).validate(sample_v01_data)
Draft202012Validator(claim_v02_schema).validate(sample_v02_data)

print("All local validations passed.")
PY
```

---

### CI validation

GitHub Actions automatically validates:

- presence of required files
- YAML syntax of the Trace Wing spec
- JSON syntax and structural validity of:
  - `trace-wing-agent-v0.1.schema.json`
  - `trace-claim-v0.1.schema.json`
  - `trace-claim-v0.2.schema.json`
- YAML syntax of both example claim files
- schema compliance of the spec
- schema compliance of both trace claim samples

Workflow file:

- `.github/workflows/validate-specs.yml`

---

### Output contract guidance

A `trace_claim` is a structured inference artifact, not a legal verdict.

Use version selection according to downstream needs:

- choose **v0.1** when a minimal baseline claim is sufficient
- choose **v0.2** when operational scope must be explicit through `claim_scope`

This keeps inference portable while allowing gradual governance expansion.

---

## Output contract

The primary machine output of Trace Wing is a `trace_claim`.

This claim is intended to be:

- auditable
- reviewable
- disputable
- portable across systems

A trace claim is not equivalent to a legal verdict.  
It is a structured inference artifact.

---

## Recommended usage pattern

A practical deployment flow looks like this:

1. observe a target artifact
2. normalize and parse structure
3. generate multi-layer fingerprints
4. retrieve lineage candidates
5. compute confidence and novelty
6. emit a `trace_claim`
7. route the result to:
   - attribution suggestion,
   - human review,
   - royalty assessment request,
   - or dispute preparation

This separation keeps the repository modular and governance-friendly.

---

## Safety posture

Trace Wing should never be used as an automatic accusation engine.

Recommended safeguards include:

- no automatic public accusation
- no automatic legal conclusion
- no silent penalty execution
- human review for high-impact claims
- preserved dispute channel
- full policy logging

The stronger the inference engine becomes, the more important restraint becomes.

---

## Versioning

Current draft set:

- **Agent spec:** `trace-wing-agent-v0.1`
- **Baseline claim schema:** `trace-claim-v0.1`
- **Extended claim schema:** `trace-claim-v0.2`

Suggested versioning approach:

- increment patch version for wording or non-breaking clarification
- increment minor version for additive fields
- increment major version for breaking structural changes

---

## Future extensions

Planned directions include:

- signed trace claim support
- federation across multiple Memory Galaxy nodes
- bridges to Signed Impact Attestation
- automatic citation suggestion
- false-positive reduction loops
- richer lineage graphs and mutation trees

---

## Contributing

Contributions should preserve the following properties:

- machine-validatable structure
- clean separation between inference and enforcement
- explicit policy boundaries
- strong auditability
- compatibility with Multi-Wing style integration

For substantial changes, update:

- the spec
- relevant schema files
- example artifacts
- the validation workflow

together, not separately.

---

## License

Choose a license appropriate to your intended governance model.

For open specification publishing, permissive licenses are often suitable for the schema and documentation layer.  
For controlled ecosystem use, additional governance documents may be appropriate.

---

## Summary

Trace Wing Agent v0.1 defines a portable provenance inference layer for Multi-Wing systems.

It is built to answer questions like:

- What structure is present here?
- Which lineage does it most likely belong to?
- How strong is that inference?
- What action is appropriate next?

It is not designed to shout.  
It is designed to trace.
