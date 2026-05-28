# CLAUDE.md — Curation Guide for awesome-autonomous-hacking-agents

This file tells you exactly how to decide what belongs in this list, which tier it goes into, and what to write for each entry.

---

## What This List Is

A curated reading list of AI-agent papers that are directly useful for **building, evaluating, or understanding autonomous hacking bots** — agents that can discover, analyze, and exploit vulnerabilities with minimal human input.

This is NOT a general AI security list. Papers about LLM safety, content moderation, and watermarking belong elsewhere unless they directly teach something about offensive agent architecture.

---

## The Tier System

There are four tiers plus one bonus category. Each tier answers a different question a builder would ask.

---

### Tier 1 — Core Offensive AI

**The question this tier answers:** "Can this paper teach me how an agent actually hacks something?"

**What belongs here:**
- Papers where the LLM agent performs an offensive action: exploit generation, CVE reproduction, CTF solving, malware analysis, binary analysis, vulnerability discovery
- Papers that benchmark agents on real or realistic attack tasks (CTF, CVE datasets, sandboxed crime simulation)
- Papers with a working end-to-end system that goes from a description/input to a working exploit or finding

**What does NOT belong here:**
- Papers that only *defend* against attacks (unless the defense paper reveals a new attack model worth understanding)
- Papers about detecting attacks without generating them
- General vulnerability scanning tools without an autonomous agent loop

**How to write the entry:** Lead with the attack capability demonstrated, then describe the architecture. Mention what input the system takes and what output it produces (e.g., "takes a CVE description, produces a runnable PoC").

**Bar:** If you read this paper and you have no new idea for how to make your bot attack something more effectively, it does not belong in Tier 1.

---

### Tier 2 — Agent Architecture

**The question this tier answers:** "How do I structure multiple agents so they can handle complex, multi-step hacking tasks autonomously?"

**What belongs here:**
- Multi-agent coordination papers where agents have specialized roles (planner, executor, reviewer, researcher)
- Long-horizon planning papers: task decomposition, recursive delegation, parallel subtask execution
- Self-improving or self-evolving agent frameworks
- Adversarial training architectures (attacker-vs-defender RL games that make an agent more robust)
- Papers that solve the "my agent gets stuck on complex tasks" problem

**What does NOT belong here:**
- Single-model reasoning improvements (chain-of-thought, etc.) with no agentic loop
- Multi-agent papers that are purely about consensus or voting (not relevant to offense)
- Papers whose domain is unrelated to code/systems (e.g., multi-agent negotiation for e-commerce)

**How to write the entry:** Describe the coordination pattern (who does what), mention what problem it solves (context overflow, task complexity, agent specialization), and explain how it maps to a hacking workflow (recon → exploit → post-exploitation).

**Bar:** If a builder could take the architecture from this paper and use it as the skeleton of their hacking bot, it belongs here.

---

### Tier 3 — Memory & Knowledge Retention

**The question this tier answers:** "How does my bot remember what it learned from past engagements and reuse it?"

**What belongs here:**
- Procedural memory: saving and reusing step-by-step procedures (attack playbooks)
- Long-horizon memory: state that persists across multiple sessions or targets
- Experience extraction: turning agent trajectories into reusable knowledge
- Memory architectures specifically designed for agents that operate over long durations

**What does NOT belong here:**
- RAG papers focused on Q&A retrieval (not agent memory)
- Memory papers where the use case is conversational assistants or personalization
- Papers about compressing context windows without a persistent external store

**How to write the entry:** Explain what kind of memory it is (procedural, episodic, semantic), how it is built (from execution traces? from human feedback?), and give a concrete example of how a hacking bot would use it (e.g., "stores a successful SQL injection sequence and reuses it against new targets").

**Bar:** If this paper would help a hacking bot avoid re-solving a problem it has already solved before, it belongs here.

---

### Tier 4 — Tool Use & Execution

**The question this tier answers:** "How does my bot actually take actions in the world — run commands, write scripts, use a browser, interface with terminals?"

**What belongs here:**
- Computer-use agents: agents that operate a desktop, terminal, or browser
- Dynamic tool creation: agents that write their own tools at inference time
- Skill libraries for agents with parameterized, composable actions
- Infinite-horizon execution frameworks that keep context bounded during long operations
- Papers about reliable code execution in autonomous agents

**What does NOT belong here:**
- Tool-calling papers focused purely on API selection benchmarks without execution
- GUI agents for productivity apps (unless they generalize to a terminal/shell)
- Papers about structured output formatting for tool calls

**How to write the entry:** Describe what the agent can do (run shell commands? write and execute Python? browse the web?), mention how it handles failures, and explain why this matters for a hacking workflow (e.g., "lets your bot write a new scanner script when its existing tools fail on a novel target").

**Bar:** If this paper would help your bot take a new category of action it could not take before, it belongs here.

---

### Bonus — Know What You're Up Against

**The question this category answers:** "What defenses and countermeasures will my bot encounter, and what can it realistically accomplish against frontier models?"

**What belongs here:**
- Papers that test which frontier models will actually execute offensive tasks (safety collapse studies)
- Papers about attack techniques that target LLM-integrated systems (prompt injection, cache attacks, RAG poisoning) — relevant if your bot targets AI-augmented applications
- Large-scale empirical studies of what AI agents can and cannot do in offensive scenarios

**What does NOT belong here:**
- Defense-only papers with no offensive insight
- Papers about abstract safety alignment with no empirical attack data

**How to write the entry:** State what the paper reveals about the attack surface or model capability, and explain the practical implication for building or deploying your bot (e.g., "tells you which model to use so your bot doesn't need jailbreaks").

---

---

### Field Reports (FR)

**The question this category answers:** "How did someone who actually shipped a working hacking bot build it — what broke, what worked, what would they do differently?"

**What belongs here:**
- Blog posts, write-ups, or post-mortems from teams that built and deployed a real autonomous hacking or security automation system
- Competition write-ups where the team shipped a working Cyber Reasoning System (e.g., DARPA AIxCC, DEF CON CTF) with substantive architectural detail
- Posts that describe actual agent design decisions with enough specificity to be actionable: specific tool schemas, agent role definitions, prompting strategies, failure modes encountered
- Posts where the author derived architectural insights from building the system — not from reading papers or theorizing

**What does NOT belong here:**
- Tutorial posts ("how to use LangChain for security") with no original system behind them
- Marketing posts for commercial security products that don't expose implementation details
- Opinion pieces or predictions about what AI could do for security
- Posts that describe a demo or toy system, not a system run against real targets or real competition benchmarks

**How to write the entry:** Three things must appear in the description — (1) what the system was actually run against (CTF challenges, real CVEs, a competition CRS, a production codebase), (2) the specific architectural insight or design pattern that makes it worth reading, and (3) a concrete artifact the reader can inspect or copy (code, schema, tool definition, prompt structure).

**Bar:** If you could replace this post with "use LangChain and prompt-engineer your way through it" and lose nothing, it does not belong here. Field reports earn inclusion by reporting on decisions that can only be known by shipping the system.

**Formatting note:** Field reports live in their own table under `## Field Reports`, separate from the papers tables. Use the same ⭐ scoring column as papers. The source column links to the original post, not an arXiv ID. All field reports that pass the inclusion checklist tend to score ⭐⭐⭐ (Q1, Q2, Q4, Q5 = Y by definition of the FR bar; Q3 = Y if open source).

---

## Inclusion Checklist

**For academic papers (T1–T4, Bonus):** Answer YES to all of the following.

1. **Relevance:** Does this paper directly help someone building an autonomous agent that performs security/hacking tasks?
2. **Agentic:** Is there an autonomous loop — an agent that takes actions, observes results, and iterates — rather than a single-shot LLM call?
3. **Non-trivial:** Does this paper contribute something architecturally or empirically new, not just restate known results?
4. **Tier fit:** Does it clearly fit into one of the four tiers (or the Bonus category) based on the definitions above?

**For field reports (FR):** Answer YES to all of the following.

1. **Shipped:** Was this system run against real targets, real competition benchmarks, or a real production codebase — not a demo or a thought experiment?
2. **Specific:** Does the post expose concrete implementation detail (tool schemas, agent role definitions, failure modes, prompt structures) that a builder can act on?
3. **Original:** Did the author derive the insight from building the system, not from reading papers or theorizing?
4. **Non-marketing:** Is the post written to share knowledge, not to sell a product?

If you answer NO to any item in the relevant checklist, do not add the entry.

---

## How to Score Each Entry

Every entry gets a ⭐ rating computed from 5 binary (Y/N) questions. Answer each question for the paper, sum the Y's, then apply the rules below.

### The 5 questions

| ID | Question |
|----|----------|
| Q1 | Does it give a concrete architecture you can implement? |
| Q2 | Was the system tested on real or realistic targets (not toy/CTF-only)? |
| Q3 | Is there open-source code or a runnable artifact? |
| Q4 | Does it cover a concept no other paper in the list addresses? |
| Q5 | Is it useful before you have a working agent (blank-slate applicable)? |

**Q1 guidance:** A paper that only surveys, theorizes, or benchmarks without describing a buildable system scores N. A paper that gives you role definitions, loop structures, memory schemas, or tool patterns scores Y.

**Q2 guidance:** HackTheBox, GOAD Active Directory, Metasploitable, real CVEs on live systems, and DARPA AIxCC repositories = Y. Synthetic CTF-only benchmarks (PicoCTF, OverTheWire) or toy environments = N.

**Q5 guidance:** If the paper's value assumes you already have a running agent (e.g., it improves memory reuse, fine-tunes a model, or diagnoses agent failures), score N. If you could use its architecture to design your first agent from scratch, score Y.

### Aggregation rules

1. **Q1 = N** → capped at ⭐⭐ regardless of other scores (no theoretical-only paper can be ⭐⭐⭐)
2. **Q1 = Y AND total Y count ≥ 3** → ⭐⭐⭐
3. **Q1 = Y AND total Y count = 1–2** → ⭐⭐
4. **Total Y count = 0** → ⭐

### Star meanings

| Stars | Read when |
|-------|-----------|
| ⭐⭐⭐ | Before you write your first agent |
| ⭐⭐ | After you have a working prototype |
| ⭐ | When you hit the specific problem it solves |

---

## How to Format Each Entry

Papers go in the per-category table under the matching numbered section. Each row uses this format:

```
| **[Paper Title](arxiv_pdf_url)** | ⭐⭐⭐ | One-sentence capability claim. One-sentence architecture note. One-sentence "why it matters for your bot." | [XXXX.XXXXX](arxiv_abs_url) |
```

**Title:** Use the exact paper title. Link to the PDF.

**Stars:** Apply the scoring rubric above before adding the entry.

**Description (3 sentences max):**
- Sentence 1: What the system *does* (its capability, stated as an action)
- Sentence 2: How it works (the key architectural idea, in plain terms)
- Sentence 3: Why a hacking bot builder should care (what problem it solves for them)

**arXiv link:** Link to the abstract page (not the PDF).

---

## What to Do When a Paper Is Borderline

If a paper is relevant to building agents in general but not specifically to offensive security, ask: "Would a security engineer building a hacking bot learn something they couldn't get from a general agentic AI survey?" If yes, include it in the appropriate tier. If no, skip it.

When in doubt between Tier 2 and Tier 3, ask whether the paper is primarily about *coordination* (Tier 2) or *knowledge persistence across time* (Tier 3).

When in doubt between Tier 3 and Tier 4, ask whether the paper is primarily about *what the agent remembers* (Tier 3) or *what the agent can do* (Tier 4).
