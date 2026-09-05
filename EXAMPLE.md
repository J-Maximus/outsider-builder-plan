# My skills map and plan — Jonas Leddington

> This assessment is Claude's read of my capabilities in light of what we've built together, not yet my own grading — I have more work to do there. It is offered here only as an example. Later, an outside reviewer will correct my live versions and note corrections in the change log. This example refers only to my ongoing build that has users. The others are left out. 

**Builder:** Jonas Leddington — maximus.work
**Date:** 2026-09-05
**Hours building to date (estimate):** about 1,200 since late April 2026
**What I'm building, in one sentence:** Maximus — a voice-first + SMS assistant with a reliable memory that helps you get where you said you were going.
**Who uses it today:** me and a handful of family members; no strangers yet
**Tier (guide §5):** 3

---

## 0 · The position

**What will I do?**

- Get the vocabulary — the names of the ways software fails: transaction, race, idempotent, N+1, coupling, injection, cascade, fan-in — and the failure classes behind the names, from taxonomies outside my own repo (OWASP, CWE, DDIA's anomaly names, Fowler's smells), so I can ask for an instrument that catches each one.
- Get the minimum reading — a diff, a stack trace, a schema, a SQL query — well enough to follow what my agents hand me every day, with AI beside me for clarification. A weekend of SQL against my own tables first.
- Spend the rest of the time on machines: instruments that look for what a reader looks for, that fail the build rather than decorate a dashboard, and that are themselves under test.

**What won't I do?**

- I will not learn to write code.
- I will not be able to review code in bulk. Line-by-line comprehension at an engineer's speed is a decade of practice I won't get at fifty, and I'm not spending a year trying.

**What will I rent?**

- Later, an outside engineer to read the architecture and the security boundaries. This person is no yet named and the cost isn't clear to me yet; my intent is to use that review to check what my instruments caught and missed, and to publish what it finds. A paid white-box penetration test before the first stranger. One human engineer hour a month as a tutor who picks a part of the system and makes me explain it.

## 2 · Where I stand — one line per sub-skill

Holder: **me** · **agents** · **shared** · **buy**. Gap: none / narrow / real / structural.

| | Standing (evidence) | Holder | Gap |
|---|---|---|---|
| 1.1 LLM foundations | Deep by consequence (speech-vendor caps, bring-your-own-key, a prompt-cap incident, model choice made on the noise floor); thin on theory | shared | narrow |
| 1.2 Grounding with data | pgvector, a four-layer memory, provenance on every fact; no document pipelines, graphs, or semantic layers — a later build will need them | shared | narrow → real later |
| 1.3 Agentic systems | Seven worker loops, an outbox, supersede chains, structural guardrails | shared | none |
| 1.4 Evaluation-driven development | Front half strong (94 dogfood findings coded into categories; grading corpora; replay harnesses); back half missing (held-out set, binary pass/fail, judge TPR/TNR) | shared | **real — highest return** |
| 1.5 Operating in production | Counted misses with false-positive budgets, alarms, a dated incidents log, audits as scheduled work; no drift detection, no prompt-injection defense | shared | narrow / real on injection |
| 1.6 ML foundations | None | — | **structural** |
| 2.1 Full-stack | A live web front end on hosted services and a managed Postgres; account page owed; accessibility untested — and for an 81-year-old the voice *is* the accessibility surface | agents; me on product | narrow |
| 2.2 Managing data | Strongest fundamentals: append-only, supersede, unique-index-not-flag, advisory locks | shared | real (lifecycle) |
| 2.3 System architecture | Pure-core / impure-edge doctrine, unenforced; slow signals unmeasured | shared | real |
| 2.4 Secure and reliable | Reliability strong; **security weakest cell** — the shift-left work in §3 is owed | agents today | **real — the one that hurts strangers** |
| 2.5 Scaling and operating | CI, hooks, cost per turn known; untested past six accounts | shared | narrow until beta |
| 3.1 Directing the workflow | Pre-work packet checked against the live system, cumulative surfaces, founder-held merges; specs are decisions, not acceptance criteria | me | narrow |
| 3.2 Enabling autonomy | Calibration and safety strong (kill switch, spend caps, migrations only on command); parallel sessions run by hand on separate surfaces (voice path, front end); **untried: agent-orchestrated fan-out with a merge step, and loop-until-success with a verifier as stop condition** | me | real |
| 3.3 Reviewing the work | Functional review strong; behavioral via dogfooding; a second agent in a fresh context; **judge validation, AI-run security and architecture audits, user-flow tests not run** | shared | real |
| 3.4 Customizing agent and environment | CLAUDE.md with a check-the-record gate, handoffs, one hook; **MCP / skills / plugins ecosystem unknown** | me | real (cheap) |
| 3.5 Coding-agent foundations | Failure modes: published and argued; mechanics (retrieval, context accounting, harness) thin | me | narrow |
| 4.x Shaping the build | Strongest by career; distribution and the one-sentence answer to "what is Maximus for" are the gaps | me | real |

*Assessed on:* 2026-09-05 (Claude's read; my own grading pending)  *Corrected by outside review on:* ______

## 3 · The empty cells, sorted

| Fill on demand | Owed | Out of reach |
|---|---|---|
| Fine-tuning, self-hosting (1.1) · graphs, semantic layers, document pipelines (1.2) · computer-use, generative UI, MCP in-product (1.3) · distillation (1.5) · non-relational storage (2.2) · monolith-vs-services (2.3) · load balancing, sharding, replication (2.5) · team context coordination (3.4) | Judge validation and held-out sets (1.4) · drift detection, prompt-injection defense (1.5) · the deletion path, built and proven (2.2) · shift-left security: scan, supply chain, cloud config (2.4) · accessibility on the voice surface (2.1) · agent-orchestrated fan-out and loop-until-success with a stop condition (3.2) · user-flow tests; AI security/architecture audits (3.3) · MCP/skills/hooks (3.4) · a restore drill, a breach playbook, vendor retention, a privacy policy the product can honor, the regulatory sentence (2.4 / 2.5) | ML/DL foundations, training models (1.6). Bias/variance and error analysis arrive with the evals work. |

About a dozen, sorted. Never "the only gap." The middle column is the plan.

## 4 · What won't close, and what replaces it

The guide's five rows, as written, plus none of my own yet. The one I'd add after an outside review is whatever the reviewer found by inspection that no instrument flagged.

## 5 · My next ninety days

**Weekly hours taken from build work:** six
**The build work I am naming that will not happen while I learn:** design work on two other builds waits until the stranger gate and the eval loop both run
**Standing cost after ninety days:** ~2 h/week of trace review, forever; the method transfers to the other builds, the instruments don't

| Phase | Weeks | Hours/week | Sources | Exit criterion (checkable by someone who isn't me or my agent) |
|---|---|---|---|---|
| Hygiene day — dependency audit, secret scan, SAST, RLS and cloud-config review, restore drill, all dated | this week | one day | the tools' own docs; OWASP ASVS L1 for checklist language | five numbers and a restore time in the incidents log |
| Evals — 30 traces by hand, then ~100 labels, binary, split; validate the extraction judge on the held-out set; set the weekly cadence | Sept | ~4 | Husain FAQ + Field Guide; Shankar, *Who Validates the Validators?*; Huyen ch. 3–4 | one judge with TPR/TNR and the interval stated on held-out data; three consecutive weeks of 10–20 traces reviewed |
| Security and the stranger gate — threat model in OWASP/ASVS vocabulary; the deletion path, built and proven against a restore, as the learning project; vendor retention and DPAs; the regulatory sentence from counsel, dated; breach playbook; white-box pentest with examined-and-clean list; scanning stays on every build | Oct–Nov, 8 | ~4 + build | OWASP LLM Top 10; ASVS; Huyen ch. 5; the database vendor's row-level-security docs; a short privacy-engineering text; counsel | stranger-gate checklist closed line by line with dates; pentest received, every P1 remediated; deletion path proven against a restore |
| The machines — five build-failing fitness functions (dependency direction, complexity ceiling, duplication threshold, mutation floor, zero high/critical with a dated allowlist); read-only signals; canary suite on a pinned model, re-baselined on retirement | Nov–Dec, 6 | ~2 + build | Ford/Parsons/Kua ch. 2; Tornhill; DORA definitions | five functions failing CI on a deliberately broken branch; canary suite run twice, a month apart |
| Fundamentals by interrogation — external taxonomies mapped onto the repo; a different vendor's model as tutor; every session ends in a prediction that outside review can score; one human engineer hour a month | from Jan, ongoing | 1.5 | Kleppmann ch. 1, 2, 7; Huyen ch. 6, 10; Ng Parts 1–3; OWASP/CWE; a SQL primer | predictions scored against outside review; four human hours done |

## 7 · What stops

- Design work on the other builds, until the gate and the loop run.
- The weekly forum thread as a substitute for the monthly human hour.
- Any new record without a `verified-by` column.
- "The log is the deliverable" as an exit criterion.
- Settling architectural disputes by asking what experiment would settle them when no two-minute experiment exists — those get a decision with a revisit date and a note that it's a guess.

## 8 · Exit criteria, collected

| Phase | Criterion |
|---|---|
| Hygiene | Five numbers + restore time in the incidents log |
| Evals | One judge with TPR/TNR and interval on held-out data; three weeks of cadence |
| Security | Stranger-gate checklist closed with dates; P1s remediated; deletion path proven against a restore |
| Machines | Five fitness functions failing CI on a broken branch; canary run twice |
| Fundamentals | Predictions scored against outside review; four human hours |

## 9 · Change log

- 2026-09-05 — v1. First assessment. Self-assessed; not yet corrected by an outside reviewer.
