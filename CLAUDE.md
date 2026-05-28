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

## Inclusion Checklist

Before adding any paper, answer YES to all of the following:

1. **Relevance:** Does this paper directly help someone building an autonomous agent that performs security/hacking tasks?
2. **Agentic:** Is there an autonomous loop — an agent that takes actions, observes results, and iterates — rather than a single-shot LLM call?
3. **Non-trivial:** Does this paper contribute something architecturally or empirically new, not just restate known results?
4. **Tier fit:** Does it clearly fit into one of the four tiers (or the bonus category) based on the definitions above?

If you answer NO to any of these, do not add the paper.

---

## How to Format Each Entry

Each row in the README table uses this format:

```
| **[Paper Title](arxiv_pdf_url)** | Tier | One-sentence capability claim. One-sentence architecture note. One-sentence "why it matters for your bot." | [arXiv:XXXX.XXXXX](arxiv_abs_url) |
```

**Title:** Use the exact paper title. Link to the PDF.

**Tier:** Write the tier number as `T1`, `T2`, `T3`, `T4`, or `Bonus`.

**Description (3 sentences max):**
- Sentence 1: What the system *does* (its capability, stated as an action)
- Sentence 2: How it works (the key architectural idea, in plain terms)
- Sentence 3: Why a hacking bot builder should care (what problem it solves for them)

**arXiv link:** Link to the abstract page (not the PDF), using the format `arXiv:XXXX.XXXXX`.

---

## What to Do When a Paper Is Borderline

If a paper is relevant to building agents in general but not specifically to offensive security, ask: "Would a security engineer building a hacking bot learn something they couldn't get from a general agentic AI survey?" If yes, include it in the appropriate tier. If no, skip it.

When in doubt between Tier 2 and Tier 3, ask whether the paper is primarily about *coordination* (Tier 2) or *knowledge persistence across time* (Tier 3).

When in doubt between Tier 3 and Tier 4, ask whether the paper is primarily about *what the agent remembers* (Tier 3) or *what the agent can do* (Tier 4).
