# Awesome Autonomous Hacking Agents

> A curated reading list of AI-agent papers for building autonomous security bots — agents that discover, analyze, and exploit vulnerabilities with minimal human input.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
![Papers](https://img.shields.io/badge/papers-23-b31b1b)
![Field Reports](https://img.shields.io/badge/field%20reports-2-orange)
![Year](https://img.shields.io/badge/year-2025--2026-blue)

---

## Tier System

| Tier | Name | The Question It Answers |
|:---:|---|---|
| **T1** | Core Offensive AI | Can this paper teach me how an agent actually hacks something? |
| **T2** | Agent Architecture | How do I structure agents to handle complex multi-step hacking tasks? |
| **T3** | Memory & Knowledge Retention | How does my bot remember what it learned and reuse it? |
| **T4** | Tool Use & Execution | How does my bot run commands, write scripts, and take real-world actions? |
| **Bonus** | Know What You're Up Against | What can frontier models realistically do, and what defenses will I face? |
| **FR** | Field Report | How did people who actually shipped a hacking bot build it? |

See [CLAUDE.md](./CLAUDE.md) for detailed criteria on what belongs in each tier.

---

## Reading Order

```
Week 1  →  T1 papers 1–4   (why/what/how + core exploit loop)
Week 2  →  T1 papers 5–9   (concrete implementations to study and copy)
Week 3  →  T2 papers        (multi-agent architecture)
Week 4  →  T3 papers        (memory layer)
Week 5  →  T4 + Bonus       (tool use + model selection)
```

---

## Papers

| Paper | Tier | Description | arXiv |
|---|:---:|---|:---:|
| **[To Defend Against Cyber Attacks, We Must Teach AI Agents to Hack](https://arxiv.org/pdf/2602.02595v1)** | T1 | Argues that AI-agent-driven cyberattacks are inevitable and that building frontier offensive AI responsibly is essential defensive infrastructure. Surveys the landscape of what agents can already do offensively, with a blueprint for responsible capability development. Read this first — it frames the entire space. | [2602.02595](https://arxiv.org/abs/2602.02595) |
| **[A Dual-Loop Agent Framework for Automated Vulnerability Reproduction](https://arxiv.org/pdf/2602.05721v1)** | T1 | Takes a CVE description as input and produces a working exploit using two feedback loops — an outer strategy loop and an inner code loop. The dual-loop pattern separates high-level attack planning from low-level code generation, preventing strategy drift when code fails. Directly copy this architecture for your bot's exploit-generation pipeline. | [2602.05721](https://arxiv.org/abs/2602.05721) |
| **[Capture the Flags: Family-Based Evaluation of Agentic LLMs](https://arxiv.org/pdf/2602.05523v1)** | T1 | Generates families of equivalent CTF challenges via code transformations to test whether an agent truly understands exploits or just memorizes patterns. Exposes the difference between genuine exploit understanding and surface-level pattern matching. Use this benchmark architecture to evaluate your own bot. | [2602.05523](https://arxiv.org/abs/2602.05523) |
| **[TxRay: Agentic Postmortem of Live Blockchain Attacks](https://arxiv.org/pdf/2602.01317v4)** | T1 | Reconstructs exploit lifecycles from limited on-chain evidence and generates runnable PoC reproductions. The agent chains together sparse signals into a coherent attack narrative, then translates that narrative into executable code. A concrete end-to-end pipeline from intelligence to working exploit. | [2602.01317](https://arxiv.org/abs/2602.01317) |
| **[Identifying Adversary Tactics and Techniques in Malware Binaries with an LLM Agent](https://arxiv.org/pdf/2602.06325v1)** | T1 | Uses an LLM agent to map MITRE ATT&CK techniques in stripped malware binaries through incremental context retrieval. Solves the problem of limited context windows on large binaries by feeding evidence incrementally. Use this when your bot needs to reason about existing malware or analyze unfamiliar binaries. | [2602.06325](https://arxiv.org/abs/2602.06325) |
| **[VirtualCrime: Evaluating Criminal Potential of LLMs via Sandbox Simulation](https://arxiv.org/pdf/2601.13981v1)** | T1 | Evaluates what LLMs can execute in sandboxed offensive scenarios without specialized prompting. Gives empirical ground truth on which models succeed at real-world attack tasks and which prompting strategies are effective. Read before choosing a backbone model for your bot. | [2601.13981](https://arxiv.org/abs/2601.13981) |
| **[AgenticSCR: An Autonomous Agentic Secure Code Review for Immature Vulnerabilities Detection](https://arxiv.org/pdf/2601.19138v1)** | T1 | Autonomous vulnerability detection via tool invocation and security-focused semantic memory for pre-commit code review. The memory architecture stores "what to look for" as indexed security patterns rather than raw rules. Reuse the memory design for your bot's vulnerability-discovery phase. | [2601.19138](https://arxiv.org/abs/2601.19138) |
| **[Multimodal Multi-Agent Ransomware Analysis Using AutoGen](https://arxiv.org/pdf/2601.20346v1)** | T1 | A working AutoGen-based multi-agent system for malware analysis that divides static analysis, dynamic analysis, and reporting across specialized agents. Shows how to wire AutoGen agents together for a security-specific task with concrete role definitions. A practical reference implementation to fork. | [2601.20346](https://arxiv.org/abs/2601.20346) |
| **[Sifting the Noise: A Comparative Study of LLM Agents in Vulnerability False Positive Filtering](https://arxiv.org/pdf/2601.22952v1)** | T1 | Head-to-head benchmark of Aider, OpenHands, and SWE-agent on vulnerability triage tasks across multiple backbone models. Measures how agent design — not just model capability — affects security task performance. Read this before picking which agent framework to build on. | [2601.22952](https://arxiv.org/abs/2601.22952) |
| **[CORAL: Towards Autonomous Multi-Agent Evolution for Open-Ended Discovery](https://arxiv.org/pdf/2604.01658)** | T2 | Self-evolving multi-agent system using shared persistent memory, asynchronous execution, and heartbeat-based interventions, achieving 3–10× improvement rates over fixed baselines. Agents evolve their own strategies without human intervention across math, algorithmic, and systems tasks. The architecture for a hacking bot that gets better at its job autonomously over time. | [2604.01658](https://arxiv.org/abs/2604.01658) |
| **[ROMA: Recursive Open Meta-Agent Framework for Long-Horizon Multi-Agent Systems](https://arxiv.org/pdf/2602.01848v1)** | T2 | Decomposes large tasks into parallel subtask trees across multiple agents without hitting context limits. Handles long-horizon workflows by distributing work recursively rather than sequentially. Use this as the planning backbone for multi-stage hacking operations (recon → enumeration → exploitation → post-exploitation). | [2602.01848](https://arxiv.org/abs/2602.01848) |
| **[Agyn: A Multi-Agent System for Team-Based Autonomous Software Engineering](https://arxiv.org/pdf/2602.01465v2)** | T2 | Assigns specialized agents to coordination, research, implementation, and review roles for autonomous software engineering. Role separation prevents agents from conflating strategy with execution. Maps directly to a hacking team: planner, OSINT/recon, exploit-writer, validator. | [2602.01465](https://arxiv.org/abs/2602.01465) |
| **[MAGIC: A Co-Evolving Attacker-Defender Adversarial Game for Robust LLM Safety](https://arxiv.org/pdf/2602.01539v2)** | T2 | RL game where an attacker agent and a defender agent co-evolve, stress-testing safety alignment against novel, never-seen attack patterns. The attacker continuously generates new attack strategies in response to what the defender blocks. Use this to train your bot to bypass defenses that don't exist yet. | [2602.01539](https://arxiv.org/abs/2602.01539) |
| **[StackPlanner: A Centralized Hierarchical Multi-Agent System with Task-Experience Memory Management](https://arxiv.org/pdf/2601.05890v1)** | T2 | Hierarchical planner that decouples coordination from execution and uses RL-driven experience reuse across sessions. Stores successful task decompositions and replays them when structurally similar tasks recur. For a hacking bot running multiple targets, this prevents re-solving already-solved planning problems. | [2601.05890](https://arxiv.org/abs/2601.05890) |
| **[ProcMEM: Learning Reusable Procedural Memory from Experience via Non-Parametric PPO for LLM Agents](https://arxiv.org/pdf/2602.01869v1)** | T3 | Saves step-by-step attack procedures from past agent runs and retrieves them for reuse without retraining, trained via non-parametric PPO. Procedural memory stores *how* to accomplish a goal, not just *that* a goal was accomplished. Your bot's exploit playbook that grows automatically with each successful engagement. | [2602.01869](https://arxiv.org/abs/2602.01869) |
| **[AutoRefine: From Trajectories to Reusable Expertise for Continual LLM Agent Refinement](https://arxiv.org/pdf/2601.22758v1)** | T3 | Extracts two forms of reusable knowledge from execution histories: specialized subagents for recurring procedural tasks and skill patterns for static knowledge lookup, with continuous pruning and merging. Turns every hacking session into training data for the next one. Use this as the long-term learning layer sitting above your short-term memory. | [2601.22758](https://arxiv.org/abs/2601.22758) |
| **[Continuum Memory Architectures for Long-Horizon LLM Agents](https://arxiv.org/pdf/2601.09913v1)** | T3 | Defines the class of memory systems for agents that need persistent, temporally chained state across multiple sessions — as opposed to stateless RAG lookups. Specifies the formal requirements a memory system must satisfy for long-horizon operation. Mandatory reading before designing the persistence layer for a multi-session hacking bot. | [2601.09913](https://arxiv.org/abs/2601.09913) |
| **[CUA-Skill: Develop Skills for Computer Using Agent](https://arxiv.org/pdf/2601.21123v2)** | T4 | Large-scale computer-use skill library with parameterized execution, composition graphs, dynamic retrieval, and memory-aware failure recovery for desktop and terminal applications. Skills are composable and parameterized — one "run nmap" skill works for any target, not just a hardcoded one. The reference implementation for giving your bot reliable terminal and GUI access. | [2601.21123](https://arxiv.org/abs/2601.21123) |
| **[Beyond Static Tools: Test-Time Tool Evolution for Scientific Reasoning](https://arxiv.org/pdf/2601.07641v1)** | T4 | Agents synthesize, verify, and evolve their own executable tools at inference time instead of relying on static pre-defined tool libraries. New tools are validated before use and pruned when they fail. For a hacking bot, this means dynamically writing a new scanner or exploit script when existing tools fail on a novel target. | [2601.07641](https://arxiv.org/abs/2601.07641) |
| **[InfiAgent: An Infinite-Horizon Framework for General-Purpose Autonomous Agents](https://arxiv.org/pdf/2601.03204v1)** | T4 | Keeps reasoning context bounded regardless of operation length by externalizing persistent state into a file-centric abstraction. The agent reads and writes state files instead of accumulating context, so it never runs out of context during a long engagement. Mandatory for any multi-day autonomous hacking operation. | [2601.03204](https://arxiv.org/abs/2601.03204) |
| **[Internal Safety Collapse in Frontier Large Language Models](https://arxiv.org/pdf/2603.23509)** | Bonus | Reveals that AI agents produce exploits and dangerous data as a side effect of normal professional tasks — no adversarial prompting needed. Tests 8+ frontier models across 56 cross-domain scenarios. Tells you which backbone model your bot can use without needing to spend effort on jailbreaks. | [2603.23509](https://arxiv.org/abs/2603.23509) |
| **[Learning to Inject: Automated Prompt Injection via Reinforcement Learning](https://arxiv.org/pdf/2602.05746v1)** | Bonus | Uses RL to auto-generate prompt injection attacks that transfer across multiple frontier LLM models. Attacks are discovered without white-box access and generalize to unseen models. Essential if your bot targets LLM-integrated applications — this is the attack technique it needs. | [2602.05746](https://arxiv.org/abs/2602.05746) |
| **[Agent Skills in the Wild: An Empirical Study of Security Vulnerabilities at Scale](https://arxiv.org/pdf/2601.10338v1)** | Bonus | Analyzes 42,447 agent skills from two major marketplaces, mapping the attack surface across prompt injection, data exfiltration, privilege escalation, and supply chain risks. Shows how real-world agent deployments fail, with prevalence data across vulnerability classes. Tells you where to aim your bot for maximum impact in the wild. | [2601.10338](https://arxiv.org/abs/2601.10338) |

---

## Field Reports

Practitioner write-ups from people who built and shipped real hacking bots. Unlike academic papers, these report on what actually broke in production, what tooling decisions worked, and what the agent loop looks like when it runs against real targets.

| Post | Tier | Description | Source |
|---|:---:|---|:---:|
| **[How the Hacking Agents Work](https://s1r1us.ninja/posts/how-hacker-sub-agent-works/)** — s1r1us (Hacktron.ai) | FR | Frames vulnerability discovery as **adversarial theorem proving** using the Curry-Howard correspondence: an exploit is a proof that an unintended program state is reachable. Proposes two discovery modes — *variant analysis* (proving known bug classes exist in new code, ~60–70% of web vulns) and *novel research* (generating new propositions from deep system understanding). The key architectural insight: top-tier hackers never load full codebases into working memory; they build compressed **abstract representations** (control-flow skeletons) and reason over those. Maps directly to agent design: an Understanding Agent builds the abstraction, a Reasoning Agent simulates what breaks it. | [s1r1us.ninja](https://s1r1us.ninja/posts/how-hacker-sub-agent-works/) |
| **[Building Effective LLM Agents \| AI Cyber Challenge](https://theori.io/blog/building-effective-llm-agents-63446)** — Xint, Theori (3rd place, DARPA AIxCC) | FR | Four battle-tested patterns from building RoboDuck, the CRS that placed 3rd at DARPA's AI Cyber Challenge: (1) **decompose tasks into sub-agents** so each agent gets only its own context — the sub-agent call doubles as context compression; (2) **curate custom tools** instead of raw bash — e.g., `read_definition`, `find_references` backed by clang AST/joern, with hard limits to prevent context floods; (3) **structure outputs with XML tags or a `terminate` tool** and include decoy fields that force the model to reason about trigger conditions (reduces false positives); (4) **adapt prompting to each model** — `<rule>` blocks for Claude, forced `tool_choice=required` for o4-mini. Open-source CRS at [theori-io/aixcc-afc-archive](https://github.com/theori-io/aixcc-afc-archive). | [theori.io](https://theori.io/blog/building-effective-llm-agents-63446) |

---

## Contributing

Before adding a paper, read [CLAUDE.md](./CLAUDE.md) — it defines each tier precisely and gives an inclusion checklist. Every entry must answer YES to all four checklist items.

---

## License

[CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) — public domain.
