<div align="center">

# 🌟 Awesome Large Model Self-Distillation

**A curated reading list for awesome self-distillation works in LLMs, MLLMs, reasoning models, diffusion LMs, and large generative models.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
![Papers](https://img.shields.io/badge/2026%20Papers-26-blue)
![Last Update](https://img.shields.io/badge/Last%20Update-2026--05--26-brightgreen)
![Topic](https://img.shields.io/badge/Topic-Self--Distillation-purple)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-orange)

</div>

---

## 🔎 Scope

This repository tracks papers where a large model **improves itself without relying on a stronger external teacher**. Typical patterns include:

- **Same-model teacher/student** under different contexts.
- **Privileged-context self-distillation**, e.g., verified solutions, feedback, documents, image crops, or target images.
- **On-policy self-distillation**, where the model learns from its own rollouts.
- **Self-revision / self-feedback**, turning sparse rewards or feedback into dense token-level supervision.
- **Self-referential compression**, e.g., post-pruning or few-step generation via self-distillation.

> 🏛️ **Venue.** The `Venue` column records the official conference/journal venue when verified from an official source; otherwise it is marked as `arXiv`.
>
> ⭐ **GitHub Stars.** For repositories with public GitHub code, this README uses dynamic Shields badges such as `img.shields.io/github/stars/...`, so star counts update automatically when rendered on GitHub. For code released inside a monorepo subdirectory, the badge shows stars of the parent repository.

---

## 🧭 Quick Navigation

| Section | What it covers |
|---|---|
| [🧩 Taxonomy](#taxonomy) | Method families and typical teacher signals. |
| [🧠 Core LLM Self-Distillation and Reasoning](#core-llm-self-distillation-and-reasoning) | OPSD, SDPO, SD-Zero, UniSD, reasoning variants. |
| [📚 Context, Continual, and Experiential Learning](#context-continual-and-experiential-learning) | SDFT, OPCD, OEL, self-play / experience internalization. |
| [⚡ Efficiency, Compression, and Code Generation](#efficiency-compression-and-code-generation) | MTP, reasoning compression, code self-distillation, diffusion LMs. |
| [🖼️ Multimodal and Generative Models](#multimodal-and-generative-models) | Vision-OPD, D-OPSD, 4D perception, long-context self-distillation. |
| [🔬 Analysis, Surveys, and Diagnostics](#analysis-surveys-and-diagnostics) | Failure modes, uncertainty, and overview papers. |
| [🤝 Contributing](#contributing) | How to add a new paper. |

---

## 📌 Highlights

| Method | Paper | Venue | Code / Stars | Why it matters |
|---|---|---|---|---|
| **OPSD** | [Self-Distilled Reasoner: On-Policy Self-Distillation for Large Language Models](https://arxiv.org/abs/2601.18734) | ICML 2026 | [Code](https://github.com/siyan-zhao/OPSD) [![Stars](https://img.shields.io/github/stars/siyan-zhao/OPSD?style=social)](https://github.com/siyan-zhao/OPSD) | Canonical same-model on-policy self-distillation for LLM reasoning. |
| **SDFT** | [Self-Distillation Enables Continual Learning](https://arxiv.org/abs/2601.19897) | ICML 2026 | [Code](https://github.com/idanshen/Self-Distillation) [![Stars](https://img.shields.io/github/stars/idanshen/Self-Distillation?style=social)](https://github.com/idanshen/Self-Distillation) | Turns demonstrations into on-policy self-distillation signals for continual learning. |
| **SDPO** | [Reinforcement Learning via Self-Distillation](https://arxiv.org/abs/2601.20802) | ICML 2026 | [Code](https://github.com/lasgroup/SDPO) [![Stars](https://img.shields.io/github/stars/lasgroup/SDPO?style=social)](https://github.com/lasgroup/SDPO) | Converts rich feedback into dense self-distillation guidance. |
| **OPCD** | [On-Policy Context Distillation](https://arxiv.org/abs/2602.12275) | arXiv | [Code](https://github.com/microsoft/LMOps/tree/main/opcd) [![Stars](https://img.shields.io/github/stars/microsoft/LMOps?style=social)](https://github.com/microsoft/LMOps) | Distills prompts, experience, and context into model parameters. |
| **Vision-OPD** | [Vision-OPD: Learning to See Fine Details for Multimodal LLMs via On-Policy Self-Distillation](https://arxiv.org/abs/2605.18740) | arXiv | [Code](https://github.com/VisionOPD/Vision-OPD) [![Stars](https://img.shields.io/github/stars/VisionOPD/Vision-OPD?style=social)](https://github.com/VisionOPD/Vision-OPD) | Transfers crop-conditioned perception into full-image MLLMs. |
| **D-OPSD** | [OPSD for Step-Distilled Diffusion Models](https://arxiv.org/abs/2605.05204) | arXiv | [Code](https://github.com/vvvvvjdy/D-OPSD) [![Stars](https://img.shields.io/github/stars/vvvvvjdy/D-OPSD?style=social)](https://github.com/vvvvvjdy/D-OPSD) | Extends OPSD to continuous tuning of few-step diffusion image models. |

---

<a id="taxonomy"></a>

## 🧩 Taxonomy

| Category | Core idea | Typical teacher signal | Representative papers |
|---|---|---|---|
| **Privileged-context self-distillation** | The same model plays teacher and student under different contexts. | Verified solution, reference trace, document, crop image, target image, or instruction prefix. | OPSD, GATES, Vision-OPD, D-OPSD |
| **On-policy self-distillation** | The student trains on its own rollouts to reduce train-test mismatch. | Token-level KL/divergence on student trajectories. | OPSD, SDPO, OPCD, OGLS-SD |
| **Self-revision / self-feedback distillation** | The model converts sparse reward or feedback into dense supervision. | Reviser distribution, feedback-conditioned distribution, successful rollout. | SD-Zero, SDPO |
| **Context / experience internalization** | Useful prompts, demonstrations, memories, or deployment traces are distilled into weights. | Context-conditioned policy or extracted experience. | SDFT, OPCD, OEL |
| **Efficiency-oriented self-distillation** | Self-distillation shortens reasoning, predicts multiple tokens, or speeds up generation. | Concise self-policy, multi-token teacher, trajectory teacher, pre-compression distribution. | CRISP, MTP, T3D, Apple SSD |
| **Multimodal / generative self-distillation** | A privileged modality, region, or condition acts as self-teacher for normal inference. | Crop-conditioned MLLM, image-conditioned diffusion branch, spatiotemporal context. | Vision-OPD, D-OPSD, SelfEvo |
| **Diagnostics and theory** | Studies when self-distillation helps or hurts. | Uncertainty, entropy, task coverage, teacher exposure. | Why Does SD Degrade?, UniSD, Brief Overview |

---

# 📄 2026 Papers

<a id="core-llm-self-distillation-and-reasoning"></a>

## 🧠 Core LLM Self-Distillation and Reasoning

| Date | Paper | Venue | Code / Stars | Area | Key idea |
|---|---|---|---|---|---|
| 2026-01 | [Self-Distilled Reasoner: On-Policy Self-Distillation for Large Language Models](https://arxiv.org/abs/2601.18734) | ICML 2026 | [Code](https://github.com/siyan-zhao/OPSD) [![Stars](https://img.shields.io/github/stars/siyan-zhao/OPSD?style=social)](https://github.com/siyan-zhao/OPSD) / [Blog](https://siyan-zhao.github.io/blog/2026/opsd/) | Math reasoning | Introduces **OPSD**: the same LLM acts as student and teacher; the teacher conditions on privileged solutions and provides dense token-level supervision on student rollouts. |
| 2026-01 | [Reinforcement Learning via Self-Distillation](https://arxiv.org/abs/2601.20802) | ICML 2026 | [Code](https://github.com/lasgroup/SDPO) [![Stars](https://img.shields.io/github/stars/lasgroup/SDPO?style=social)](https://github.com/lasgroup/SDPO) | RLVR, code, math, tool use | Proposes **SDPO**, turning rich textual feedback into dense self-distillation signals without an external teacher or explicit reward model. |
| 2026-02 | [Learning While Staying Curious: Entropy-Preserving Supervised Fine-Tuning via Adaptive Self-Distillation for Large Reasoning Models](https://arxiv.org/abs/2602.02244) | ACL 2026 Main | [Code](https://github.com/HaoooWang/CurioSFT) [![Stars](https://img.shields.io/github/stars/HaoooWang/CurioSFT?style=social)](https://github.com/HaoooWang/CurioSFT) | Reasoning SFT | **CurioSFT** uses self-exploratory distillation and entropy-guided temperature selection to preserve exploration during SFT; accepted to ACL 2026 Main according to the project page. |
| 2026-02 | [GATES: Self-Distillation under Privileged Context with Consensus Gating](https://arxiv.org/abs/2602.20574) | arXiv | - | Document-grounded QA, math | Uses asymmetric document context and tutor consensus to gate reliable self-distillation when labels/rewards are unavailable. |
| 2026-03 | [PACED: Distillation and On-Policy Self-Distillation at the Frontier of Student Competence](https://arxiv.org/abs/2603.11178) | arXiv | - | Math reasoning | Weights examples by the student's empirical pass rate, focusing self-distillation on the competence frontier rather than too-easy or too-hard samples. |
| 2026-04 | [Self-Distillation Zero: Self-Revision Turns Binary Rewards into Dense Supervision](https://arxiv.org/abs/2604.12002) | arXiv | [Project](https://ying-hui-he.github.io/publication/sdzero) | Math and code reasoning | **SD-Zero** trains one model as both generator and reviser, converting binary rewards into dense token-level supervision through self-revision. |
| 2026-05 | [Adaptive Teacher Exposure for Self-Distillation in LLM Reasoning](https://arxiv.org/abs/2605.11458) | arXiv | - | Math reasoning | Treats how much privileged reasoning the teacher sees as an adaptive control variable rather than always exposing the full solution. |
| 2026-05 | [Training with Harnesses: On-Policy Harness Self-Distillation for Complex Reasoning](https://arxiv.org/abs/2605.08741) | arXiv | - | Complex reasoning | Distills temporary inference-time harnesses, such as draft-verify or plan-solve workflows, back into the base model. |
| 2026-05 | [OGLS-SD: On-Policy Self-Distillation with Outcome-Guided Logit Steering for LLM Reasoning](https://arxiv.org/abs/2605.12400) | arXiv | - | Reasoning | Calibrates self-teacher logits using outcome-level correctness signals to reduce reflection-induced teacher bias. |
| 2026-05 | [Respecting Self-Uncertainty in On-Policy Self-Distillation for Efficient LLM Reasoning](https://arxiv.org/abs/2605.13255) | arXiv | - | Efficient reasoning | **EGRSD / CL-EGRSD** gates token updates by teacher entropy and reward-grounded direction, preserving uncertainty-aware reasoning. |
| 2026-05 | [UniSD: Towards a Unified Self-Distillation Framework for Large Language Models](https://arxiv.org/abs/2605.06597) | arXiv | - | Unified framework | Integrates multi-teacher agreement, EMA stabilization, token-level contrastive learning, feature matching, and divergence clipping. |

<a id="context-continual-and-experiential-learning"></a>

## 📚 Context, Continual, and Experiential Learning

| Date | Paper | Venue | Code / Stars | Area | Key idea |
|---|---|---|---|---|---|
| 2026-01 | [Self-Distillation Enables Continual Learning](https://arxiv.org/abs/2601.19897) | arXiv | [Code](https://github.com/idanshen/Self-Distillation) [![Stars](https://img.shields.io/github/stars/idanshen/Self-Distillation?style=social)](https://github.com/idanshen/Self-Distillation) / [Project](https://self-distillation.github.io/SDFT) | Continual learning | **SDFT** uses demonstration-conditioned in-context behavior as a self-teacher, reducing catastrophic forgetting compared with SFT. |
| 2026-02 | [On-Policy Context Distillation for Language Models](https://arxiv.org/abs/2602.12275) | arXiv | [Code](https://github.com/microsoft/LMOps/tree/main/opcd) [![Stars](https://img.shields.io/github/stars/microsoft/LMOps?style=social)](https://github.com/microsoft/LMOps) | Context distillation | **OPCD** trains on student-generated trajectories while matching a context-conditioned teacher, internalizing prompts, demonstrations, and experience. |
| 2026-03 | [Online Experiential Learning for Language Models](https://arxiv.org/abs/2603.16856) | arXiv | [Code](https://aka.ms/oel-code) | Online learning, text games | **OEL** extracts transferable experience from deployment trajectories and consolidates it into model weights through on-policy context distillation. |
| 2026-04 | [$\pi$-Play: Multi-Agent Self-Play via Privileged Self-Distillation without External Data](https://arxiv.org/abs/2604.14054) | arXiv | - | Search agents, self-play | Uses the question construction path from self-play as privileged context for dense self-distillation in data-free search-agent training. |

<a id="efficiency-compression-and-code-generation"></a>

## ⚡ Efficiency, Compression, and Code Generation

| Date | Paper | Venue | Code / Stars | Area | Key idea |
|---|---|---|---|---|---|
| 2026-02 | [Multi-Token Prediction via Self-Distillation](https://arxiv.org/abs/2602.06019) | arXiv | [Code](https://github.com/jwkirchenbauer/mtp-lm) [![Stars](https://img.shields.io/github/stars/jwkirchenbauer/mtp-lm?style=social)](https://github.com/jwkirchenbauer/mtp-lm) / [Models](https://huggingface.co/collections/tomg-group-umd/mtp-lm) | Inference acceleration | Converts a next-token LM into a standalone multi-token prediction model through online self-distillation, enabling faster decoding without a separate speculator. |
| 2026-02 | [Few-Step Diffusion Language Models via Trajectory Self-Distillation](https://arxiv.org/abs/2602.12262) | arXiv | [Code](https://github.com/Tyrion58/T3D) [![Stars](https://img.shields.io/github/stars/Tyrion58/T3D?style=social)](https://github.com/Tyrion58/T3D) | Diffusion LMs | Uses trajectory-level self-distillation to train few-step diffusion language models and reduce factorization error. |
| 2026-02 | [Post-Training Probability Manifold Correction via Structured SVD Pruning and Self-Referential Distillation](https://arxiv.org/abs/2602.00372) | arXiv | - | Model compression | Combines structured SVD pruning with self-referential distillation that matches the model's pre-compression distribution. |
| 2026-03 | [CRISP: Compressed Reasoning via Iterative Self-Policy Distillation](https://arxiv.org/abs/2603.05433) | arXiv | [Code](https://github.com/HJSang/OPSD_Reasoning_Compression) [![Stars](https://img.shields.io/github/stars/HJSang/OPSD_Reasoning_Compression?style=social)](https://github.com/HJSang/OPSD_Reasoning_Compression) | Reasoning compression | Distills the model's own concise behavior into itself, reducing reasoning tokens while preserving or improving accuracy. Earlier versions used the title *On-Policy Self-Distillation for Reasoning Compression*. |
| 2026-04 | [Embarrassingly Simple Self-Distillation Improves Code Generation](https://arxiv.org/abs/2604.01193) | arXiv | [Code](https://github.com/apple/ml-ssd) [![Stars](https://img.shields.io/github/stars/apple/ml-ssd?style=social)](https://github.com/apple/ml-ssd) | Code generation | Samples code solutions from the model itself and fine-tunes on those samples, improving LiveCodeBench without external teacher, verifier, or RL. |

<a id="multimodal-and-generative-models"></a>

## 🖼️ Multimodal and Generative Models

| Date | Paper | Venue | Code / Stars | Area | Key idea |
|---|---|---|---|---|---|
| 2026-04 | [OPSDL: On-Policy Self-Distillation for Long-Context Language Models](https://arxiv.org/abs/2604.17535) | arXiv | - | Long-context LLMs | Uses the model's short-context strength as a self-teacher for long-context generation, providing dense supervision under extracted relevant context. |
| 2026-04 | [Self-Improving 4D Perception via Self-Distillation](https://arxiv.org/abs/2604.08532) | arXiv | - | 4D perception | **SelfEvo** uses spatiotemporal context asymmetry to improve pretrained multi-view reconstruction models from unlabeled videos. |
| 2026-05 | [D-OPSD: On-Policy Self-Distillation for Continuously Tuning Step-Distilled Diffusion Models](https://arxiv.org/abs/2605.05204) | arXiv | [Code](https://github.com/vvvvvjdy/D-OPSD) [![Stars](https://img.shields.io/github/stars/vvvvvjdy/D-OPSD?style=social)](https://github.com/vvvvvjdy/D-OPSD) / [Project](https://vvvvvjdy.github.io/d-opsd/) | Image generation | Applies OPSD to step-distilled diffusion models; the teacher conditions on text plus target image while the student rolls out from text only. |
| 2026-05 | [Vision-OPD: Learning to See Fine Details for Multimodal LLMs via On-Policy Self-Distillation](https://arxiv.org/abs/2605.18740) | arXiv | [Code](https://github.com/VisionOPD/Vision-OPD) [![Stars](https://img.shields.io/github/stars/VisionOPD/Vision-OPD?style=social)](https://github.com/VisionOPD/Vision-OPD) | MLLMs, fine-grained visual understanding | Transfers crop-conditioned privileged perception into full-image MLLM behavior without external teachers, labels, verifiers, or inference-time visual tools. |

<a id="analysis-surveys-and-diagnostics"></a>

## 🔬 Analysis, Surveys, and Diagnostics

| Date | Paper | Venue | Code / Stars | Area | Key idea |
|---|---|---|---|---|---|
| 2026-03 | [Why Does Self-Distillation (Sometimes) Degrade the Reasoning Capability of LLMs?](https://arxiv.org/abs/2603.24472) | arXiv | - | Diagnostics | Shows that rich teacher conditioning can suppress epistemic verbalization and hurt OOD math reasoning; highlights uncertainty preservation as a key issue. |
| 2026-05 | [A Brief Overview: On-Policy Self-Distillation In Large Language Models](https://arxiv.org/abs/2605.18141) | arXiv | - | Overview | Beginner-friendly overview of OPSD concepts, design patterns, and recent developments. |

---

## 🧰 Related Awesome Lists

| Resource | Stars | Notes |
|---|---|---|
| [Awesome On-Policy Distillation](https://github.com/thinkwee/AwesomeOPD) | [![Stars](https://img.shields.io/github/stars/thinkwee/AwesomeOPD?style=social)](https://github.com/thinkwee/AwesomeOPD) | Broader OPD list, including self-distillation and external-teacher OPD. |
| [awesome-on-policy-distillation](https://github.com/chrisliu298/awesome-on-policy-distillation) | [![Stars](https://img.shields.io/github/stars/chrisliu298/awesome-on-policy-distillation?style=social)](https://github.com/chrisliu298/awesome-on-policy-distillation) | Papers, tools, and industrial recipes for on-policy distillation. |

---

<a id="contributing"></a>

## 🤝 Contributing

Contributions are welcome. A good entry should satisfy most of the following:

1. **Large-model relevance:** LLM, MLLM, diffusion LM, large generative model, or foundation-model adaptation/compression.
2. **Self-distillation signal:** no stronger external teacher is required, or the same model is used as teacher/student under different conditions.
3. **Clear training signal:** e.g., on-policy rollout KL, self-revision distribution, context-conditioned teacher, trajectory-level distillation, or self-referential pre/post-compression distribution.
4. **Reproducibility:** paper link, code/project link if available, model/data links if available.

Suggested PR format:

```markdown
| YYYY-MM | [Paper Title](paper_url) | Venue | [Code](code_url) [![Stars](https://img.shields.io/github/stars/owner/repo?style=social)](https://github.com/owner/repo) | Area | One-sentence key idea. |
```

Please avoid adding standard knowledge-distillation papers that only use a stronger external teacher unless they are directly connected to self-distillation or on-policy self-distillation.

---

## 📜 Citation

If this list helps your research, please consider starring the repository and citing the original papers.

```bibtex
@misc{awesome_self_distillation,
  title        = {Awesome Self-Distillation},
  author       = {MAC-AutoML},
  year         = {2026},
  howpublished = {\url{https://github.com/MAC-AutoML/Awesome-Self-Distillation}}
}
```

---

<div align="center">

**If you find this list useful, please consider giving it a star ⭐ and opening a PR to add new papers.**

</div>
