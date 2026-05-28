---
title: Paper Priority Scoring System
date: 2026-05-28
status: approved
---

# Paper Priority Scoring System

## Purpose

Score each paper and field report in the awesome-autonomous-hacking-agents list so a blank-slate builder has a clear priority reading order. Stars appear inline in each README table row.

## Target reader

Someone who has not yet written a single line of their hackbot and wants to know what to read first.

## Scoring mechanism

Each paper is assessed against 5 binary (Y/N) questions. The star rating is computed from the answers.

### The 5 questions

| ID | Question |
|----|----------|
| Q1 | Does it give a concrete architecture you can implement? |
| Q2 | Was the system tested on real or realistic targets (not toy/CTF-only)? |
| Q3 | Is there open-source code or a runnable artifact? |
| Q4 | Does it cover a concept no other paper in the list addresses? |
| Q5 | Is it useful before you have a working agent (blank-slate applicable)? |

### Aggregation rules

1. **Q1 = N** → capped at ⭐⭐ regardless of other scores (theoretical-only papers can never be ⭐⭐⭐)
2. **Q1 = Y AND total Y count ≥ 3** → ⭐⭐⭐
3. **Q1 = Y AND total Y count = 1–2** → ⭐⭐
4. **Total Y count = 0** → ⭐

Tie-break: a paper with Q1=N and 4 other Y's scores ⭐⭐, not ⭐⭐⭐. The knockout is hard.

### Star meanings

| Stars | Label | When to read |
|-------|-------|--------------|
| ⭐⭐⭐ | Must-read | Before you write your first agent |
| ⭐⭐ | Enrich-later | After you have a working prototype |
| ⭐ | Reference | When you hit the specific problem it solves |

## Field report scoring

Field reports use the same 5 questions. Because all FRs describe real shipped systems:
- Q1 is almost always Y (they describe concrete architectures)
- Q2 is almost always Y (run against real targets by definition)
- Q3 varies (some are open source, some are not)

The same aggregation rules apply.

## README integration

Add a **Stars** column as the second column in each per-category table, immediately after the paper title link:

```
| Paper | ⭐ | Description | arXiv |
```

Stars are rendered as emoji: `⭐⭐⭐`, `⭐⭐`, `⭐`.

## Implementation steps

1. Score all 40 papers against Q1–Q5, compute star rating per aggregation rules
2. Score all 6 field reports
3. Add Stars column to each README table
4. Commit and push
