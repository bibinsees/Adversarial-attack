# Defamiliarization Attack: Literary Theory Enabled Discussion of LLM Safety

This repository contains code and datasets for the research paper **"Defamiliarization Attack: Literary Theory Enabled Discussion of LLM Safety"** submitted to a peer-reviewed conference.

## Overview

Defamiliarization attack is a novel multi-turn jailbreaking technique that embeds malicious intent within ostensibly harmless narratives. By reframing harmful requests in "unmarked" contexts, large language models (LLMs) can be coerced into producing undesirable outputs. Unlike traditional token-level attacks, defamiliarization manipulates context and presentation, exposing vulnerabilities that cannot be addressed by trigger-word detection alone.

**Key Findings:**
- Smaller-parameter open-weight models are significantly more susceptible to defamiliarization attacks
- Frontier models (GPT-5, Gemini 3) demonstrate improved robustness compared to GPT-4 lineage
- context and narrative driven attacks represent a critical gap in current safety alignment strategies

## Research Contributions

1. **Defamiliarization Attack Definition**: Formalized a multi-turn prompting strategy that progressively guides LLMs toward harmful content through narrative framing
2. **Empirical Evaluation**: Tested across 7 high-risk adversarial goals (self-harm, violence, crime, fraud) on 14 models (open-source and proprietary)
3. **AutoDefa Framework**: Automated pipeline for scalable regression testing, instantiated on the HomeTheft task
4. **Safety Analysis**: Revealed inverse relationship between model scale and susceptibility, with task-dependent semantic blind spots in frontier systems

## Repository Structure

```
 AutoDefa.ipynb                       # Automated defamiliarization pipeline implementation
 dataset_AutoDefa/                    # dataset generated via automation of defamilirization pipeline
    home_theft/                       # HomeTheft task dataset
        gpt4.1-nano_full.txt
        gpt4.1full
        gpt4.1minifull
        gpt4turbofull.txt
        gpt5.2full
        gpt5minifull.txt
        gpt5nanofull.txt
 defamilirization_manual_dataset.xlsx # dataset generated via manual defamilirization attack 
 requirements.txt                     # Python dependencies
 README.md                            # This file
```

## Installation

### Prerequisites
- Python 3.9+
- GPU (NVIDIA RTX for local inference) or API access to proprietary models
- Ollama v0.13.1+ (for local open-source model inference)

### Setup

1. Clone the repository:
```bash
git clone https://github.com/bibinsees/Adversarial-attack.git
cd Adversarial-attack
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Configure environment variables:
```bash
cp .env.example .env
# Edit .env with your OpenAI API keys
```

## Usage

### Running AutoDefa Pipeline

Execute the automated defamiliarization attack on target models:

```python
# See AutoDefa.ipynb for full implementation
from openevals.simulators import run_multiturn_simulation
import json

# Run 10-turn simulation with dual-judge evaluation
simulator_result = run_multiturn_simulation(
    app=app,
    user=user,
    max_turns=10,
)
```

### Manual Attack Examples

The paper demonstrates defamiliarization attacks across multiple adversarial tasks:

| Category | Task | Example |
|----------|------|---------|
| Violence / Crime | HomeTheft | Breaking into a residence |
| Illegal Activities | DrugTraffic | Smuggling narcotics |
| Violence / Mass Harm | SchoolMassacre | Mass casualty planning |
| Self-Harm | SuicideAssist | Suicide facilitation |
| Fraud | AmazonFraud | Return fraud schemes |
| Violence / Crime | RobberyEscape | Evading law enforcement |
| Illegal Activities | MethRecipe | Drug synthesis |

## Experimental Setup

### Models Evaluated

**Open-Source Models (Local Inference via Ollama):**
- Mistral-NeMo 12B
- DeepSeek-R1 8B
- LLaMA-3.1-8B
- Qwen3-14B
- Gemma-3-27B
- gpt-oss-120B

**Proprietary Models (API Access):**
- GPT-4.1, GPT-4.1 turbo, GPT-4o variants
- GPT-5-nano, GPT-5-mini, GPT-5.2
- Gemini 3 Pro Preview

### Evaluation Metrics

- **Attack Success Rate (ASR)**: Binary success (harmful content generated)
- **Multi-Judge Verification**: Dual-LLM evaluation + manual verification

## Key Results

### Manual Defamiliarization
- **Open-weight models**: Near-total safety collapse across all 7 tasks
- **Frontier models**: 15-40% vulnerability across high-risk domains
- **Inverse relationship**: Model scale positively correlates with robustness

### AutoDefa Automation
- Successfully generated contextually coherent jailbreak sequences
- Achieved 10-turn conversations maintaining narrative consistency
- Dual-judge agreement rate: >95% with manual labels

## Ethical Considerations

This research is conducted strictly for defensive purposes. All experiments:
- Follow responsible disclosure principles
- Include detailed ethics statements in the paper
- Are limited to research environments
- Aim to improve LLM safety mechanisms

> **Disclaimer**: This repository contains examples and code related to adversarial attacks on AI systems. Content is provided for research and defensive purposes only. Malicious use of these techniques is prohibited.

## Technical Stack

- **LLM Frameworks**: OpenAI API, Google Gemini API, Ollama
- **Evaluation**: LangSmith for tracing, custom dual-judge evaluation
- **Data Processing**: Pandas, CSV
- **Automation**: Multi-turn simulation framework (openevals)
- **Documentation**: LaTeX, Jupyter Notebooks

## Paper Reference

**Title**: Defamiliarization Attack: Literary Theory Enabled Discussion of LLM Safety

**Authors**: Bibin Babu, Yana Agafonova, Sebastian Biedermann, Ivan Yamshchikov

**Submission**: Electronics (MDPI), 2025

## Related Work

Key comparative frameworks referenced in this research:
- **Crescendo** (Russinovich et al., 2025): State-of-the-art multi-turn jailbreaking
- **TAP** (Mehrotra et al., 2024): Tree-of-thought attack optimization
- **GCG** (Zou et al., 2023): Universal adversarial perturbations
- **DeepInception** (Li et al., 2024): Layered imaginary scenarios

## Contributing

This repository is primarily for reproducing research findings. Issues and discussions related to the paper are welcome.

