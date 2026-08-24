# ADSA Evidence & Reproducibility

This file separates **what the public repository directly demonstrates** from historical performance claims that require additional benchmark evidence.

## Repository-verifiable implementation evidence

At commit `4d56cba05e81d30207201a0e639fbff0ec28a3c8`, the public source code contains an autonomous/model-assisted machine-learning loop with:

- Azure OpenAI model calls for solution generation and optimization;
- Anthropic Claude calls for code repair after execution errors;
- generated Python solution execution through a subprocess boundary;
- a bounded execution timeout (`MAX_RUNTIME_MINUTES`); 
- explicit timeout recovery that asks the model to produce a faster replacement;
- error inspection and model-assisted repair;
- iterative solution refinement across a bounded iteration count;
- archiving of previous solutions and progress/result artefacts;
- `progress_report.json`, `results.csv` and execution-log outputs;
- optional GPU-aware instructions in generated ML solutions.

These are inspectable implementation properties. They are useful evidence that Atenea Labs has built autonomous/tool-using AI software, but they do not by themselves prove any particular competition percentile or general performance level.

## Historical `98%` claim

The original README and initial commit message state that ADSA had demonstrated performance exceeding 98% of data scientists in global competitions.

**Current evidence status: `HISTORICAL_CLAIM / PUBLIC_REPRODUCTION_EVIDENCE_NOT_YET_FROZEN`.**

The repository currently includes example Spaceship Titanic data, source code and whitepapers, but the current public tree does not contain a complete immutable benchmark package that independently establishes how the `98%` percentile was calculated.

Until such a package is added, external grant, funding or technical-capability materials should **not cite `98%` as a verified result**.

## Evidence required to promote the claim

A future benchmark evidence package should freeze at least:

1. exact competition/dataset and stable source/leaderboard reference;
2. train/test snapshot identity and any competition-specific data rules;
3. metric definition and exact score produced by ADSA;
4. percentile methodology: denominator/population and date of leaderboard snapshot;
5. ADSA code SHA and configuration;
6. model/provider identities and relevant inference settings;
7. Python/dependency/environment identity;
8. random seeds or documented nondeterminism controls;
9. immutable run artefacts (`solution.py`, progress report, predictions, logs);
10. independent leaderboard/result receipt or archived source supporting the percentile.

Once those artefacts exist, update this file with their immutable hashes/links and only then restore a precise percentile claim to the README.

## Appropriate external claim today

A defensible statement is:

> ADSA is a publicly released Atenea Labs implementation of an autonomous, model-assisted machine-learning loop that generates and executes candidate solutions, observes failures/runtime behaviour, requests repairs or optimizations, and persists progress/result artefacts across iterations.

## Inappropriate extrapolations

The ADSA repository should not currently be used as evidence of:

- automotive validation or OpenSCENARIO expertise;
- a verified `98%` global data-scientist percentile;
- a specific current production SLA;
- safety-critical execution controls;
- current compatibility with the latest provider model/API versions;
- customer deployment or commercial traction unless separately evidenced.

## Relationship to newer Atenea R&D

ADSA can be cited as **prior Atenea Labs autonomous/tool-using AI implementation experience**. Newer projects such as SafetyGraph have separate architecture, validation, provenance and evidence requirements and should not imply that ADSA already implemented those domain-specific capabilities.

## Licence wording

The source is publicly available under the terms in `LICENSE.md`. That file contains an MIT-style permission grant plus explicit trademark and attribution provisions. Refer to the repository licence directly rather than describing it as unmodified standard MIT unless/until the licence text is standardised.
