# ATBench Repository Leaderboard Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update the public ATBench GitHub README with a polished COLM 2026 acceptance announcement, a comparable full-1,000-case leaderboard, and a table limited to papers that actually evaluate or use an ATBench release.

**Architecture:** Keep the update as static Markdown in `README.md`, immediately after the existing Release Zoo. Use the evidence matrix in the approved design as the single source for leaderboard values, while narrowing the second table to ten verified evaluation/use papers and excluding citation-only rows. The GitHub README is implemented and published first; Hugging Face synchronization is explicitly deferred.

**Tech Stack:** GitHub-flavored Markdown, shell/awk structural checks, bounded HTTP link checks, Git.

---

### Task 1: Record the approved scope refinement

> Completed in commit `dd0e06d` (`docs: plan Repo-first leaderboard update`). Do not repeat this task or recreate its commit.

**Files:**
- Modify: `docs/superpowers/specs/2026-07-10-atbench-leaderboard-design.md`
- Create: `docs/superpowers/plans/2026-07-10-atbench-repo-leaderboard.md`

- [x] **Step 1: Update the Repo-first scope**

The design now makes GitHub the first publication target and explicitly defers Hugging Face. It records this exact News wording:

```markdown
- `2026/07/10`: 🎉🎉🎉 **ATBench has been accepted to COLM 2026!**
```

- [x] **Step 2: Narrow Table 2 to verified evaluation/use papers**

The rendered tracker is limited to these ten rows in descending first-arXiv-date order:

```text
2606.20510 SDP
2606.01166 BraveGuard
2605.29801 AgentDoG 1.5
2605.27690 TRACES
2605.21422 PRISM
2605.11882 FATE
2605.11053 Content-Aware Attack Detection
2604.14858 ATBench-Claw / ATBench-Codex
2602.14364 Clawdbot audit
2601.18491 AgentDoG
```

VERA, AgentCanary, Online Agent-as-a-Judge, RUBAS, TRACE, and Boiling the Frog remain in the design audit only.

- [x] **Step 3: Verify the design has no stale rendered-row count**

The design verification and acceptance sections now require exactly 10 rendered evaluation/use rows. The 13-paper direct-citation lower bound remains internal audit evidence and is not public README content.

- [x] **Step 4: Commit the scope refinement and initial implementation plan**

Recorded in `dd0e06d`. Executors begin at Task 2.

### Task 2: Add the News item and two README tables

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Confirm the new content is absent before editing**

Run:

```bash
! rg -q 'ATBench has been accepted to COLM 2026' README.md
! rg -q '^## Leaderboard and Recent Evaluations$' README.md
```

Expected: exit 0 because both negated searches find no existing content.

- [ ] **Step 2: Add the exact COLM 2026 News item**

Insert this line as the first bullet under `## News`:

```markdown
- `2026/07/10`: 🎉🎉🎉 **ATBench has been accepted to COLM 2026!**
```

- [ ] **Step 3: Insert the exact leaderboard and evaluation/use block**

Insert the following complete block after the two Release Zoo definition notes and before `## Shared Task Definition`. Do not edit values, links, ordering, bold cells, notes, headings, or markers.

```markdown
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
| 2026-01-27 | [AgentDoG](https://arxiv.org/abs/2601.18491) | Evaluated | Full ATBench500 held-out evaluation | AgentDoG-Qwen3-4B: Acc 92.8, Precision 90.5, Recall 95.6, F1 93.0 | [Code](https://github.com/AI45Lab/AgentDoG), [Models](https://huggingface.co/collections/AI45Research/agentdog) |

_Checked through 2026-07-10. This table includes only papers that evaluate or use a released ATBench configuration; citation-only papers remain in the internal evidence audit._
<!-- ATBENCH-LEADERBOARD:END -->
```

- [ ] **Step 4: Review the rendered scope**

Run these exact exclusion checks; the citation-only `TRACE` paper is identified
by `2606.00611` so the allowed `TRACES` evaluation row is not rejected:

```bash
! rg -q 'Cites only|Cites extension' README.md
! rg -q '2607\.01793|2606\.10484|2606\.08200|2606\.04051|2606\.00611|2605\.22643' README.md
! rg -q '13-paper direct-citation|verified lower bound of 13' README.md
```

Expected: all three negated searches exit 0. The structural commands in Task 3
separately enforce 27 leaderboard rows and exactly 10 evaluation/use rows.

- [ ] **Step 5: Commit the README update**

Run:

```bash
git add README.md
git diff --cached --check
test "$(git diff --cached --name-only)" = "README.md"
git commit -m "docs: add ATBench leaderboard and evaluation tracker"
```

Expected: the commit contains only `README.md`.

### Task 3: Verify and publish the Repo update

**Files:**
- Verify: `README.md`
- Verify: `docs/superpowers/specs/2026-07-10-atbench-leaderboard-design.md`
- Verify: `docs/superpowers/plans/2026-07-10-atbench-repo-leaderboard.md`

- [ ] **Step 1: Run the complete structural table checks**

Run these commands from the repository root. `README_PATH` exists only to permit smoke-testing the validator against the exact embedded block; normal execution uses `README.md`.

```bash
readme="${README_PATH:-README.md}"

awk '
function clean(value) {
  gsub(/^[[:space:]]+|[[:space:]]+$/, "", value)
  gsub(/\*\*/, "", value)
  return value
}
BEGIN {
  active = 0
  rows = 0
  failed = 0
}
/^### Comparable Full-Set Leaderboard$/ {
  active = 1
  next
}
/^### Recent Papers Evaluating or Using ATBench$/ {
  active = 0
}
active && /^\| [0-9]+ \|/ {
  split($0, column, "|")
  rows++
  rank = clean(column[2]) + 0
  method = clean(column[3])
  f1 = clean(column[8]) + 0

  if (rows > 1 && f1 > previous_f1) {
    printf "F1 order error at row %d: %.1f after %.1f\n", rows, f1, previous_f1 > "/dev/stderr"
    failed = 1
  }

  expected_rank = (rows == 1 ? 1 : (f1 == previous_f1 ? previous_rank : rows))
  if (rank != expected_rank) {
    printf "Rank error at row %d: got %d, expected %d\n", rows, rank, expected_rank > "/dev/stderr"
    failed = 1
  }

  ranks[rows] = rank
  scores[rows] = f1
  methods[rows] = method
  previous_rank = rank
  previous_f1 = f1
}
END {
  if (rows != 27) {
    printf "Leaderboard row-count error: got %d, expected 27\n", rows > "/dev/stderr"
    failed = 1
  }
  if (!(scores[10] == 67.8 && scores[11] == 67.8 &&
        ranks[10] == 10 && ranks[11] == 10 && ranks[12] == 12)) {
    print "Competition-tie error around F1 67.8" > "/dev/stderr"
    failed = 1
  }
  if (methods[10] !~ /AgentDoG 1\.5-2B/ ||
      methods[11] !~ /Qwen3\.5-397B-A17B/) {
    print "Tie-order error for the two F1 67.8 rows" > "/dev/stderr"
    failed = 1
  }
  if (failed) {
    exit 1
  }
  printf "Leaderboard rows=%d; rank/F1 order=OK; F1 67.8 ranks=%d,%d; following rank=%d\n",
         rows, ranks[10], ranks[11], ranks[12]
}
' "$readme"

awk '
function clean(value) {
  gsub(/^[[:space:]]+|[[:space:]]+$/, "", value)
  return value
}
BEGIN {
  active = 0
  rows = 0
  failed = 0
  expected[1] = "2606.20510"
  expected[2] = "2606.01166"
  expected[3] = "2605.29801"
  expected[4] = "2605.27690"
  expected[5] = "2605.21422"
  expected[6] = "2605.11882"
  expected[7] = "2605.11053"
  expected[8] = "2604.14858"
  expected[9] = "2602.14364"
  expected[10] = "2601.18491"
}
/^### Recent Papers Evaluating or Using ATBench$/ {
  active = 1
  next
}
/^<!-- ATBENCH-LEADERBOARD:END -->$/ {
  active = 0
}
active && /^\| 2026-/ {
  split($0, column, "|")
  rows++
  date = clean(column[2])
  date_key = date
  gsub(/-/, "", date_key)
  date_key += 0

  if (rows > 1 && date_key > previous_date_key) {
    printf "Date-order error at row %d: %s after %s\n", rows, date, previous_date > "/dev/stderr"
    failed = 1
  }
  if (index($0, expected[rows]) == 0) {
    printf "Paper-order error at row %d: expected arXiv %s\n", rows, expected[rows] > "/dev/stderr"
    failed = 1
  }
  if ($0 ~ /\| Cites (only|extension) \|/) {
    printf "Citation-only relation rendered at row %d\n", rows > "/dev/stderr"
    failed = 1
  }

  previous_date = date
  previous_date_key = date_key
}
END {
  if (rows != 10) {
    printf "Evaluation/use row-count error: got %d, expected 10\n", rows > "/dev/stderr"
    failed = 1
  }
  if (failed) {
    exit 1
  }
  printf "Evaluation/use rows=%d; date order=OK; exact paper order=OK\n", rows
}
' "$readme"
```

Expected output:

```text
Leaderboard rows=27; rank/F1 order=OK; F1 67.8 ranks=10,10; following rank=12
Evaluation/use rows=10; date order=OK; exact paper order=OK
```

- [ ] **Step 2: Check links and Markdown whitespace**

Run:

```bash
git diff --check
rg -o 'https://[^[:space:])>"}]+' README.md | sort -u | xargs -n1 -P8 sh -c 'u="$1"; code=$(curl -L -sS --max-time 20 -o /dev/null -w "%{http_code}" "$u"); printf "%s %s\n" "$code" "$u"; [ "$code" = 200 ]' sh
```

The URL character class deliberately excludes Markdown, HTML, and BibTeX closing delimiters. Expected: `git diff --check` is silent, the URL command has no xargs/shell quoting errors, and every line begins with HTTP `200`.

- [ ] **Step 3: Confirm only unrelated untracked files remain**

Run:

```bash
git status --short
```

Expected: only `.DS_Store` and `COLM Rebuttal/` are untracked; no tracked file is modified or staged.

- [ ] **Step 4: Push and verify the public README**

Run the push, then fetch and assert against the repository's exact raw README URL:

```bash
set -euo pipefail

git push origin main

raw_url='https://raw.githubusercontent.com/LiYu0524/ATbench/main/README.md'
raw_readme="$(curl -fsSL --max-time 30 "$raw_url")"

rg -Fqx -- '- `2026/07/10`: 🎉🎉🎉 **ATBench has been accepted to COLM 2026!**' <<< "$raw_readme"
rg -Fqx '## Leaderboard and Recent Evaluations' <<< "$raw_readme"
rg -Fq 'Qwen3-8B-Instruct + FATE' <<< "$raw_readme"
rg -Fq 'AgentDoG 1.5-4B-U' <<< "$raw_readme"

awk '
BEGIN {
  active = 0
  rows = 0
  expected[1] = "2606.20510"
  expected[2] = "2606.01166"
  expected[3] = "2605.29801"
  expected[4] = "2605.27690"
  expected[5] = "2605.21422"
  expected[6] = "2605.11882"
  expected[7] = "2605.11053"
  expected[8] = "2604.14858"
  expected[9] = "2602.14364"
  expected[10] = "2601.18491"
}
/^### Recent Papers Evaluating or Using ATBench$/ {
  active = 1
  next
}
/^<!-- ATBENCH-LEADERBOARD:END -->$/ {
  active = 0
}
active && /^\| 2026-/ {
  rows++
  if (index($0, expected[rows]) == 0) {
    printf "Remote paper-order error at row %d: expected arXiv %s\n", rows, expected[rows] > "/dev/stderr"
    failed = 1
  }
}
END {
  if (rows != 10) {
    printf "Remote evaluation/use row-count error: got %d, expected 10\n", rows > "/dev/stderr"
    failed = 1
  }
  if (failed) {
    exit 1
  }
  print "Remote README assertions passed; evaluation/use rows=10"
}
' <<< "$raw_readme"
```

Expected final line:

```text
Remote README assertions passed; evaluation/use rows=10
```

Hugging Face synchronization remains deferred and is not part of this plan's completion gate.
