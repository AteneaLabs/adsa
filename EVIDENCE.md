# ADSA Evidence and Reproducibility

This file separates **capabilities visible in source code** from **performance claims that require a reproducible benchmark receipt**.

## Source-backed capabilities

At `main` commit `4d56cba05e81d30207201a0e639fbff0ec28a3c8`, the public implementation contains:

- iterative candidate-solution generation through Azure OpenAI;
- local execution of generated Python under a timeout;
- feedback from prior `progress_report.json` metrics into subsequent iterations;
- Anthropic Claude repair when generated code raises recognized errors;
- a timeout-optimization path;
- archival of previous solutions, progress reports and results;
- execution logs and explicit iteration/runtime limits.

These are implementation facts that can be inspected directly in `adsa.py`. They do not imply a particular benchmark score, leaderboard position, safety guarantee or production readiness.

## Benchmark claims

A benchmark claim is considered reproducible only when the repository or a stable linked archive records at least:

```yaml
benchmark_id:
dataset_or_competition:
competition_or_dataset_version:
metric:
comparison_population_definition:
code_sha:
python_environment:
model_provider_and_model_ids:
provider_configuration:
prompt_or_problem_spec_hash:
train_validation_protocol:
random_seeds_or_repeat_protocol:
runtime_budget:
hardware:
raw_run_artifact_hashes: []
result:
public_leaderboard_reference: null
verification_date:
```

Claims such as a percentile relative to data scientists/competition participants additionally require the comparison population and calculation method to be reproducible.

## Current public evidence status

The repository contains source code, example data/problem configuration and ADSA whitepapers. At the time this evidence policy was added, there is **no standalone immutable benchmark receipt in the repository that is sufficient by itself to reproduce a global “top X% of data scientists” claim**.

Therefore the README intentionally describes the system's source-backed capabilities without publishing that percentile as an established result.

This does not assert that earlier experiments did not occur. It only keeps public claims aligned with the evidence currently committed and independently inspectable.

## How to restore a quantitative claim

Add a versioned benchmark package containing the evidence contract above, ideally including:

- immutable code SHA;
- sanitized run configuration;
- raw progress/result artifacts or hashes;
- exact metric computation;
- external/public leaderboard evidence when applicable;
- a short reproduction command or notebook/script;
- limitations and whether the result is single-run or repeated.

Then update this file and the README with the exact scoped result rather than a broader marketing generalization.
