# ATBench: Agent Trajectory Safety Benchmark Family

<p align="center">
  <a href="https://arxiv.org/abs/2604.02022">📄 ATBench Paper</a>&nbsp&nbsp | &nbsp&nbsp
  <a href="https://arxiv.org/abs/2601.18491">🧾 AgentDoG Paper (ATBench500)</a>
 <br>
  <a href="https://huggingface.co/datasets/AI45Research/ATBench">🤗 Hugging Face Dataset</a>&nbsp&nbsp | &nbsp&nbsp
  <a href="https://huggingface.co/collections/AI45Research/agentdog">🤗 Hugging Face Collection</a>
</p>

**ATBench** is a family of trajectory-level safety benchmarks for long-horizon, tool-using AI agents.
The latest release is introduced in [ATBench: A Diverse and Realistic Agent Trajectory Benchmark for Safety Evaluation and Diagnosis](https://arxiv.org/abs/2604.02022).

This repository follows a versioned naming scheme:

- **ATBench**: the latest 1,000-trajectory release
- **ATBench500**: the original 500-trajectory release introduced with AgentDoG

The benchmark data is available on Hugging Face. This GitHub repository serves as the project home and will be expanded with more code and project resources over time.

## News

- `2026/07/10`: 🎉🎉🎉 **ATBench has been accepted to COLM 2026!**
- `2026/04/09`: We add **ATBench**, a new 1,000-trajectory release with higher diversity, longer context, broader tool coverage, and a full human audit. The previous 500-case release is renamed to **ATBench500** in the public release lineage.
- `2026/04/09`: **ATBench Engine Coming Soon**. The data generation engine and related tooling will be released in a future update.
- `2026/01/27`: We release the original **ATBench500** benchmark together with the AgentDoG paper.

## Release Zoo

| Release | Status | Cases | Safe | Unsafe | Available Tools | Used Tools | Avg. Turns | Avg. Tokens | Access |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| `ATBench` | Latest | 1,000 | 503 | 497 | 2,084 | 1,954 | 9.01 | 3.95k | [HF config](https://huggingface.co/datasets/AI45Research/ATBench) |
| `ATBench500` | Legacy | 500 | 250 | 250 | 1,575 | 1,357 | 8.97 | 1.52k | [HF config](https://huggingface.co/datasets/AI45Research/ATBench) |

**Available Tools** counts unique tools exposed through per-trajectory tool pools.  
**Used Tools** counts unique tools actually invoked in released trajectories.

<!-- ATBENCH-LEADERBOARD:START -->
## Leaderboard and Recent Evaluations

Only complete evaluations of all 1,000 trajectories in the current `ATBench` release are cross-ranked below; `unsafe` is the positive class. Results on ATBench500, custom splits, subsets, transformed tasks, and official extensions remain visible in the evaluation/use tracker but do not share a rank with the current full-set leaderboard.

### Comparable Full-Set Leaderboard

| Rank | Model / Method | Type | Acc | Prec. | Rec. | F1 | R.S. | F.M. | R.H. |
| ---: | --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 1 | [Qwen3-8B-Instruct + FATE](https://arxiv.org/abs/2605.11882) | Fine-tuned | 77.8 | 80.5 | 78.6 | **79.5** | 49.2 | 18.4 | 43.1 |
| 2 | [AgentDoG 1.5-4B-U (Qwen3.5 Base)](https://arxiv.org/abs/2605.29801) | Guard | **78.4** | 79.8 | 75.7 | 77.7 | 24.1 | 9.5 | 28.4 |
| 3 | [GPT-5.4](https://arxiv.org/abs/2604.02022) | Closed | 73.7 | 68.5 | 87.1 | 76.7 | 33.6 | 13.5 | 30.2 |
| 4 | [Gemini-3.1-Pro](https://arxiv.org/abs/2604.02022) | Closed | 75.5 | 76.1 | 73.8 | 75.0 | 24.8 | 12.6 | 18.5 |
| 5 | [Gemini-3-Flash](https://arxiv.org/abs/2604.02022) | Closed | 76.4 | 79.3 | 71.0 | 74.9 | 18.4 | 8.3 | 15.0 |
| 6 | [AgentDoG 1.5-4B (Qwen3.5 Base)](https://arxiv.org/abs/2605.29801) | Guard | 72.4 | 69.2 | 80.3 | 74.3 | **75.2** | **27.5** | **62.9** |
| 7 | [AgentDoG 1.5-8B (Llama-3.1 Base)](https://arxiv.org/abs/2605.29801) | Guard | 70.9 | 67.1 | 81.2 | 73.5 | 72.9 | 24.6 | 52.5 |
| 8 | [GPT-5.2](https://arxiv.org/abs/2604.02022) | Closed | 69.0 | 65.6 | 79.3 | 71.8 | 29.5 | 12.0 | 26.8 |
| 9 | [AgentDoG-Qwen3-4B](https://arxiv.org/abs/2604.02022) | Guard | 64.0 | 59.2 | 88.9 | 71.1 | 46.8 | 16.5 | 40.6 |
| 10 | [AgentDoG 1.5-2B (Qwen3.5 Base)](https://arxiv.org/abs/2605.29801) | Guard | 69.0 | 70.1 | 65.7 | 67.8 | 68.0 | 24.0 | 53.8 |
| 10 | [Qwen3.5-397B-A17B](https://arxiv.org/abs/2604.02022) | Open | 66.8 | 65.5 | 70.2 | 67.8 | 7.7 | 3.6 | 6.8 |
| 12 | [ShieldAgent](https://arxiv.org/abs/2604.02022) | Guard | 62.5 | 58.0 | 81.4 | 67.7 | - | - | - |
| 13 | [AgentDoG 1.5-0.8B (Qwen3.5 Base)](https://arxiv.org/abs/2605.29801) | Guard | 60.3 | 58.6 | 68.6 | 63.2 | 65.7 | 18.4 | 44.9 |
| 14 | [Llama3.1-8B-Instruct](https://arxiv.org/abs/2604.02022) | Open | 45.3 | 47.3 | **89.5** | 61.9 | 6.2 | 5.8 | 15.5 |
| 15 | [Qwen3-235B-A22B-Instruct-2507](https://arxiv.org/abs/2604.02022) | Open | 59.2 | 58.2 | 63.8 | 60.8 | 7.0 | 11.6 | 26.6 |
| 16 | [NemoGuard](https://arxiv.org/abs/2605.29801) | Guard | 49.9 | 49.5 | 41.6 | 45.2 | - | - | - |
| 17 | [JoySafety](https://arxiv.org/abs/2605.29801) | Guard | 56.9 | 61.7 | 35.0 | 44.7 | - | - | - |
| 18 | [LlamaGuard4-12B](https://arxiv.org/abs/2604.02022) | Guard | 58.1 | 63.8 | 30.9 | 41.7 | - | - | - |
| 19 | [QwQ-32B](https://arxiv.org/abs/2604.02022) | Open | 57.7 | 81.9 | 19.1 | 31.0 | 15.8 | 9.4 | 22.9 |
| 20 | [Qwen3.5-2B](https://arxiv.org/abs/2605.29801) | Open | 59.1 | 74.3 | 19.2 | 30.5 | 7.7 | 6.6 | 11.1 |
| 21 | [Qwen3.5-4B](https://arxiv.org/abs/2604.02022) | Open | 45.9 | 41.2 | 20.7 | 27.6 | 6.6 | 3.0 | 8.2 |
| 22 | [Qwen3-4B-Instruct-2507](https://arxiv.org/abs/2604.02022) | Open | 55.7 | 77.6 | 15.3 | 25.5 | 1.0 | 9.6 | 21.2 |
| 23 | [Qwen2.5-7B-Instruct](https://arxiv.org/abs/2604.02022) | Open | 53.4 | 73.8 | 9.7 | 17.1 | 5.3 | 6.0 | 15.5 |
| 24 | [Qwen3-4B](https://arxiv.org/abs/2604.02022) | Open | 52.6 | 78.0 | 6.4 | 11.9 | 4.4 | 8.2 | 18.3 |
| 25 | [Qwen3.5-0.8B](https://arxiv.org/abs/2605.29801) | Open | 48.6 | 66.7 | 5.9 | 10.8 | 1.3 | 2.9 | 4.7 |
| 26 | [LlamaGuard3-8B](https://arxiv.org/abs/2604.02022) | Guard | 53.1 | **85.7** | 3.8 | 7.3 | - | - | - |
| 27 | [Qwen3-Guard](https://arxiv.org/abs/2604.02022) | Guard | 51.5 | 40.0 | 0.4 | 0.8 | - | - | - |

Ranks use standard competition ranking on the displayed one-decimal F1 value. Ties are ordered by accuracy descending and then model name ascending. `PRISM` has the protocol shape of a rankable full-set evaluation, but remains unranked because its exact best F1 is plot-only rather than numerically reported.

### Recent Papers Evaluating or Using ATBench

| Date | Paper / Method | Relation | Release / Protocol | Reported result | Resources |
| --- | --- | --- | --- | --- | --- |
| 2026-06-18 | [Efficient and Sound Probabilistic Verification for AI Agents](https://arxiv.org/abs/2606.20510) / SDP | Dataset use | 377 trajectories from the legacy AgentDoG-era ATBench (now ATBench500); transformed taint/Datalog task and size filtering | At threshold 0.8: utility 0.983, security 1.000, AUC 0.998; 303 ms vs. Praline 7,227 ms | Paper only |
| 2026-05-31 | [BraveGuard](https://arxiv.org/abs/2606.01166) | Evaluated | Full ATBench500, final held-out evaluation | BraveGuard-Qwen3-Guard-8B: Acc 86.4, Recall 95.2, F1 86.1 | [Code](https://github.com/Yunhao-Feng/BraveGuard), [Model](https://huggingface.co/Yunhao-Feng/BraveGuard) |
| 2026-05-28 | [AgentDoG 1.5](https://arxiv.org/abs/2605.29801) | Ranked | Full current 1,000-case ATBench evaluation; five released model variants | Best coarse result, AgentDoG 1.5-4B-U: Acc 78.4, Precision 79.8, Recall 75.7, F1 77.7; best fine-grained model, AgentDoG 1.5-4B: R.S. 75.2, F.M. 27.5, R.H. 62.9 | [Code](https://github.com/AI45Lab/AgentDoG), [Models](https://huggingface.co/collections/AI45Research/agentdog15) |
| 2026-05-26 | [TRACES](https://arxiv.org/abs/2605.27690) | Evaluated | Current ATBench, stratified 60/20/20 train/validation/test split | TRACES-Llama3.1-8B: Acc 85.5, F1 86.3, Recall 91.9 | Paper only |
| 2026-05-20 | [PRISM](https://arxiv.org/abs/2605.21422) | Evaluated | Private approximately 2K training pool; full current ATBench evaluation | Best at 40% data selection; exact F1 is plot-only | Paper only |
| 2026-05-12 | [On-Policy Self-Evolution via Failure Trajectories](https://arxiv.org/abs/2605.11882) / FATE | Ranked | Full current ATBench external evaluation; no ATBench training or tuning | Acc 77.8, Precision 80.5, Recall 78.6, F1 79.5 | [Code](https://github.com/YinBo0927/FATE), [Project](https://yinbo0927.github.io/FATE/) |
| 2026-05-11 | [Content-Aware Attack Detection in LLM Agent Tool-Call Traffic](https://arxiv.org/abs/2605.11053) | Evaluated | 999 extractable current ATBench cases; label-stratified 70/10/20, three seeds | Random Forest: AUROC 0.784 +/- 0.006, F1 0.669 +/- 0.036 | Paper only |
| 2026-04-16 | [ATBench-Claw and ATBench-Codex](https://arxiv.org/abs/2604.14858) | Official extension | Two separate 500-case domain-customized releases | AgentDoG-Qwen3-4B F1: 89.58 on Claw, 83.79 on Codex | [Claw data](https://huggingface.co/datasets/AI45Research/ATBench-Claw), [Codex data](https://huggingface.co/datasets/AI45Research/ATBench-Codex) |
| 2026-02-16 | [A Trajectory-Based Safety Audit of Clawdbot](https://arxiv.org/abs/2602.14364) | Dataset use | Ten ATBench500-derived cases inside a 34-case audit | No source-specific ATBench score reported | Paper only |
| 2026-01-26 | [AgentDoG](https://arxiv.org/abs/2601.18491) | Evaluated | Full ATBench500 held-out evaluation | AgentDoG-Qwen3-4B: Acc 92.8, Precision 90.5, Recall 95.6, F1 93.0 | [Code](https://github.com/AI45Lab/AgentDoG), [Models](https://huggingface.co/collections/AI45Research/agentdog) |

_Checked through 2026-07-10. Includes papers that evaluate or use a released ATBench configuration._
<!-- ATBENCH-LEADERBOARD:END -->

## Shared Task Definition

Both releases evaluate safety at the **trajectory level**.

Each sample is a complete execution trace containing user requests, agent responses, tool calls, and environment feedback. The evaluator must:

1. predict whether the overall trajectory is `safe` or `unsafe`;
2. for unsafe trajectories, diagnose the trajectory along three taxonomy dimensions:
   - **Risk Source**: where the risk enters the trajectory;
   - **Failure Mode**: how unsafe behavior unfolds;
   - **Real-World Harm**: what downstream harm is produced.

This shared formulation makes the two releases directly comparable while preserving their different scales and schemas.

## Safety Taxonomy

ATBench organizes unsafe trajectories along three diagnosis dimensions: **Risk Source**, **Failure Mode**, and **Real-World Harm**. The taxonomy contains 8 risk-source categories, 14 failure-mode categories, and 10 real-world-harm categories, and serves as the shared fine-grained label space for benchmark construction and analysis.

<p align="center">
  <img src="assets/safety_taxonomy.png" alt="ATBench three-dimensional safety taxonomy" width="100%">
</p>

## Latest Release: ATBench

**ATBench** is the current main release introduced in [ATBench: A Diverse and Realistic Agent Trajectory Benchmark for Safety Evaluation and Diagnosis](https://arxiv.org/abs/2604.02022).

<p align="center">
  <img src="assets/teaser.png" alt="ATBench teaser" width="100%">
</p>

- **Scale**: 1,000 trajectories
- **Label balance**: 503 safe / 497 unsafe
- **Interaction horizon**: 9.01 average turns
- **Tool coverage**: 2,084 available tools and 1,954 invoked tools
- **Quality control**: rule-based filtering, LLM-based filtering, and full human audit

### Model Performance on ATBench

The figure below compares representative model performance on prior agent-safety benchmarks and **ATBench**. For most models, performance is lower on **ATBench**, indicating higher overall difficulty.

<p align="center">
  <img src="assets/model_performance.png" alt="Model performance comparison including ATBench" width="100%">
</p>

### Generation Pipeline

ATBench is constructed with a taxonomy-guided data generation engine designed to maximize diversity under realism constraints. Starting from sampled risks and candidate tool pools, the planner produces a trajectory blueprint, which is then instantiated through query generation, risk injection, tool call simulation, tool response simulation, and agent response generation. A validation layer further applies rule-based and LLM-based filtering before release.

<p align="center">
  <img src="https://huggingface.co/datasets/AI45Research/ATBench/resolve/main/figures/ATBench/data_generation_pipeline.png" alt="ATBench data generation pipeline" width="100%">
</p>

### Representative Cases

The figure below shows two representative unsafe cases from the latest ATBench release. In both examples, the model can often detect that the trajectory is unsafe, but still struggles to recover the correct fine-grained cause.

<p align="center">
  <img src="https://huggingface.co/datasets/AI45Research/ATBench/resolve/main/figures/ATBench/case_studies.png" alt="Representative ATBench case studies" width="100%">
</p>

## Legacy Release: ATBench500

**ATBench500** is the original release from the AgentDoG project. It remains available for backward compatibility and historical comparison.

- **Scale**: 500 trajectories
- **Label balance**: 250 safe / 250 unsafe
- **Interaction horizon**: 8.97 average turns
- **Tool coverage**: 1,575 available tools
- **Paper**: [AgentDoG: A Diagnostic Guardrail Framework for AI Agent Safety and Security](https://arxiv.org/abs/2601.18491)

The figure below shows the fine-grained taxonomy distribution for the original **ATBench500** release:

<p align="center">
  <img src="https://huggingface.co/datasets/AI45Research/ATBench/resolve/main/figures/ATBench500/benchmark_distribution.png" alt="ATBench500 taxonomy distribution" width="100%">
</p>

## Quick Start

```python
from datasets import load_dataset

atbench = load_dataset("AI45Research/ATBench", "ATBench", split="test")
atbench500 = load_dataset("AI45Research/ATBench", "ATBench500", split="test")
```

## Citation

If you use this benchmark family, please cite the corresponding release.

```bibtex
@article{li2026atbench,
  title={ATBench: A Diverse and Realistic Agent Trajectory Benchmark for Safety Evaluation and Diagnosis},
  author={Yu Li and Haoyu Luo and Yuejin Xie and Yuqian Fu and Zhonghao Yang and Shuai Shao and Qihan Ren and Wanying Qu and Yanwei Fu and Yujiu Yang and Jing Shao and Xia Hu and Dongrui Liu},
  journal={arXiv preprint arXiv:2604.02022},
  year={2026},
  doi={10.48550/arXiv.2604.02022},
  url={https://arxiv.org/abs/2604.02022}
}

@article{liu2026agentdog,
  title={AgentDoG: A Diagnostic Guardrail Framework for AI Agent Safety and Security},
  author={Yu Li and Haoyu Luo and Yuejin Xie and Jiapeng Gu and Yuhan Wang and Yanwei Fu and Yujiu Yang and Jing Shao and Xia Hu and Dongrui Liu},
  journal={arXiv preprint arXiv:2601.18491},
  year={2026},
  url={https://arxiv.org/abs/2601.18491}
}
```
