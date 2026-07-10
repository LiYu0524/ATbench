# ATBench Repository Leaderboard Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update the public ATBench GitHub README with a polished COLM 2026 acceptance announcement, a comparable full-1,000-case leaderboard, and a table limited to papers that actually evaluate or use an ATBench release.

**Architecture:** Keep the update as static Markdown in `README.md`, immediately after the existing Release Zoo. Use the evidence matrix in the approved design as the single source for leaderboard values, while narrowing the second table to ten verified evaluation/use papers and excluding citation-only rows. Record the scope refinement in the design document before publishing.

**Tech Stack:** GitHub-flavored Markdown, shell/awk structural checks, bounded HTTP link checks, Git.

---

### Task 1: Record the approved scope refinement

**Files:**
- Modify: `docs/superpowers/specs/2026-07-10-atbench-leaderboard-design.md`
- Create: `docs/superpowers/plans/2026-07-10-atbench-repo-leaderboard.md`

- [ ] **Step 1: Update the Repo-first scope**

Change the implementation scope to GitHub first, with Hugging Face explicitly deferred. Add the new News wording:

```markdown
- `2026/07/10`: 🎉🎉🎉 **ATBench has been accepted to COLM 2026!**
```

- [ ] **Step 2: Narrow Table 2 to verified evaluation/use papers**

Keep exactly these ten rows, in descending first-arXiv-date order:

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

Remove VERA, AgentCanary, Online Agent-as-a-Judge, RUBAS, TRACE, and Boiling the Frog from the rendered initial tracker. Preserve their audit evidence in the design document as known citation-only or extension-only papers, not as rendered evaluation rows.

- [ ] **Step 3: Verify the design has no stale rendered-row count**

Run:

```bash
rg -n 'exactly (16|15|14) rows|Table 2 has exactly' docs/superpowers/specs/2026-07-10-atbench-leaderboard-design.md
```

Expected: the rendered Table 2 verification requirement says exactly 10 rows; any 13-paper citation coverage statement remains clearly separate from the rendered evaluation table.

- [ ] **Step 4: Commit the scope refinement and implementation plan**

Run:

```bash
git add docs/superpowers/specs/2026-07-10-atbench-leaderboard-design.md docs/superpowers/plans/2026-07-10-atbench-repo-leaderboard.md
git diff --cached --check
git commit -m "docs: plan Repo-first leaderboard update"
```

Expected: the commit contains exactly the design refinement and this implementation plan.

### Task 2: Add the News item and two README tables

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Confirm the new content is absent before editing**

Run:

```bash
! rg -q 'ATBench has been accepted to COLM 2026' README.md
! rg -q '^## Leaderboard and Recent Evaluations' README.md
```

Expected: exit 0 because both negated searches find no existing content.

- [ ] **Step 2: Add the COLM 2026 News item**

Insert this as the first bullet under `## News`:

```markdown
- `2026/07/10`: 🎉🎉🎉 **ATBench has been accepted to COLM 2026!**
```

- [ ] **Step 3: Add the comparable leaderboard after Release Zoo**

Insert a marker-delimited `## Leaderboard and Recent Evaluations` section after the Release Zoo notes. Table 1 must contain the 27 rows in Section 4.3 of `docs/superpowers/specs/2026-07-10-atbench-leaderboard-design.md`, sorted by F1 with competition ranking. Bold exactly these metric maxima:

```text
Acc: 78.4, AgentDoG 1.5-4B-U
Precision: 85.7, LlamaGuard3-8B
Recall: 89.5, Llama3.1-8B-Instruct
F1: 79.5, Qwen3-8B-Instruct + FATE
R.S./F.M./R.H.: 75.2 / 27.5 / 62.9, AgentDoG 1.5-4B
```

The protocol note must say that only complete current 1,000-case ATBench evaluations are cross-ranked and that unsafe is the positive class.

- [ ] **Step 4: Add the ten-paper evaluation/use table**

Use this heading and relation vocabulary:

```markdown
### Recent Papers Evaluating or Using ATBench
```

Include the ten papers listed in Task 1 with their exact release, case count, split/transformation, reported result, and official resources from Section 5.2 of the design. Do not render any `Cites only` or `Cites extension` row. Add a one-line maintenance note saying the table was checked through 2026-07-10.

- [ ] **Step 5: Commit the README update**

Run:

```bash
git add README.md
git diff --cached --check
git commit -m "docs: add ATBench leaderboard and evaluation tracker"
```

Expected: the commit contains only `README.md`.

### Task 3: Verify and publish the Repo update

**Files:**
- Verify: `README.md`
- Verify: `docs/superpowers/specs/2026-07-10-atbench-leaderboard-design.md`
- Verify: `docs/superpowers/plans/2026-07-10-atbench-repo-leaderboard.md`

- [ ] **Step 1: Run structural table checks**

Run awk checks that assert:

```text
Leaderboard rows = 27
Leaderboard F1 order = non-increasing
F1 67.8 rows share rank 10 and are followed by rank 12
Evaluation/use rows = 10
Evaluation/use dates = non-increasing
```

Expected: all assertions pass with exit 0.

- [ ] **Step 2: Check links and Markdown whitespace**

Run:

```bash
git diff --check
rg -o 'https://[^)> ]+' README.md | sort -u | xargs -n1 -P8 sh -c 'u="$1"; code=$(curl -L -sS --max-time 20 -o /dev/null -w "%{http_code}" "$u"); printf "%s %s\n" "$code" "$u"; [ "$code" = 200 ]' sh
```

Expected: `git diff --check` is clean and every bounded URL check returns HTTP 200.

- [ ] **Step 3: Confirm only unrelated untracked files remain**

Run:

```bash
git status --short
```

Expected: only `.DS_Store` and `COLM Rebuttal/` are untracked; no tracked file is modified or staged.

- [ ] **Step 4: Push and verify the public README**

Run:

```bash
git push origin main
```

Then fetch the raw GitHub README and assert that it contains the COLM News item, the leaderboard heading, FATE, AgentDoG 1.5, and exactly ten evaluation/use rows.

Expected: push succeeds and the remote structural checks pass.
