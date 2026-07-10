# ATBench Leaderboard and Evaluation Tracker Design

Date: 2026-07-10
Status: approved for Repo-first implementation

## 1. Goal

Add a two-table section to the ATBench GitHub README first:

1. an official leaderboard for comparable full-set evaluations on the current
   1,000-trajectory ATBench release;
2. a dated tracker limited to papers that genuinely evaluate or use a released
   ATBench configuration, including results that are not eligible for the
   official ranking.

The presentation follows the compact, paper-first style requested by the user
and previewed in the approved two-table mockup. The tables are static Markdown
so that they render reliably on GitHub. Synchronizing the approved block to the
`AI45Research/ATBench` Hugging Face dataset card is explicitly deferred to a
later step after the repository version is implemented, published, and checked.

## 2. Scope

### In scope

- Update `/Users/liyu/Documents/AILab/ATbench/README.md`.
- Add this exact News item as the first bullet under `## News`:

  ```markdown
  - `2026/07/10`: 🎉🎉🎉 **ATBench has been accepted to COLM 2026!**
  ```
- Use absolute links for papers, code, models, and datasets so a later
  Hugging Face synchronization can reuse the reviewed table block.
- Mark the tracker as checked through `2026-07-10`.

### Out of scope

- A hosted submission backend, automatic evaluation service, or dynamic web
  leaderboard.
- Ranking results from ATBench500, custom train/test splits, filtered subsets,
  or ATBench-Claw/ATBench-Codex together with the current ATBench release.
- Treating search snippets, repository claims, or digitized plot coordinates
  as exact official scores.
- Adding unverified “ATBench-style” synthetic tests that do not run the
  released dataset.
- Updating or publishing the Hugging Face dataset card in this Repo-first
  phase; that synchronization is a later, separately verified step.

## 3. Placement and presentation

Insert a `## Leaderboard and Recent Evaluations` section after `## Release Zoo`
in the GitHub README. This keeps the benchmark releases and the evidence about
their use adjacent and makes the leaderboard visible before the long task and
schema descriptions.

The section contains:

- a short protocol note;
- Table 1, sorted by F1 descending;
- a short comparability note;
- Table 2 with exactly 10 evaluation/use papers, sorted by first arXiv
  publication date descending;
- a short maintenance note.

Use standard Markdown tables, linked method names, bold for the best score in
each Table 1 metric, and no custom HTML/CSS. Values in Table 1 are percentages
with one decimal place. Table 2 can use compact decimals or percentages that
match the source paper, but the unit must be explicit in the result cell.
Citation-only evidence remains documented in Section 5.3 for audit coverage and
is not rendered as a public Table 2 row.

## 4. Table 1: Official ATBench Leaderboard

### 4.1 Columns

| Column | Meaning |
| --- | --- |
| Rank | Rank by coarse unsafe-class F1, descending |
| Model / Method | Evaluator name, linked to its paper or primary resource |
| Type | `Closed`, `Open`, `Guard`, or `Fine-tuned` |
| Acc | Binary safe/unsafe accuracy |
| Prec. | Precision with unsafe as the positive class |
| Rec. | Recall with unsafe as the positive class |
| F1 | Binary F1 with unsafe as the positive class |
| R.S. | Risk Source accuracy on unsafe trajectories |
| F.M. | Failure Mode accuracy on unsafe trajectories |
| R.H. | Real-World Harm accuracy on unsafe trajectories |

### 4.2 Eligibility rules

A row is rankable only when all of the following are true:

1. It evaluates the current `ATBench` configuration containing all 1,000
   released trajectories.
2. It uses the released labels only for evaluation, not for training,
   validation, threshold tuning, or model selection.
3. It reports the official trajectory-level binary task with unsafe as the
   positive class.
4. Its metrics are explicitly reported as numbers in a paper table, paper
   text, or reproducible official artifact.
5. Missing or unparsable predictions follow the benchmark's evaluation
   contract rather than being silently removed.

Results using `ATBench500`, a custom split, a subset, a transformed task, or a
different metric stay visible in Table 2 but receive no shared rank.

### 4.3 Initial ranked rows

The initial leaderboard has 27 comparable rows: 17 from Table 2 of the ATBench
paper, one from Table 4 of FATE, and nine newly reported in Tables 2 and 3 of
AgentDoG 1.5. The nine AgentDoG 1.5-paper additions comprise five AgentDoG 1.5
variants and four newly evaluated baselines. This keeps the leaderboard complete
for every explicit full-1,000-case result found in the paper audit rather than
showing only newly proposed methods.

Ranks use standard competition ranking on the displayed one-decimal F1 value:
equal F1 values share a rank and the following rank is skipped. Tied rows are
displayed by accuracy descending and then model name ascending. The `Source`
column below records design-time provenance; it is omitted from the rendered
table because the rendered model/method names carry the same links.

| Rank | Model / Method | Type | Acc | Prec. | Rec. | F1 | R.S. | F.M. | R.H. | Source |
| ---: | --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | --- |
| 1 | Qwen3-8B-Instruct + FATE | Fine-tuned | 77.8 | 80.5 | 78.6 | 79.5 | 49.2 | 18.4 | 43.1 | [FATE](https://arxiv.org/abs/2605.11882) |
| 2 | AgentDoG 1.5-4B-U (Qwen3.5 Base) | Guard | 78.4 | 79.8 | 75.7 | 77.7 | 24.1 | 9.5 | 28.4 | [AgentDoG 1.5](https://arxiv.org/abs/2605.29801) |
| 3 | GPT-5.4 | Closed | 73.7 | 68.5 | 87.1 | 76.7 | 33.6 | 13.5 | 30.2 | [ATBench](https://arxiv.org/abs/2604.02022) |
| 4 | Gemini-3.1-Pro | Closed | 75.5 | 76.1 | 73.8 | 75.0 | 24.8 | 12.6 | 18.5 | ATBench |
| 5 | Gemini-3-Flash | Closed | 76.4 | 79.3 | 71.0 | 74.9 | 18.4 | 8.3 | 15.0 | ATBench |
| 6 | AgentDoG 1.5-4B (Qwen3.5 Base) | Guard | 72.4 | 69.2 | 80.3 | 74.3 | 75.2 | 27.5 | 62.9 | AgentDoG 1.5 |
| 7 | AgentDoG 1.5-8B (Llama-3.1 Base) | Guard | 70.9 | 67.1 | 81.2 | 73.5 | 72.9 | 24.6 | 52.5 | AgentDoG 1.5 |
| 8 | GPT-5.2 | Closed | 69.0 | 65.6 | 79.3 | 71.8 | 29.5 | 12.0 | 26.8 | ATBench |
| 9 | AgentDoG-Qwen3-4B | Guard | 64.0 | 59.2 | 88.9 | 71.1 | 46.8 | 16.5 | 40.6 | ATBench |
| 10 | AgentDoG 1.5-2B (Qwen3.5 Base) | Guard | 69.0 | 70.1 | 65.7 | 67.8 | 68.0 | 24.0 | 53.8 | AgentDoG 1.5 |
| 10 | Qwen3.5-397B-A17B | Open | 66.8 | 65.5 | 70.2 | 67.8 | 7.7 | 3.6 | 6.8 | ATBench |
| 12 | ShieldAgent | Guard | 62.5 | 58.0 | 81.4 | 67.7 | - | - | - | ATBench |
| 13 | AgentDoG 1.5-0.8B (Qwen3.5 Base) | Guard | 60.3 | 58.6 | 68.6 | 63.2 | 65.7 | 18.4 | 44.9 | AgentDoG 1.5 |
| 14 | Llama3.1-8B-Instruct | Open | 45.3 | 47.3 | 89.5 | 61.9 | 6.2 | 5.8 | 15.5 | ATBench |
| 15 | Qwen3-235B-A22B-Instruct-2507 | Open | 59.2 | 58.2 | 63.8 | 60.8 | 7.0 | 11.6 | 26.6 | ATBench |
| 16 | NemoGuard | Guard | 49.9 | 49.5 | 41.6 | 45.2 | - | - | - | AgentDoG 1.5 |
| 17 | JoySafety | Guard | 56.9 | 61.7 | 35.0 | 44.7 | - | - | - | AgentDoG 1.5 |
| 18 | LlamaGuard4-12B | Guard | 58.1 | 63.8 | 30.9 | 41.7 | - | - | - | ATBench |
| 19 | QwQ-32B | Open | 57.7 | 81.9 | 19.1 | 31.0 | 15.8 | 9.4 | 22.9 | ATBench |
| 20 | Qwen3.5-2B | Open | 59.1 | 74.3 | 19.2 | 30.5 | 7.7 | 6.6 | 11.1 | AgentDoG 1.5 |
| 21 | Qwen3.5-4B | Open | 45.9 | 41.2 | 20.7 | 27.6 | 6.6 | 3.0 | 8.2 | ATBench |
| 22 | Qwen3-4B-Instruct-2507 | Open | 55.7 | 77.6 | 15.3 | 25.5 | 1.0 | 9.6 | 21.2 | ATBench |
| 23 | Qwen2.5-7B-Instruct | Open | 53.4 | 73.8 | 9.7 | 17.1 | 5.3 | 6.0 | 15.5 | ATBench |
| 24 | Qwen3-4B | Open | 52.6 | 78.0 | 6.4 | 11.9 | 4.4 | 8.2 | 18.3 | ATBench |
| 25 | Qwen3.5-0.8B | Open | 48.6 | 66.7 | 5.9 | 10.8 | 1.3 | 2.9 | 4.7 | AgentDoG 1.5 |
| 26 | LlamaGuard3-8B | Guard | 53.1 | 85.7 | 3.8 | 7.3 | - | - | - | ATBench |
| 27 | Qwen3-Guard | Guard | 51.5 | 40.0 | 0.4 | 0.8 | - | - | - | ATBench |

The bold cells in the rendered table are fixed by these maxima: Acc 78.4
(AgentDoG 1.5-4B-U), Precision 85.7 (LlamaGuard3-8B), Recall 89.5
(Llama3.1-8B-Instruct), F1 79.5 (FATE), and R.S./F.M./R.H. 75.2/27.5/62.9
(AgentDoG 1.5-4B).

`PRISM` is eligible in protocol shape because it evaluates the full current
ATBench release without training on ATBench. It is not initially ranked because
the paper states that 40% selection is best but only plots the F1 values without
numeric labels. It remains in Table 2 until an exact author-confirmed value is
available.

## 5. Table 2: Recent Papers Evaluating or Using ATBench

### 5.1 Columns

| Column | Meaning |
| --- | --- |
| Date | First arXiv publication date |
| Paper / Method | Linked paper title and method name |
| Relation | `Ranked`, `Evaluated`, `Official extension`, or `Dataset use` |
| Release / Protocol | ATBench version, sample count, and split or transformation |
| Reported result | Most informative ATBench result, or `No ATBench result` |
| Resources | Verified official code, model, project, or dataset links |

### 5.2 Initial tracker rows

The rendered initial tracker contains exactly the following 10 full-text-
verified papers that evaluate or use an ATBench release, sorted by first arXiv
publication date descending:

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
| 2026-01-27 | [AgentDoG](https://arxiv.org/abs/2601.18491) | Evaluated | Full ATBench500 held-out evaluation | AgentDoG-Qwen3-4B: Acc 92.8, Precision 90.5, Recall 95.6, F1 93.0 | [Code](https://github.com/AI45Lab/AgentDoG), [Models](https://huggingface.co/collections/AI45Research/agentdog) |

### 5.3 Citation-only and extension-only audit coverage

The following six full-text-verified papers are preserved in the evidence audit
but deliberately excluded from the rendered initial tracker because they do not
evaluate or use an ATBench release:

| Date | Paper / Method | Audited relationship | Reason not rendered |
| --- | --- | --- | --- |
| 2026-07-02 | [Safety Testing LLM Agents at Scale](https://arxiv.org/abs/2607.01793) / VERA | Direct citation to main ATBench | Cites `arXiv:2604.02022`; no ATBench evaluation or dataset use |
| 2026-06-09 | [AgentCanary](https://arxiv.org/abs/2606.10484) | Direct citation to main ATBench | Cites `arXiv:2604.02022`; no ATBench evaluation or dataset use |
| 2026-06-06 | [Online Agent-as-a-Judge](https://arxiv.org/abs/2606.08200) | Direct citation to main ATBench | Cites `arXiv:2604.02022`; no ATBench evaluation or dataset use |
| 2026-06-02 | [RUBAS](https://arxiv.org/abs/2606.04051) | Direct citation to main ATBench | Cites `arXiv:2604.02022`; no ATBench evaluation or dataset use |
| 2026-05-30 | [TRACE: Trajectory Risk-Aware Compression for Long-Horizon Agent Safety](https://arxiv.org/abs/2606.00611) | Direct citation to main ATBench | Cites `arXiv:2604.02022`; experiments use ASSEBench, Pre-Ex-Bench, R-Judge, and LongSafety instead of ATBench |
| 2026-05-21 | [Boiling the Frog: A Multi-Turn Benchmark for Agentic Safety](https://arxiv.org/abs/2605.22643) | Citation to extension only | Cites ATBench-Claw/ATBench-Codex (`arXiv:2604.14858`), not the main ATBench paper; no ATBench release evaluation or use |

VERA, AgentCanary, Online Agent-as-a-Judge, RUBAS, and TRACE are citation-only
direct citations to the main ATBench paper. Boiling the Frog cites only the
official extension. None is a rendered Table 2 evaluation/use row.

### 5.4 Direct-citation coverage statement

As of 2026-07-10, PDF full-text checks establish a lower bound of 13 papers
whose current public versions directly cite `arXiv:2604.02022`. Semantic
Scholar links seven of them. The six additional PDF-verified citations are the
latest AgentDoG revision, the official ATBench-Claw/ATBench-Codex extension,
FATE, BraveGuard, AgentDoG 1.5, and TRACE. Their reference lists explicitly name
the ATBench paper or arXiv identifier even though the citation graph does not
link them to the target record.

The rendered tracker also includes papers that use the legacy ATBench data while
citing AgentDoG or the Hugging Face dataset rather than `arXiv:2604.02022`;
their `Relation` cells say `Dataset use`, not `Ranked`. `Boiling the Frog`
remains only in the audit subsection because it references the official
ATBench-Claw/ATBench-Codex report rather than the main ATBench paper; it is not
counted in the 13 direct citations to the main ATBench paper.

The README must describe 13 as a verified lower bound rather than a complete
global citation count because Google Scholar was inaccessible behind CAPTCHA,
while OpenAlex and DataCite returned no useful citing records.

### 5.5 Other audited exclusions

The initial public tracker omits two code-only candidates found during the
repository audit:

- ProcessGuard reports a full-1,000-case result, but its training manifest
  references an `atbench_asse1600` input and does not establish source-disjoint
  evaluation. It is not presented as a clean benchmark result.
- TraceHound has no accompanying paper, and its headline result comes from an
  864-case summer-camp mixture while its fine-grained experiment uses an
  `ATBench300` subset. Neither result is labeled as current full ATBench.

Adapters, data loaders, smoke tests, and synthetic “ATBench-style” cases that do
not evaluate a released ATBench configuration also remain out of scope. These
exclusions can be revisited if the authors publish a citable report with a
source-disjoint, reproducible protocol.

## 6. Data and maintenance rules

- Treat the paper PDF and official artifact as authoritative; do not copy
  metrics from search snippets or third-party summaries.
- Record the exact benchmark release and evaluation split before adding a
  result.
- Add a new Table 1 row only after checking every eligibility condition in
  Section 4.2.
- Add a paper to Table 2 only when it evaluates or uses a released ATBench
  configuration; include enough protocol detail to explain why non-comparable
  results are not ranked.
- Preserve citation-only and extension-only discoveries in the design audit,
  not as rendered Table 2 rows.
- Use the first arXiv publication date for tracker ordering and the latest PDF
  version for content verification.
- Use `-` for unsupported metrics and `Not reported` when the paper supports a
  metric but does not provide a numeric value.
- Keep matching `<!-- ATBENCH-LEADERBOARD:START -->` and
  `<!-- ATBENCH-LEADERBOARD:END -->` comments around the GitHub section so a
  later Hugging Face synchronization can compare or replace the block safely.

## 7. Repo-first publication and deferred synchronization flow

Current Repo-first phase:

1. Build and review the complete Markdown section in the GitHub README.
2. Verify the 27-row leaderboard, 10-row evaluation/use table, links, ordering,
   and exact COLM 2026 News wording locally.
3. Commit and push the GitHub change.
4. Fetch the public GitHub README and verify that the News item, headings, FATE
   row, AgentDoG 1.5 rows, and all 10 evaluation/use rows are present.

Deferred Hugging Face phase, performed only after the GitHub version is public
and verified:

1. Copy the reviewed marker-delimited block byte-for-byte to the Hugging Face
   README.
2. Keep the Hugging Face YAML front matter unchanged.
3. Verify that both blocks are identical after normalizing only line endings.
4. Publish the Hugging Face README through the authenticated Hub API.
5. Fetch the remote card and verify the synchronized block independently.

No generator is added in this iteration. A small static section is easier to
audit and avoids introducing maintenance code before recurring submissions
justify it.

## 8. Verification

Before publishing:

- check Table 1 has exactly 27 ranked rows and monotonically non-increasing F1;
- check the two F1 67.8 rows share rank 10, appear in the specified tie order,
  and are followed by rank 12;
- check Table 2 has exactly 10 rows and is monotonically non-increasing by first
  arXiv publication date;
- independently recompute every displayed rank from the row values;
- check every tracker row has a relation and an explicit release/protocol;
- confirm no citation-only or extension-only audit row is rendered in Table 2;
- confirm current ATBench, ATBench500, and extension results never share a
  rank;
- run bounded HTTP checks on all paper, code, model, project, and dataset URLs;
- inspect `git diff --check` and the final Markdown diff;
- verify the remote GitHub README after publication.

The deferred Hugging Face phase will separately compare the marker-delimited
blocks for exact equality and verify the remote dataset card; those checks are
not acceptance gates for this Repo-first phase.

## 9. Acceptance criteria

The Repo-first phase is complete when the public GitHub README contains the
exact COLM 2026 News item and both tables; Table 1 has 27 rows with FATE ranked
first on the current full-set ATBench leaderboard at F1 79.5; AgentDoG 1.5
contributes all five released variants; Table 2 has exactly the 10 verified
evaluation/use papers with clear release/protocol labels; citation-only and
extension-only papers remain out of the rendered tracker; the separately
documented 13-paper direct-citation lower bound remains accurate; and every
linked resource resolves. Updating the Hugging Face card is explicitly
deferred and is not required to accept this phase.
