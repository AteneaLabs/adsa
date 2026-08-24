# ADSA — Autonomous Data Scientist Agent

<div align="center">
  <img src="atenea-icono.svg" alt="Atenea Labs Logo" width="150"/>

**Atenea Labs Research**

Autonomous iterative ML solution generation, execution, repair and optimization.

**[English](#english) · [Español](#español)**
</div>

---

<a name="english"></a>

# English

## What ADSA is

ADSA is an **open-source research prototype** from Atenea Labs for autonomous data-science workflows. Given a tabular ML problem, it can generate candidate Python solutions, execute them, inspect results/errors, request repairs or performance improvements from AI models, and iterate while preserving previous solutions and progress reports.

The repository demonstrates a real autonomous execution loop. It should be evaluated from its source code and reproducible runs rather than from unsupported leaderboard or percentile claims.

> **Evidence policy:** benchmark/performance claims are only considered verified when the repository contains or links an immutable evidence receipt describing the dataset, metric, code version, model/provider configuration and result. See [`EVIDENCE.md`](EVIDENCE.md).

## What the current code demonstrates

At the current `main` implementation, ADSA includes:

- **Iterative ML solution generation** using Azure OpenAI.
- **Execution feedback loops** that feed previous metrics/results into the next iteration.
- **Automatic repair** using Anthropic Claude when generated Python fails.
- **Timeout handling and performance recovery** for solutions that exceed a configurable runtime budget.
- **Solution history** through archived code, results and `progress_report.json` artifacts.
- **GPU-aware prompting** so generated solutions can use acceleration when available.
- **Provider separation** between solution generation and repair/optimization paths.

ADSA is a research prototype, not a production AutoML service or a safety sandbox.

## Architecture

```text
problem_info.md + train.csv/test.csv
            |
            v
   solution-generation model
            |
            v
      generated Python
            |
            v
  bounded-time local execution
       |              |
       | success      | error/timeout
       v              v
 progress/results   repair or optimization model
       |              |
       +------ feedback+
              |
              v
         next iteration
```

The loop is intentionally simple and inspectable. Generated solutions, progress reports and outputs are materialized to disk so each iteration can inform the next one.

## Security warning

**ADSA executes model-generated Python locally.** The current research implementation can also ask a repair model to add package-install commands when imports are missing.

Run it only in an isolated/disposable environment:

- use a container/VM or otherwise sandbox the process;
- use least-privilege, revocable API credentials;
- do not expose production secrets or sensitive/private datasets to generated code;
- restrict filesystem/network access where appropriate;
- review generated code before using ADSA on valuable systems or data;
- do not assume model-generated dependency installation is trustworthy.

See [`SECURITY.md`](SECURITY.md) for the project security boundary.

## Requirements

- Python 3.8+ for the historical implementation
- dependencies from `requirements.txt`
- Azure OpenAI credentials
- Anthropic API credentials

## Installation

```bash
git clone https://github.com/AteneaLabs/adsa.git
cd adsa
pip install -r requirements.txt
cp .env.example .env
```

Configure the variables documented in `.env.example`.

## Problem specification

Create `problem_info.md` describing:

- objective/target;
- train/test files;
- evaluation metric;
- runtime/memory constraints;
- expected output format.

The repository contains an example specification and example tabular data.

## Run

```bash
python adsa.py
```

Typical generated artifacts:

- `solution.py` — current candidate solution;
- `progress_report.json` — metrics/progress produced by the candidate;
- `results.csv` — predictions/output;
- `execution_logs.txt` — execution feedback;
- `older_solutions/` — previous iterations.

## Research and reproducibility

The included whitepapers document the project concept:

- [`ADSA_Whitepaper_EN.pdf`](ADSA_Whitepaper_EN.pdf)
- [`ADSA_Whitepaper_ES.pdf`](ADSA_Whitepaper_ES.pdf)

For externally cited performance claims, prefer immutable benchmark receipts over prose in a paper or README. The minimum evidence contract is documented in [`EVIDENCE.md`](EVIDENCE.md).

## License

ADSA source is publicly available under the project license in [`LICENSE.md`](LICENSE.md). It is a permissive MIT-derived software license with additional attribution and Atenea/Atenea Labs trademark conditions. Review the actual license text before redistribution or derivative use.

---

<a name="español"></a>

# Español

## Qué es ADSA

ADSA es un **prototipo de investigación open source** de Atenea Labs para flujos autónomos de ciencia de datos. A partir de un problema de machine learning tabular, puede generar soluciones candidatas en Python, ejecutarlas, inspeccionar resultados/errores, solicitar reparaciones o mejoras de rendimiento a modelos de IA e iterar conservando soluciones y métricas anteriores.

El repositorio demuestra un bucle autónomo real de ejecución. Debe evaluarse por su código y ejecuciones reproducibles, no mediante afirmaciones de ranking o percentiles sin evidencia reproducible asociada.

> **Política de evidencia:** un claim de benchmark/rendimiento sólo se considera verificado cuando existe o se enlaza un receipt inmutable con dataset, métrica, versión del código, configuración de modelos/proveedores y resultado. Ver [`EVIDENCE.md`](EVIDENCE.md).

## Qué demuestra el código actual

La implementación actual incluye:

- **Generación iterativa de soluciones ML** mediante Azure OpenAI.
- **Bucle de feedback de ejecución**, utilizando métricas/resultados previos en iteraciones posteriores.
- **Reparación automática** mediante Anthropic Claude cuando falla el Python generado.
- **Timeouts y recuperación de rendimiento** cuando una solución supera el presupuesto de ejecución.
- **Historial de soluciones**, resultados y `progress_report.json`.
- **Prompts conscientes de GPU** para aprovechar aceleración cuando esté disponible.
- **Separación de proveedores** entre generación y reparación/optimización.

ADSA es un prototipo de investigación; no es todavía un servicio AutoML de producción ni un sandbox de seguridad.

## Arquitectura

```text
problem_info.md + train.csv/test.csv
            |
            v
 modelo generador de solución
            |
            v
       Python generado
            |
            v
 ejecución local con timeout
       |              |
       | éxito        | error/timeout
       v              v
 progreso/resultados reparación u optimización
       |              |
       +------ feedback+
              |
              v
       siguiente iteración
```

## Advertencia de seguridad

**ADSA ejecuta Python generado por modelos de IA en la máquina local.** La implementación de investigación actual también puede pedir al modelo reparador que introduzca comandos de instalación de dependencias cuando faltan imports.

Úsalo únicamente en un entorno aislado/desechable:

- contenedor/VM o sandbox equivalente;
- credenciales API revocables y con mínimo privilegio;
- no expongas secretos de producción ni datasets sensibles/privados al código generado;
- limita filesystem/red cuando proceda;
- revisa el código generado antes de usar ADSA sobre sistemas o datos valiosos;
- no asumas que una dependencia propuesta por el modelo es confiable.

Ver [`SECURITY.md`](SECURITY.md).

## Requisitos

- Python 3.8+ para la implementación histórica
- dependencias de `requirements.txt`
- credenciales Azure OpenAI
- credenciales Anthropic

## Instalación

```bash
git clone https://github.com/AteneaLabs/adsa.git
cd adsa
pip install -r requirements.txt
cp .env.example .env
```

Configura las variables documentadas en `.env.example`.

## Especificación del problema

Crea `problem_info.md` indicando:

- objetivo/target;
- ficheros de train/test;
- métrica de evaluación;
- restricciones de ejecución/memoria;
- formato de salida esperado.

El repositorio contiene un ejemplo.

## Ejecución

```bash
python adsa.py
```

Artefactos habituales:

- `solution.py` — solución candidata actual;
- `progress_report.json` — métricas/progreso producidas por la solución;
- `results.csv` — predicciones/salida;
- `execution_logs.txt` — feedback de ejecución;
- `older_solutions/` — iteraciones anteriores.

## Investigación y reproducibilidad

Whitepapers incluidos:

- [`ADSA_Whitepaper_EN.pdf`](ADSA_Whitepaper_EN.pdf)
- [`ADSA_Whitepaper_ES.pdf`](ADSA_Whitepaper_ES.pdf)

Para claims externos de rendimiento, deben preferirse receipts de benchmark inmutables y reproducibles frente a afirmaciones narrativas del whitepaper o README. El contrato mínimo está en [`EVIDENCE.md`](EVIDENCE.md).

## Licencia

El código fuente de ADSA es público bajo la licencia del proyecto en [`LICENSE.md`](LICENSE.md): una licencia permisiva derivada de MIT con requisitos adicionales de atribución y protección de las marcas Atenea/Atenea Labs. Consulta el texto real antes de redistribuir o crear derivados.

---

## Contact

- Atenea Labs: https://atenealabs.com
- Research: https://adsa.atenea.dev
- Repository: https://github.com/AteneaLabs/adsa

ADSA is developed by the Atenea Labs Research Team.
