# Trace Claim v0.2

Trace Claim v0.2 is a versioned output contract for provenance inference in Multi-Wing environments.  
It defines a machine-readable claim format for structural lineage, attribution suggestion, and governance-aware routing.  
A trace claim is a structured inference artifact, not a legal verdict.

---

## Overview

This repository publishes the **Trace Claim v0.2** contract as a lightweight, validation-ready package.

It currently includes:

- the JSON Schema for `trace-claim-v0.2`
- a sample YAML artifact validated against that schema
- a GitHub Actions workflow for automated validation
- repository documentation and license metadata

This repository is intentionally minimal.

It does **not** currently publish the full Trace Wing agent specification.  
Instead, it focuses on the portable output contract that downstream systems can consume.

In other words:

- **Trace Wing Agent** may generate trace claims
- **this repository** defines and validates the **claim artifact format**

---

## Purpose

The purpose of `trace_claim` is to carry structured provenance inference results across systems.

A trace claim can express:

- likely origin candidates
- lineage classification
- confidence level
- evidence bundle
- policy outcome
- operational scope

This allows downstream systems to interpret provenance results in a controlled and auditable way.

Typical downstream consumers include:

- review workflows
- governance layers
- dispute preparation layers
- royalty assessment layers
- archival or provenance registries

---

## Why v0.2 exists

`trace-claim-v0.2` extends the baseline trace claim model by introducing:

- `claim_scope`

This field clarifies the intended operational scope of a claim.

Examples include:

- `structural_lineage_only`
- `attribution_suggestion_only`
- `royalty_assessment_ready`
- `dispute_ready`

This makes the contract more useful for governance-oriented routing without collapsing inference into enforcement.

---

## Design posture

Trace Claim v0.2 follows these principles:

- **Structure over surface**  
  The claim should describe structural lineage rather than shallow wording similarity alone.

- **Inference before enforcement**  
  A trace claim may support review or routing, but it is not itself a verdict.

- **Evidence before assertion**  
  Claims should carry observable evidence fields.

- **Operational scope must be explicit**  
  The meaning of a claim should be bounded through `claim_scope`.

- **Governance compatibility**  
  The contract should be easy to connect to review, dispute, attribution, and value-routing systems.

---

## Non-goals

This repository does **not** define:

- the full Trace Wing agent runtime
- a legal infringement decision engine
- a truth-verification engine
- automatic accusation logic
- automatic penalty execution
- a complete royalty settlement system

This repository defines an **output contract**, not a complete civilization stack.

---

## Repository Structure

```text
.
├─ schemas/
│  └─ trace-claim-v0.2.schema.json
├─ examples/
│  └─ trace-claim-v0.2.sample.yaml
└─ .github/
   └─ workflows/
      └─ validate-specs.yml

LICENSE
README.md
Structure notes
schemas/trace-claim-v0.2.schema.json
The JSON Schema for the Trace Claim v0.2 contract.
examples/trace-claim-v0.2.sample.yaml
A sample artifact showing a valid trace_claim instance.
.github/workflows/validate-specs.yml
Automated validation for the schema and the sample.
README.md
Repository documentation.
LICENSE
License metadata for the repository.
Start Here

Read the files in this order:

schemas/trace-claim-v0.2.schema.json
The machine-readable definition of the claim contract.
examples/trace-claim-v0.2.sample.yaml
A valid example showing how the contract is instantiated.
.github/workflows/validate-specs.yml
The CI workflow that validates the schema and the sample.

This order gives the clearest path:

first understand the contract
then inspect a concrete instance
then confirm how validation is enforced
Core files
schemas/trace-claim-v0.2.schema.json

This is the primary contract file in the repository.

It defines the required structure of a trace_claim, including fields such as:

schema_version
claim_id
generated_at
engine
target_artifact
classification
claim_scope
confidence
origin_candidate
evidence
policy_result
review
audit

This schema is intended to act as a stable machine-readable contract for downstream provenance-aware systems.

examples/trace-claim-v0.2.sample.yaml

This file demonstrates a valid trace claim instance.

It shows:

how a target artifact is described
how lineage type and novelty are represented
how claim_scope is expressed
how evidence is bundled
how policy and review status are attached
how audit metadata is recorded

This sample is validated in CI against the schema.

.github/workflows/validate-specs.yml

This workflow ensures that the repository stays consistent.

It validates:

presence of required files
JSON syntax of the schema
YAML syntax of the sample
JSON Schema correctness
schema compliance of the sample artifact

This makes the repository lightweight but still trustworthy.

Contract summary

The primary object defined by this repository is:

trace_claim

A trace claim is a portable structured inference artifact.

It is designed to answer questions such as:

What artifact is being evaluated?
What lineage type was inferred?
Which origin candidate is most likely?
How strong is the inference?
What evidence supports it?
What operational scope does this claim have?
What downstream action is appropriate?
claim_scope

The most important addition in v0.2 is:

claim_scope

This field makes the contract more explicit for downstream handling.

Supported values are:

structural_lineage_only
attribution_suggestion_only
royalty_assessment_ready
dispute_ready
Meaning
structural_lineage_only
The claim is limited to lineage inference.
attribution_suggestion_only
The claim is suitable for attribution-oriented handling, but not yet for stronger routing.
royalty_assessment_ready
The claim is mature enough to be passed to a royalty or contribution assessment layer.
dispute_ready
The claim is suitable for dispute preparation or contested review contexts.

This field does not turn the claim into enforcement.
It only clarifies how the claim may be used.

Schema Usage

This repository currently uses:

1 trace claim schema
1 example trace claim artifact
1 CI validation workflow
Validate the trace claim contract

The file:

examples/trace-claim-v0.2.sample.yaml

is validated against:

schemas/trace-claim-v0.2.schema.json

This ensures that the published example remains structurally valid and machine-readable.

Local validation example

Install dependencies:

pip install pyyaml jsonschema

Validate the schema and sample locally:

python - <<'PY'
import json
from pathlib import Path
import yaml
from jsonschema import Draft202012Validator

schema_path = Path("schemas/trace-claim-v0.2.schema.json")
sample_path = Path("examples/trace-claim-v0.2.sample.yaml")

with schema_path.open("r", encoding="utf-8") as f:
    schema = json.load(f)

with sample_path.open("r", encoding="utf-8") as f:
    sample = yaml.safe_load(f)

Draft202012Validator.check_schema(schema)
Draft202012Validator(schema).validate(sample)

print("All local validations passed.")
PY
CI validation

GitHub Actions automatically validates:

presence of the required schema file
presence of the required sample file
JSON syntax of the schema
YAML syntax of the sample
JSON Schema validity
schema compliance of the sample artifact

Workflow file:

.github/workflows/validate-specs.yml
Output contract guidance

A trace_claim is a structured inference artifact, not a legal verdict.

This distinction matters.

The contract is designed to support:

review
attribution suggestion
governance-aware routing
dispute preparation
royalty assessment preparation

It is not designed to function as an automatic judgment engine.

Recommended usage pattern

A practical usage flow looks like this:

a provenance inference system analyzes an artifact
it emits a trace_claim
downstream systems inspect:
lineage type
confidence
evidence
claim scope
policy result
the claim is routed to:
archive,
review,
attribution suggestion,
royalty assessment,
or dispute handling

This separation keeps the contract reusable across multiple governance contexts.

Positioning

This repository should be understood as a contract repository, not a full agent repository.

A useful mental model is:

Trace Wing Agent = the inference-producing system
Trace Claim v0.2 = the output contract emitted by such a system
this repository = the validation-ready publication of that contract

So even if the broader architecture grows later, this repository already has a clear role:
it defines the shape of the claim packet.

Safety posture

This repository should not be interpreted as support for automatic accusation systems.

Recommended safeguards for systems consuming this contract include:

no automatic public accusation
no automatic legal conclusion
no silent penalty execution
human review for high-impact usage
dispute channels for contested cases
transparent logging of downstream policy decisions

The contract becomes stronger when its limits are explicit.

Versioning

Current published contract:

Trace Claim: trace-claim-v0.2

Suggested versioning logic:

increment patch version for wording or non-breaking clarification
increment minor version for additive fields
increment major version for breaking structural changes

Because claim_scope changes the operational interpretation of the claim, it is correctly introduced as a new versioned contract rather than a silent edit.

Future extensions

Possible next steps include:

adding score_breakdown
adding weight_profile_id
adding counter_evidence_summary
publishing a baseline trace-claim-v0.1 side by side
publishing a full Trace Wing agent spec in a separate or expanded repository
bridging to Signed Impact Attestation or dispute-oriented registries

This lightweight structure is intentionally compatible with future expansion.

Contributing

Contributions should preserve the following properties:

machine-validatable structure
explicit operational boundaries
auditability
portability across downstream systems
clear separation between inference and enforcement

For any structural change, update:

the schema
the example artifact
the validation workflow
the documentation

together, not separately.

License

See LICENSE for repository licensing terms.

If this contract is later embedded into a larger governance stack, additional policy documents may be added outside this repository.

Summary

Trace Claim v0.2 defines a lightweight, versioned output contract for provenance inference systems.

It is built to carry:

structural lineage
attribution-oriented inference
explicit operational scope
evidence bundles
governance-aware routing intent

It does not judge.
It does not accuse.
It makes structured tracing portable.
