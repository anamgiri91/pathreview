# JOURNAL

## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/36

**Issue title:** Architecture doc doesn't explain the hybrid retrieval scoring formula

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
The `docs/ARCHITECTURE.md` file mentions that the retrieval system blends vector search and keyword search scores, but it never explains how that blend is actually calculated or what the default weighting is. Right now a reader has no way to know how much each score contributes to the final ranking, or to reproduce it by hand. A successful fix adds a clear section explaining the scoring formula, the default weights, and a worked example so future contributors can understand and tune the retrieval logic. This affects the retrieval/RAG portion of the codebase.

**Branch name:** docs/36-hybrid-retrieval-scoring-formula

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [ ] Issue added to cohort ledger

## Issue Selection Checklist Reasoning

**Part 1 — Understanding:** The issue is that ARCHITECTURE.md mentions hybrid
retrieval blends vector and keyword scores, but never explains the formula or
default weights. I confirmed this by reading the current doc section and found
it's a one-line description with no math. I then found the actual
implementation in rag/retriever/hybrid.py: it's a weighted sum of normalized
vector and BM25 scores (default weights 0.7 vector / 0.3 keyword), where each
score is divided by the max score in its own result set before blending.
Done = a new doc section explaining this formula, the default weights, and a
worked numeric example.

**Part 2 — Tier fit:** This is my first pathreview contribution, so Tier 1 is
the right starting point regardless of my prior RAG experience — the goal
here is learning the contribution workflow, not testing my RAG knowledge.

**Part 3 — Codebase readiness:** Found and read rag/retriever/hybrid.py in
full, including the retrieve() method and score normalization logic. This is
a docs-only issue so there's no test file to modify, but I confirmed the
scoring behavior directly from the source rather than guessing from the
issue description.

**Part 4 — Scope and time:** Several other students have also claimed issue
#36 in the comments (at least 10+ across multiple AI-201 sections). Claims
are non-exclusive per the checklist, and my grade is based on my own
artifacts, so I'm comfortable proceeding despite the overlap. Estimated time:
2-3 hours as labeled, and I've already done the code investigation, so this
is realistic for Weeks 8-9. No blockers or dependencies mentioned on the issue.