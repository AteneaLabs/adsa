# ADSA (Autonomous Data Scientist Agent)

<div align="center">
  <img src="atenea-icono.svg" alt="Atenea Labs Logo" width="150"/>


By Atenea Labs Research Team


**[🇬🇧 English](#english) | [🇪🇸 Español](#español)**

</div>

---

<a name="english"></a>
# 🇬🇧 English

## Overview

ADSA is an autonomous multi-agent system developed by [Atenea Labs](https://www.atenea.dev/) that automates the entire machine learning process. In its evaluation it placed 71st of 2,461 active participants (top 2.9%) in Kaggle's Spaceship Titanic competition ([whitepaper](ADSA_Whitepaper_EN.pdf), section 7.3).

> **Context.** ADSA was built at Atenea Labs in late 2024, when OpenAI o1 and Claude 3.5 Sonnet were the frontier models. It pairs an o1 agent that writes the ML code with a Claude 3.5 Sonnet agent that debugs and fixes it, under a coordinator that runs the loop. The whitepaper was published on 15 January 2025. This repository is kept as that work was released.

📄 Read our detailed whitepaper: [English Version](ADSA_Whitepaper_EN.pdf)

## About Atenea Labs

Atenea Labs is the applied-AI lab Carlos Navarro founded in 2023, where ADSA was built. Today Atenea Labs builds [Vitalink](https://www.vitalink.chat/), the action layer for healthcare, and [Brida](https://www.brida.ai/), the all-in-one infrastructure for autonomous companies. More at [atenea.dev](https://www.atenea.dev/).

## Key Features

- **Autonomous Operation**: Fully automated machine learning pipeline
- **Multi-Agent Architecture**: Utilizes multiple AI agents for different tasks
- **Iterative Optimization**: Continuously improves models through multiple iterations
- **GPU Acceleration**: Automatic GPU detection and utilization when available
- **Error Recovery**: Self-healing capabilities with automatic error detection and correction
- **Performance Monitoring**: Detailed progress tracking and reporting

## System Components

1. **API Clients Setup**
   - Azure OpenAI integration
   - Anthropic Claude integration
   - Environment configuration management

2. **Data Processing**
   - Automated data loading and preparation
   - Dynamic feature engineering
   - Training/test set management

3. **ML Solution Generation**
   - Automated code generation
   - Model selection and optimization
   - GPU utilization when available
   - Cross-validation implementation

4. **Error Handling & Optimization**
   - Automatic error detection
   - Code optimization for performance
   - Timeout management
   - Self-healing capabilities

## Security

ADSA generates and runs Python code. Treat that code as untrusted and run ADSA in an isolated environment; see [SECURITY.md](SECURITY.md).

## Requirements

- Python 3.8+
- Required Python packages (see requirements.txt)
- API Keys:
  - Azure OpenAI API
  - Anthropic Claude API

## API Setup

### Azure OpenAI Setup
1. Visit [Azure OpenAI Service](https://azure.microsoft.com/en-us/products/cognitive-services/openai-service)
2. Sign up for an Azure account if you don't have one
3. Create a new Azure OpenAI resource
4. Deploy o1 model in your resource
5. Get your API credentials:
   - Endpoint URL
   - API Key
   - Deployment Name
   - API Version

### Anthropic Claude Setup
1. Visit [Anthropic Claude](https://www.anthropic.com/claude)
2. Sign up for an account
3. Navigate to API settings
4. Generate an API key

## Installation

1. Clone the repository:
```bash
git clone https://github.com/atenealabs/adsa.git
cd adsa
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Configure environment variables:
```bash
cp .env.example .env
# Edit .env with your API keys:
# AZURE_OPENAI_KEY=your_azure_key
# AZURE_OPENAI_ENDPOINT=your_azure_endpoint
# AZURE_OPENAI_DEPLOYMENT=your_deployment_name
# AZURE_OPENAI_VERSION=your_api_version
# ANTHROPIC_API_KEY=your_claude_key
```

## Problem Specification

Before running ADSA, you need to create a `problem_info.md` file that describes your machine learning task. This file is crucial as it guides the AI agents in understanding and solving your problem.

### problem_info.md Structure

```markdown
# Problem Description
[Brief description of the problem]

## Objective
[Clear statement of what needs to be predicted/classified/etc.]

## Data Description
- Input file: train.csv
- Test file: test.csv
- Target variable: [name of the target column]
- Features: [list of important features]

## Evaluation Metric
[Specify the metric used to evaluate the model (e.g., accuracy, RMSE, etc.)]

## Constraints
- [Any time constraints]
- [Memory constraints]
- [Other technical constraints]

## Expected Output Format
[Description of the required output format]
```

### Example problem_info.md

```markdown
# Spaceship Titanic Classification

## Objective
Predict which passengers were transported to an alternate dimension during the Spaceship Titanic's collision with a spacetime anomaly.

## Data Description
- Input file: train.csv (8700 passengers)
- Test file: test.csv (4300 passengers)
- Target variable: Transported (boolean)
- Features: PassengerId, HomePlanet, CryoSleep, Cabin, Destination, Age, VIP, RoomService, FoodCourt, ShoppingMall, Spa, VRDeck

## Evaluation Metric
Binary classification accuracy

## Constraints
- Maximum runtime: 30 minutes per iteration
- Memory usage: <32GB RAM
- GPU acceleration when available

## Expected Output Format
CSV file with columns:
- PassengerId
- Transported (boolean: True/False)
```

## Usage

1. Place your training data in `train.csv`
2. Place your test data in `test.csv`
3. Create and configure `problem_info.md` as described above
4. Run ADSA:
```bash
python adsa.py
```

## Output Files

- `solution.py`: Current iteration's ML solution
- `progress_report.json`: Performance metrics and progress tracking
- `results.csv`: Final predictions and results
- `execution_logs.txt`: Detailed execution logs
- `older_solutions/`: Archive of previous iterations

## Architecture

ADSA operates through an iterative process:

1. **Initial Setup**
   - Environment configuration
   - API client initialization
   - Data preparation

2. **Solution Generation**
   - ML code generation via Azure OpenAI
   - Code optimization and error checking
   - GPU utilization verification

3. **Execution & Monitoring**
   - Solution implementation
   - Performance tracking
   - Error detection and recovery

4. **Optimization Loop**
   - Performance analysis
   - Code improvement suggestions
   - Iterative refinement

## Performance

- Maximum runtime: 30 minutes per iteration
- Maximum iterations: 50
- Automatic performance optimization
- GPU acceleration when available

## License

See [LICENSE.md](LICENSE.md) for details.

## Contact

- 🌐 Website: [atenea.dev](https://www.atenea.dev/)
- 📧 Email: [info@atenea.dev](mailto:info@atenea.dev)
- 🔬 Research: [adsa.atenea.dev](https://adsa.atenea.dev)
- 💼 LinkedIn: [Atenea Labs](https://linkedin.com/company/atenealabs)

## About the Team

ADSA is developed by the Atenea Labs Research Team, led by Carlos Navarro Cabrera. Our team combines expertise in artificial intelligence, machine learning, and software engineering to create cutting-edge AI solutions that drive business transformation. 

---

<a name="español"></a>
# 🇪🇸 Español

## Descripción General

ADSA es un sistema multi-agente autónomo desarrollado por [Atenea Labs](https://www.atenea.dev/) que automatiza todo el proceso de machine learning. En su evaluación quedó en el puesto 71 de 2.461 participantes activos (top 2,9 %) de la competición Spaceship Titanic de Kaggle ([whitepaper](ADSA_Whitepaper_ES.pdf), sección 7.3).

> **Contexto.** ADSA se construyó en Atenea Labs a finales de 2024, cuando OpenAI o1 y Claude 3.5 Sonnet eran los modelos frontera. Combina un agente o1 que escribe el código de ML con un agente Claude 3.5 Sonnet que lo depura y corrige, bajo un coordinador que dirige el ciclo. El whitepaper se publicó el 15 de enero de 2025. Este repositorio se conserva tal como se publicó ese trabajo.

📄 Lee nuestro whitepaper detallado: [Versión en Español](ADSA_Whitepaper_ES.pdf)

## Sobre Atenea Labs

Atenea Labs es el laboratorio de IA aplicada que Carlos Navarro fundó en 2023, donde se construyó ADSA. Hoy Atenea Labs construye [Vitalink](https://www.vitalink.chat/), la capa de acción de la salud, y [Brida](https://www.brida.ai/), la infraestructura todo en uno para empresas autónomas. Más en [atenea.dev](https://www.atenea.dev/).

## Características Principales

- **Operación Autónoma**: Pipeline de machine learning completamente automatizado
- **Arquitectura Multi-Agente**: Utiliza múltiples agentes de IA para diferentes tareas
- **Optimización Iterativa**: Mejora continua de modelos a través de múltiples iteraciones
- **Aceleración GPU**: Detección automática y utilización de GPU cuando está disponible
- **Recuperación de Errores**: Capacidades de auto-reparación con detección y corrección automática de errores
- **Monitoreo de Rendimiento**: Seguimiento y reportes detallados del progreso

## Componentes del Sistema

1. **Configuración de Clientes API**
   - Integración con Azure OpenAI
   - Integración con Anthropic Claude
   - Gestión de configuración del entorno

2. **Procesamiento de Datos**
   - Carga y preparación automatizada de datos
   - Ingeniería de características dinámica
   - Gestión de conjuntos de entrenamiento/prueba

3. **Generación de Soluciones ML**
   - Generación automática de código
   - Selección y optimización de modelos
   - Utilización de GPU cuando está disponible
   - Implementación de validación cruzada

4. **Manejo de Errores y Optimización**
   - Detección automática de errores
   - Optimización de código para rendimiento
   - Gestión de tiempos de ejecución
   - Capacidades de auto-reparación

## Requisitos

- Python 3.8+
- Paquetes Python requeridos (ver requirements.txt)
- Claves API:
  - API de Azure OpenAI
  - API de Anthropic Claude

## Instalación

1. Clonar el repositorio:
```bash
git clone https://github.com/atenealabs/adsa.git
cd adsa
```

2. Instalar dependencias:
```bash
pip install -r requirements.txt
```

3. Configurar variables de entorno:
```bash
cp .env.example .env
# Editar .env con tus claves API
```

## Uso

1. Coloca tus datos de entrenamiento en `train.csv`
2. Coloca tus datos de prueba en `test.csv`
3. Configura las especificaciones del problema en `problem_info.md`
4. Ejecuta ADSA:
```bash
python adsa.py
```

## Archivos de Salida

- `solution.py`: Solución ML de la iteración actual
- `progress_report.json`: Métricas de rendimiento y seguimiento del progreso
- `results.csv`: Predicciones y resultados finales
- `execution_logs.txt`: Logs detallados de ejecución
- `older_solutions/`: Archivo de iteraciones anteriores

## Arquitectura

ADSA opera a través de un proceso iterativo:

1. **Configuración Inicial**
   - Configuración del entorno
   - Inicialización de clientes API
   - Preparación de datos

2. **Generación de Soluciones**
   - Generación de código ML vía Azure OpenAI
   - Optimización y verificación de código
   - Verificación de utilización de GPU

3. **Ejecución y Monitoreo**
   - Implementación de soluciones
   - Seguimiento del rendimiento
   - Detección y recuperación de errores

4. **Ciclo de Optimización**
   - Análisis de rendimiento
   - Sugerencias de mejora de código
   - Refinamiento iterativo

## Rendimiento

- Tiempo máximo de ejecución: 30 minutos por iteración
- Iteraciones máximas: 50
- Optimización automática del rendimiento
- Aceleración GPU cuando está disponible

## Licencia

Ver [LICENSE.md](LICENSE.md) para más detalles.

## Contacto

- 🌐 Sitio web: [atenea.dev](https://www.atenea.dev/)
- 📧 Email: [info@atenea.dev](mailto:info@atenea.dev)
- 🔬 Investigación: [adsa.atenea.dev](https://adsa.atenea.dev)
- 💼 LinkedIn: [Atenea Labs](https://linkedin.com/company/atenealabs)

## Sobre el Equipo

ADSA es desarrollado por el Equipo de Investigación de Atenea Labs, liderado por Carlos Navarro Cabrera. Nuestro equipo combina experiencia en inteligencia artificial, machine learning e ingeniería de software para crear soluciones de IA de vanguardia que impulsan la transformación empresarial. 