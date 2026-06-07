# Cybersecurity Assessment LLM-HITL Benchmark

Dataset and research artifacts associated with the master's dissertation:

**Avaliação do Uso de Grandes Modelos de Linguagem na Análise de Riscos em Segurança da Informação: Um Estudo Comparativo com Especialistas Humanos**

Universidade Federal de Uberlândia (UFU)  
Programa de Pós-Graduação em Ciência da Computação (PPGCO)  
Author: Gustavo Roberto Pinto  
Advisor: Rodrigo Sanches Miani

---

## Overview

This repository provides the datasets and experimental artifacts used in a study investigating the use of Large Language Models (LLMs) for information security risk assessment.

The research compares risk evaluations produced by human cybersecurity professionals and five state-of-the-art LLMs:

- ChatGPT 5
- Claude Opus 4.1
- Gemini 2.5 Pro
- DeepSeek V3.1
- Llama 4 Scout

The study evaluates whether LLMs can reliably replicate human judgment in cybersecurity risk assessment and examines the role of Human-in-the-Loop (HITL) validation.

---

## Research Questions

### RQ1

To what extent can LLMs be considered reliable for performing information security risk assessments without the participation of human experts?

### RQ2

How do LLMs compare with human professionals when evaluating cybersecurity risks across 18 structured scenarios?

Sub-questions:

- Comparison against Senior and Specialist professionals.
- Comparison against other professional experience levels.

---

## Methodology

The benchmark was developed using 18 cybersecurity risk scenarios derived from the CIS Critical Security Controls (Version 8).

The research followed four major phases:

1. Creation of risk assessment scenarios.
2. Calibration and validation of LLM responses.
3. Collection of responses from 50 cybersecurity and technology professionals.
4. Statistical comparison between human and LLM assessments.

Participants assigned risk scores to each scenario, and the same scenarios were evaluated by the selected LLMs under identical conditions.

---

## Main Findings

The results indicate that:

- All evaluated LLMs showed strong positive correlation with human assessments.
- However, LLMs consistently assigned lower risk scores than human participants.
- Risk underestimation was more pronounced when compared with Senior and Specialist professionals.
- The findings support the use of LLMs as decision-support tools rather than autonomous cybersecurity risk assessors.

---

## Repository Contents

### results_final_scenarios.xlsx

Final consolidated dataset used in the statistical analysis.

Contains:

- Human responses
- LLM responses
- Aggregated risk scores
- Statistical comparison data

### Pesquisa-de-riscos-cibernéticos-respostas.csv

Anonymized responses collected from the 50 human participants.

### Additional Artifacts

The repository may also contain supporting materials related to:

- Risk scenarios
- Benchmark construction
- Experimental setup
- Statistical analysis

---

## Reproducibility

This repository was created to support transparency, reproducibility, and future research on the application of Large Language Models in cybersecurity risk assessment.

Researchers are encouraged to reuse the benchmark, datasets, and methodology in future studies.

---

## Related Publication

A scientific article derived from this research was submitted to the *International Journal of Data Science and Analytics* (Springer Nature).

A preprint version is available at:

https://arxiv.org/abs/2605.05424

---

## Citation

If you use this repository, dataset, or benchmark in academic work, please cite the dissertation and repository metadata provided in `CITATION.cff`.

---

## License

MIT License
