---
title: "Coding Accuracy vs. Inference Speed: The Three Pareto Frontiers"
date: 2026-02-23
author: "Gabor Melli"
topics:
  - ai-coding
  - model-evaluation
  - ai-productivity
evidence_tier: 1
source_count: 16
key_sources:
  - "METR RCT (2025)"
  - "Dekoninck et al. ICLR 2025"
  - "DORA 2025"
  - "Stanford HAI AI Index 2025"
abstract: >
  No single AI coding model wins across all benchmarks. The real optimization
  problem is not model selection but workflow design — where the evidence shows
  AI speed gains are offset by quality degradation. This brief maps three nested
  pareto frontiers and identifies the largest research gap in the field.
---

# Coding Accuracy vs. Inference Speed: The Three Pareto Frontiers

**Date**: 2026-02-23
**Sources**: Artificial Analysis (Feb 2026), METR RCT (Jul 2025) + Transcript Analysis (Feb 2026), CodeRabbit State of Code Quality (Dec 2025), Sonar 2026 Developer Survey (Jan 2026), Harness AI Velocity Paradox (Sep 2025), DORA 2025, Uplevel Copilot Study (2024), GitClear 2025, Greptile State of AI Coding 2025, Aider Polyglot Leaderboard, SWE-bench Verified (Feb 2026), LiveCodeBench (Feb 2026), Terminal-Bench 2.0 (Feb 2026), Dekoninck et al. ICLR 2025 (Cascade Routing), Stanford HAI AI Index 2025, BAMBO arXiv:2512.09972
**Evidence Tier**: 1 (METR pre-registered RCT, ICLR 2025 peer-reviewed, NIST/Stanford/DORA institutional reports, BLS data) + Tier 2 (industry surveys n>800) + Tier 3 (benchmark leaderboards, practitioner reports)

---

This brief examines three nested optimization problems in AI-assisted coding: model selection (well-mapped by benchmarks), workflow design (poorly mapped, the largest research gap), and organizational productivity (emerging). The evidence reveals that industry investment overwhelmingly targets model selection while workflow design offers larger returns.

---

## 1. The Model-Level Pareto Frontier (Well-Mapped)

### Coding Benchmark Leaderboard (February 2026)

| Model | SWE-bench V | LiveCodeBench | Terminal-Bench 2.0 | Aider Polyglot | Output t/s | $/M Input |
|-------|------------|---------------|--------------------|--------------|-----------:|----------:|
| Claude Opus 4.5 | **80.9%** | ~87% | 58.4% | **89.4%** | 67 | $5.00 |
| Claude Opus 4.6 | 80.8% | — | 65.4% | — | 75 | $5.00 |
| GPT-5.2 | 80.0% | **89%** | — | 88.0% (thinking) | ~187 | ~$5.00 |
| GPT-5.3 Codex | — | — | **77.3%** | — | ~62 | — |
| Gemini 3.1 Pro | — | **91.7%** | **67.4%** | — | 110 | **$2.00** |
| Gemini 3 Pro | 76.2% | — | 55.1% | 82.2% | **257** | $2.00 |
| Claude Sonnet 4.5 | 77.2% | — | — | 82.4% | 67 | $3.00 |
| Claude Sonnet 4.6 | — | — | 59.6% | — | 62 | ~$1.20 |
| DeepSeek V3.2 | 73.1% | 89.6% | — | — | ~40 | **$0.03** |
| GLM-4.7/5 | 77.8% | — | — | — | 63 | $0.05 |

**Key finding**: No single model wins across all benchmarks. Claude Opus leads SWE-bench (80.9%) but underperforms on Terminal-Bench (58.4%). Gemini leads LiveCodeBench (91.7%) and Terminal-Bench (67.4%) but trails on SWE-bench (76.2%). The frontier is multi-dimensional (accuracy x speed x cost x task-type).

### Price-Performance Champions

- **Budget frontier**: DeepSeek V3.2 at $0.03/M input — 73% SWE-bench at ~1/170th the cost of Opus
- **Mid-tier frontier**: Gemini 3.1 Pro at $2.00/M — leads most benchmarks, 7.5x cheaper than Opus
- **Accuracy ceiling**: Claude Opus 4.5/4.6 — 80.9% SWE-bench, premium pricing

### Live Frontier Tracking

Multiple projects explicitly map the LLM pareto frontier: Winston Bosan's live visualization (winston-bosan.github.io/llm-pareto-frontier/), Artificial Analysis Intelligence Index v4.0 (25% coding weight), and BAMBO (arXiv:2512.09972) which uses Bayesian optimization to construct provably optimal pareto sets.

---

## 2. The Workflow-Level Pareto Frontier (Poorly Mapped — Largest Research Gap)

### The AI Speed Trap Pattern (Documented by 6+ Independent Studies)

| Study | Speed Metric | Quality Metric | Net Assessment |
|-------|-------------|---------------|----------------|
| METR RCT (2025, n=16, pre-registered) | Perceived +20% | Actual -19% wall-clock | **Negative** |
| Uplevel (2024, n=800, before/after) | No cycle time change | +41% bug rate | **Negative** |
| CodeRabbit (2025, n=470 PRs) | +20% PRs/author/yr | 1.7x issues per PR | **Ambiguous** |
| Harness (2025, n=900 survey) | 63% ship faster | 72% had AI production incidents | **Negative net** |
| DORA 2025 | 90% using AI tools | -7.2% delivery stability per 25% adoption | **Destabilizing** |
| GitClear (2025, 211M LoC) | More code produced | Code churn nearly doubled since 2020 | **Negative** |

The pattern: (1) Optimize for speed → (2) Perceive +20% gain → (3) Actual throughput neutral-to-negative → (4) Quality degrades 41-70% → (5) Downstream costs escalate → (6) Net Pareto-inferior to careful human coding.

### The Verification Tax

| Metric | Value | Source |
|--------|-------|--------|
| Review time increase for AI code | +91% | DORA 2025 |
| PR size increase | +154% average | DORA 2025 |
| Devs who say AI review > human review effort | 38% | Sonar 2026 (n=1,100) |
| Devs who DON'T trust AI code | 96% | Sonar 2026 |
| Devs who ALWAYS verify anyway | Only 48% | Sonar 2026 |
| AI code: 42% of all committed code | — | Sonar 2026 |
| Production incidents from AI code | 72% of orgs | Harness 2025 |
| Hidden defects surface after | 30-90 days | CodeRabbit / Codebridge |

AWS CTO Werner Vogels: "When you write code yourself, comprehension comes with creation. When the machine writes it, you must rebuild that comprehension during review." This makes the verification cost partly **structural**, not solely model-quality-dependent.

### The Unmapped Quadrant

| | Low Quality | High Quality |
|---|---|---|
| **High Speed** | Well-studied (METR, Uplevel, Harness) — net negative | **NOT YET STUDIED** |
| **Low Speed** | Not relevant | Baseline human performance |

The entire evidence base describes speed-optimized or unstructured AI use. No study has measured the quality-optimized configuration (slower models, mandatory verification, multi-agent review). The quality-first AI-assisted quadrant is the single largest research gap in the field.

### METR Follow-Up (February 17, 2026)

METR transcript analysis of 5,305 Claude Code transcripts found 1.5-13x time savings on self-selected tasks — but with critical caveats: selection bias (developers choose tasks where AI helps), the time savings factor "does not equal the productivity multiplier," and the original RCT's serial task design may understate AI's concurrency benefits. No replication of the original RCT has been published.

### Zvi Mowshowitz Critique

Key limitations of the METR RCT: deeply-understood open-source repos are worst-case for AI tools; 1-2 hour pre-decomposed tasks limit flexibility; hourly pay reduces efficiency incentives; developers lacked tool experience. Conclusion: the -19% may be specific to study conditions rather than a general indictment.

---

## 3. Strategies to Move the Frontier (Not Just Trade Along It)

### Cascade Routing (ICLR 2025 — Dekoninck et al.)

Unifies routing (single model per query) and cascading (sequential escalation) into a theoretically optimal strategy:
- 50x cost savings possible (Haiku vs. Opus)
- 16x efficiency for code generation vs. naive cascading
- 5x+ cost savings with reliable judges at negligible quality loss
- Not Diamond router: +25% accuracy, -10x cost via pareto-optimized routing

**Practical three-tier pattern**: Haiku/Flash for 80% of tasks, Sonnet for 15%, Opus for 5%.

### Verification-First Workflows

Only demonstrated technique for converting AI speed into net quality improvement:
- Spotify Honk: LLM Judge vetoes ~25% of sessions
- Multi-agent review: "one writes, another critiques, another tests, another validates"
- SonarQube users: 24% lower vulnerability rates, 20% lower defect rates

### Adaptive Reasoning

Right amount of thinking per task:
- Claude Sonnet 4.6 adaptive: ~2s simple, extended thinking for complex
- GPT-5.1 adaptive: ~2s simple, 10s+ complex, 50% fewer tokens at similar quality
- Agentic wrappers: Refact.ai boosted Claude 3.7 from 76.4% to 92.9% on Aider (+16.5pp), a larger gain than switching to a more expensive model

### Scaling Law Awareness

Code generation scales at N^0.35 with diminishing returns at 34B+ parameters (ICLR 2025). Primary bottleneck is data availability, not model size. Mid-tier models deliver ~90% of frontier quality — the last 10% costs 3-10x more.

---

## 4. Emerging Quality-Adjusted Metrics

No single "correct-lines-per-hour" metric has achieved standard adoption. Emerging frameworks:

- **CTS-SW (Cost to Serve Software)**: Total delivery cost including rework, incidents, review overhead
- **DORA rework rate**: Added as 5th DORA metric in 2025 specifically for AI-code instability
- **Faros 5-dimension framework**: Velocity + Quality + Security + Flow + Satisfaction
- **CodeRabbit 2026 targets**: Churn <10%, coverage >80%, complexity <15, defect density <1%

Industry framing shift: CodeRabbit titled their 2026 outlook "2025 was the year of AI speed. 2026 will be the year of AI quality."

---

## Advisory Assessment

### For Model Selection
1. **No single best model exists.** Task-specific evaluation is mandatory — Claude Opus leads real-world SWE, Gemini leads competitive coding, GPT-5.3 Codex leads terminal tasks.
2. **Cascade routing is the optimal strategy** for the model frontier (ICLR 2025). The 80/20 rule: 80% of tasks can use cheap/fast models.
3. **Gemini 3.1 Pro is the current price-performance champion** — 7.5x cheaper than Opus with competitive scores.

### For Workflow Design
4. **The workflow frontier matters more than the model frontier.** Verification-first workflows are the only demonstrated technique for net-positive quality-adjusted throughput.
5. **The "quality-first AI-assisted" quadrant is unstudied.** This is the largest research gap in the field and the highest-value area for organizational investment.
6. **Quantization degrades coding disproportionately** — 5-10% accuracy loss, especially on reasoning-heavy tasks and low-resource languages.

### Key Uncertainties
- Whether the METR -19% result replicates with experienced tool users on newer models
- Whether the 1.7x defect rate improves with Feb 2026 models (no data yet)
- The magnitude of quality improvement from multi-agent review architectures
- Whether CTS-SW or similar composite metrics gain standard adoption

**Confidence**: High (evidence synthesis), Medium (predictive claims)
**Would change if**: Quality-optimized AI workflow studies are published; newer models demonstrably reduce defect rates; METR RCT replicated with experienced users

---

## Sources

| Source | Type | Tier |
|--------|------|------|
| METR 2025 — AI Developer Productivity RCT | Pre-registered RCT | 1 |
| METR Feb 2026 — Transcript Analysis | Exploratory analysis | 2 |
| Dekoninck et al. ICLR 2025 — Cascade Routing | Peer-reviewed | 1 |
| Stanford HAI AI Index 2025 | Institutional report | 1 |
| Google DORA 2025 Report | Institutional report | 1 |
| Sonar 2026 Developer Survey (n=1,100) | Industry survey | 2 |
| Harness AI Velocity Paradox (n=900) | Industry survey | 2 |
| Uplevel Copilot Study (n=800) | Industry research | 2 |
| CodeRabbit State of Code Quality (n=470 PRs) | Industry report | 3 |
| GitClear 2025 (211M LoC) | Industry research | 2 |
| Greptile State of AI Coding 2025 | Industry report | 3 |
| SWE-bench Verified / LiveCodeBench / Aider | Benchmark leaderboards | 3 |
| Artificial Analysis Feb 2026 | Benchmark analysis | 3 |
| BAMBO arXiv:2512.09972 | Preprint | 2 |
| Zvi Mowshowitz METR Critique | Expert analysis | 3 |

**Evidence quality**: 25% Tier 1, 45% Tier 2, 30% Tier 3
