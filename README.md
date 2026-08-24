# ADSA — Autonomous Data Scientist Agent

<div align="center">
  <img src="atenea-icono.svg" alt="Atenea Labs Logo" width="150"/>

**Atenea Labs Research**

Autonomous, model-assisted machine-learning experimentation.
</div>

---

## What ADSA is

ADSA is a publicly released Atenea Labs research implementation of an autonomous machine-learning loop. It uses language models to propose ML solutions, executes generated Python code, observes runtime/errors and progress, requests repairs or optimizations, and iterates while persisting results.

The repository is useful as inspectable evidence of **autonomous/tool-using AI engineering**. It is a 2025 research codebase, not a claim that every provider model/API or dependency remains current in 2026.

## What the code directly demonstrates

At the original implementation commit, ADSA contains:

- Azure OpenAI calls for candidate solution generation and optimization;
- Anthropic Claude calls for repair of failed generated code;
- generated Python execution through a subprocess boundary;
- bounded execution timeouts;
- timeout-aware optimization requests;
- runtime/error feedback into later iterations;
- iterative solution replacement and archiving;
- progress, prediction and execution-log artifacts;
- instructions for GPU-aware generated ML solutions.

See [`EVIDENCE.md`](EVIDENCE.md) for the exact evidence boundary and reproducibility requirements.

## Historical performance claim

The original project description stated that ADSA had outperformed **98% of data scientists in global competitions**. The current public repository does not yet contain a complete immutable leaderboard/benchmark package sufficient to independently reproduce that percentile.

For that reason, this README does **not** present the 98% figure as a verified current result. `EVIDENCE.md` lists the artifacts required to promote the historical claim back to a reproducible benchmark result.

## Architecture

```text
problem specification + sample data
             |
             v
   model-generated ML solution
             |
             v
      local code execution
             |
     +-------+--------+
     |                |
  success          error/timeout
     |                |
metrics/results   repair/optimization
     |                |
     +-------+--------+
             |
        next iteration
             |
             v
 archived solutions + progress + results
```

The implementation is intentionally simple and research-oriented: the main orchestration loop currently lives in `adsa.py`.

## Important execution-safety note

**ADSA executes model-generated Python code.**

Do not run it with sensitive credentials, private datasets, production infrastructure access, or broad filesystem/network permissions unless you first provide an appropriate sandbox and policy boundary. Generated code may install packages or perform actions not suitable for an unrestricted production host.

This repository should be treated as research software, not a hardened arbitrary-code-execution sandbox.

## Repository contents

- `adsa.py` — autonomous generation/execution/recovery loop.
- `problem_info.md` — example task specification.
- `train.csv` / `test.csv` — example Spaceship Titanic data included for experimentation.
- `ADSA_Whitepaper_EN.pdf` / `ADSA_Whitepaper_ES.pdf` — original project whitepapers.
- `EVIDENCE.md` — claim/evidence and reproducibility ledger.
- `LICENSE.md` — repository licence terms.

## Requirements

The historical implementation uses Python and provider APIs including Azure OpenAI and Anthropic Claude. Model identifiers and APIs in the source reflect the implementation period and may require updating before a new run.

Install the pinned/current repository dependencies with:

```bash
pip install -r requirements.txt
```

Create local configuration from the example:

```bash
cp .env.example .env
```

Then provide the relevant provider credentials in your local environment. Never commit API keys.

## Problem specification

ADSA expects a `problem_info.md` describing the ML task. A useful specification includes:

```markdown
# Problem Description

## Objective
What must be predicted/classified/regressed.

## Data Description
- training file
- test file
- target variable
- important feature/context notes

## Evaluation Metric
The metric used to compare candidate solutions.

## Constraints
- runtime
- memory
- any domain restrictions

## Expected Output Format
Required prediction/result columns and types.
```

## Running the research implementation

Place the expected training/test inputs and problem specification in the repository working directory, configure provider credentials, and run:

```bash
python adsa.py
```

Typical outputs include:

- `solution.py` — current generated candidate solution;
- `progress_report.json` — model-reported/solution-reported progress and metrics;
- `results.csv` — generated predictions/results;
- `execution_logs.txt` — execution output;
- `older_solutions/` — archived prior iterations.

## Reproducibility

A future benchmark-quality ADSA run should freeze at least:

- code SHA;
- dataset snapshot and task/competition identity;
- provider/model versions and relevant generation settings;
- Python/dependency environment;
- metric definition;
- random seeds/nondeterminism policy;
- generated solution and progress/result artifacts;
- independent leaderboard/result receipt when a percentile claim is made.

See [`EVIDENCE.md`](EVIDENCE.md).

## Relationship to newer Atenea Labs R&D

ADSA is legitimate prior evidence that Atenea Labs has built autonomous/model-assisted software that can generate, execute, observe and repair code-driven ML work.

It should **not** be used to imply prior automotive validation, OpenSCENARIO, safety-critical control or SafetyGraph-specific capabilities. New projects must establish those capabilities independently.

## Licence

The source is publicly available under the terms in [`LICENSE.md`](LICENSE.md). The current licence contains an MIT-style permission grant plus explicit attribution and trademark provisions; consult the actual licence text for reuse conditions.

## Contact

- Atenea Labs: https://atenealabs.com
- Research site referenced by the original project: https://adsa.atenea.dev
- GitHub organization: https://github.com/AteneaLabs

---

## Resumen en español

ADSA es una implementación pública de investigación de Atenea Labs para automatizar un ciclo de experimentación de machine learning mediante modelos de IA: genera soluciones, ejecuta código, observa errores/tiempos de ejecución, solicita correcciones u optimizaciones y conserva artefactos de progreso y resultados.

El código demuestra experiencia real en sistemas autónomos/tool-using AI, pero **no utilizamos actualmente como hecho verificado el claim histórico de superar al 98% de data scientists**, porque el repositorio público todavía no contiene el paquete inmutable de benchmark/leaderboard necesario para reproducir ese percentil. Consulta [`EVIDENCE.md`](EVIDENCE.md).

**Importante:** ADSA ejecuta Python generado por modelos. Debe utilizarse en un entorno controlado/sandbox si existen datos sensibles, credenciales o acceso a infraestructura relevante.
