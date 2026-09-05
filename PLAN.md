# AI Engineering Skills Map and Plan — for outsider builders

> For people who came to software from outside it and are directing coding agents to ship something other people will use. Designed and red-teamed with Claude around one outsider's build, against Andrew Ng's AI Engineering Skills Map (Aug–Sep 2026), then generalized: the map, the rules, the tiers and the sources are ours; the assessment, the sorted gaps and the ninety days are yours to fill in. This file is the guide. `TEMPLATE.md` is the blank you copy. `EXAMPLE.md` is the template as I filled it in, dated, so you can see what finished cells look like — not so you can copy them. Where a section below says *fill in*, it shows one or two of my lines for the grain.

---

## 0 · The position — what will you do, and what won't you do?

Before the map, decide what kind of builder you are trying to become, because the plan changes completely depending on the answer. There are three different things people mean by "reading code":

**Line-by-line comprehension at an engineer's speed.** Reviewing a 400-line diff and seeing the race condition, the missing index, the abstraction that will hurt in six months. This is a decade of pattern library. Some engineers who have it have chosen to stop using it — Robert C. Martin has said he measures coverage, dependency structure, complexity and mutation scores and leaves the code itself to the AI. The difference is that they can fall back to reading when the instruments miss. If you can't, the instruments and the outside reader matter more for you than for them.

**The vocabulary and the failure classes.** The names of the ways software fails — transaction, race, idempotent, N+1, coupling, injection, cascade — and what each one does to a user. Weeks, not years, and non-negotiable whatever you decide, because you cannot ask for an instrument you can't name, and you cannot adjudicate two agents' disagreement without knowing what experiment would settle it. Get the names from outside your own project (OWASP, CWE, the transaction-anomaly names in Kleppmann's chapter 7, Fowler's smells), so your agent isn't the only one teaching you what to look for.

**The minimum reading.** A diff, a stack trace, a schema, a SQL query — well enough to follow what your agents hand you every day, with AI beside you for clarification. Days. Required from hour one. This is not learning to code; it is learning to read the three documents you'll see every day.

Now answer, in writing, in the template:

- **What will you do?** Which of the three will you actually acquire, to what depth, by when?
- **What won't you do?** "I won't learn to write code" and "I won't review code in bulk" are legitimate answers. "I'll pick it up as I go" is not an answer.
- **What will you rent?** Whatever you won't do still has to be done by someone. Name who reads your architecture and your security boundaries, and how often. If you can't name them yet, write the date by which you will.

*One builder's answer (Sept 2026):* I will not learn to write code. I will not be able to review code in bulk — line-by-line comprehension at an engineer's speed is a decade of practice I won't get at fifty. I will get the vocabulary, the failure classes from taxonomies outside my own repo, and the minimum reading, with AI beside me. Reading is rented — later, an outside engineer reads the architecture and the security boundaries, and I'll publish what they find. The rest of the time goes to machines: instruments that look for what a reader looks for, that fail the build rather than decorate a dashboard, and that are themselves under test.

**Five rules that don't depend on your answer or your hours.**

1. **Verify behavior, not vibes.** Every change gets checked by something that isn't the agent that made it — a test, a replay against real data, a second agent in a fresh context, or you, using the product.
2. **Keep a dated record.** What you decided, what you rejected, why. Agents begin every session with no memory; the record is the only past they have. Append; never edit.
3. **Count every miss.** A failure that isn't counted looks like a quiet day. If something can fail silently, add a counter before you add a feature.
4. **Buy security.** You're unlikely to learn it before strangers arrive. Before anyone you don't know uses your product, pay a person to try to break it, and fix what they find.
5. **No strangers before scan, restore, and deletion.** Zero high or critical vulnerabilities in your dependencies (anything you can't fix yet goes on a dated allowlist that expires), a backup you have actually restored, and a way to delete a user that actually deletes them. 

## 1 · The map

Ng's four skills (Aug 14, 2026) and the three detail letters published so far. Part 4 pending.

| Skill | Sub-skills |
|---|---|
| 1 · Building and deploying AI applications (Aug 21) | 1.1 LLM foundations · 1.2 Grounding with data · 1.3 Agentic systems · 1.4 Evaluation-driven development · 1.5 Operating in production · 1.6 ML foundations |
| 2 · Software engineering fundamentals (Aug 28) | 2.1 Full-stack · 2.2 Managing data · 2.3 System architecture · 2.4 Secure and reliable · 2.5 Scaling and operating |
| 3 · Using coding agents (Sept 4) | 3.1 Directing the workflow · 3.2 Enabling autonomy · 3.3 Reviewing the work · 3.4 Customizing agent and environment · 3.5 Coding-agent foundations |
| 4 · Shaping the build (pending) | product sense · business context · identifying problems · MVP-fast vs. build-carefully · ownership |

**Translated for outsiders** — what each sub-skill means when you don't write the code.

*Skill 1.* **LLM foundations:** you need the consequences, not the theory — context windows fill up and things fall off the end; caching changes cost; a model can be retired on sixty days' notice. Learn by being burned, then read Ng's Part 1 once. **Grounding:** what goes in the prompt versus what the model fetches; when a vector index is enough. Defer until your product needs documents. **Agentic systems:** workflows (fixed steps) versus agents (the model decides); start with workflows; Anthropic's *Building Effective Agents* is the whole syllabus. **Evaluation-driven development:** the most important skill on the map, and it does not require code — read your own product's outputs, name the failure categories, count them, build a labeled set, check any automated judge against your own labels. **Operating in production:** counters, alerts, a dated incidents log, cost. **ML foundations:** skip unless you train models; take bias/variance and error analysis, which arrive with the evals work.

*Skill 2.* **Full-stack:** know the parts exist — auth, sessions, caching, async, persistence, accessibility — so you know to ask; accessibility starts with whatever surface your users actually touch. **Managing data:** your schema is the hardest thing to change later; learn to read it, learn enough SQL to query your own tables, know what a transaction is and what happens when two things write at once. **Architecture:** boundaries and tradeoffs; the slow signals (duplication, coupling) are what readers see and you won't — that is what fitness functions are for, with one limit: they hold a line already drawn and don't notice a new one. **Secure and reliable:** reliability you can build toward with tests and structure; security you buy, after the hygiene a machine can do. **Scaling and operating:** deployment, CI, rollback, backups, and what changes at ten times the users.

*Skill 3 — where outsiders can be strongest.* **Directing the workflow:** plan → build → verify → deploy → monitor; small verified steps; a pre-work check of the plan's assumptions against the live system before any change. **Enabling autonomy:** interactive versus delegated versus loop-until-success; the loop needs a stop condition, which is a verifier, which is evals; permissions — the agent must not be able to touch production without you. **Reviewing the work:** tests matched to the task; a second agent in a fresh context; behavior review by you; AI-run security and architecture audits; human review of behavior often and of code rarely — Ng's own words. **Customizing:** a standing context file (CLAUDE.md / AGENTS.md); hooks for the repeatable checks; MCP servers and skills when you know what they're for; post-run retrospectives. **Foundations:** how the agent searches your code, what fills its context, and its failure modes — overengineering, losing rigor without a verifier, stopping short, destructive actions.

*Skill 4.* Product sense, business context, what to build and what not to, when to ship rough and when to build carefully. If you come from operating a business, this is where you start ahead.

## 2 · Where you stand — one line per sub-skill *(fill in)*

The table in the template has one row per sub-skill. For each, write three things.

**Standing** — one line of evidence, not adjectives. "Strong" is not evidence; "94 findings coded into four categories, a replay harness for each" is. If you can't point at an artifact, a number, or an incident, the cell is empty and you should say so.

**Holder** — who actually holds the skill in your build today: **you**, your **agents**, **shared**, or **buy** (someone outside). Be honest about "agents": if the agent does it and you couldn't tell whether it did it well, the holder is the agent alone, and that is a finding.

**Gap** — *none* (you hold it at the level your product needs); *narrow* (a week or two of directed work closes it); *real* (months, or a machine you haven't built, or a person you haven't hired); *structural* (you won't close it; go to §4).

Four of my rows, as of September 2026, so you can see the grain:

| | Standing | Holder | Gap |
|---|---|---|---|
| 1.4 Evals | Front half strong (94 findings coded into categories; grading corpora; replay harnesses); back half missing (held-out set, binary pass/fail, judge TPR/TNR) | shared | **real — highest return** |
| 2.4 Secure & reliable | Reliability strong; **security weakest cell** — the shift-left work in §3 is owed | agents today | **real — the one that hurts strangers** |
| 3.2 Autonomy | Calibration and safety strong (kill switch, spend caps, migrations only on command); parallel sessions run by hand on separate surfaces (voice path, front end); **untried: agent-orchestrated fan-out with a merge step, and loop-until-success with a verifier as the stop condition** | me | real |
| 4.x Shaping | Strongest by career; distribution and the one-sentence answer to "what is this for" are the gaps | me | real |

Date the table. Revisit it when the outside reviewer's findings come back; their corrections to your self-assessment are the most useful data you'll get.

## 3 · The empty cells, sorted *(fill in)*

Every outsider's table has a dozen empty or thin cells. The mistake is calling one of them "the gap." Sort them into three columns.

**Fill on demand** — cells you don't need until the product does, and can fill in weeks when it does. Leaving them empty is correct. Examples for most outsiders: fine-tuning and self-hosting (1.1); knowledge graphs, semantic layers, document pipelines (1.2); computer-use and generative UI (1.3); distillation (1.5); non-relational storage (2.2); monolith-versus-services (2.3); load balancing, sharding, replication (2.5); team context coordination (3.4).

**Owed** — cells where the emptiness *is* the risk, today, to a user. These are the plan. For most outsiders past the first fifty hours: judge validation and held-out sets (1.4); drift detection and prompt-injection defense (1.5); the deletion path (2.2); shift-left security — dependency scan, supply chain, cloud configuration (2.4); accessibility on the primary surface (2.1); a restore drill, a breach playbook, vendor retention, a privacy policy the product can honor (2.4 / 2.5); parallel agents with a stop condition (3.2); user-flow tests and AI-run security and architecture audits (3.3).

**Out of reach** — cells you will not fill, ever, and shouldn't try to. Name them so you stop feeling guilty and start mitigating (§4). For nearly every outsider: ML and deep-learning foundations (1.6), except the two frameworks Ng names inside it — bias/variance and error analysis — which arrive with the evals work.

Our view, for what it's worth: the middle column is where outsiders underestimate themselves and overestimate their agents at the same time. The agent will build a deletion path if you ask; it will not tell you that you owe one.

## 4 · What won't close, and what replaces it

Our view, general. Add your own rows in the template.

| Won't close | Why | Mitigation |
|---|---|---|
| Reading fluency at engineer speed | Decades of pattern library; Böckeler's "20 years mattered most" is about exactly this | Rent it (outside review, on a schedule); fitness functions that fail the build for the slow signals; a canary suite for agent-performance drift |
| Security specialty | Even senior engineers buy it; agent reviewers are noisiest here | Hygiene day now; threat model in OWASP/ASVS vocabulary; paid white-box pentest with an examined-and-clean list; scanning on every build after it |
| ML/DL theory | Not needed unless you train models | Skip; take bias/variance and error analysis from the evals method |
| Statistics beyond counts | — | Husain's method is counts, rates, TPR/TNR; the discipline is the held-out set, and the honesty is stating the interval |
| Debugging pattern library | Speed of recognizing a bug class | Accept the day it costs; treat a recorded cause as a hypothesis until reproduced |

**On fitness functions**, since they carry most of the weight above. They are not dashboards you glance at; they are checks bound to a *named* architectural property with a threshold that *fails the build* (Ford, Parsons & Kua, *Building Evolutionary Architectures*). Five to build once you reach Tier 3: dependency direction, a per-function complexity ceiling, a duplication threshold, a mutation-score floor, and zero high/critical vulnerabilities with a dated allowlist that expires. Read but not gated: hotspots and change coupling from git history (Tornhill), change-failure rate and time-to-restore from your incidents log, test-suite runtime and flake rate. And a fixed canary task suite replayed monthly on a pinned model, re-baselined when that model is retired. Their limit: they hold a line already drawn. Noticing the new line is what the rented reader is for.

## 5 · The plan — by hours, then your ninety days

### Tier 1 — the first 50 hours

You have an idea and an agent. Nothing you build should touch another person's data yet.

*Learn:* the minimum reading (one weekend); the vocabulary as you meet each failure, kept in a list; what a test is and what a passing test does *not* prove; where your production database lives and what can delete it — one builder lost every table on day fourteen to a publish button he hadn't read.

*Build:* the record from day one — a `decisions.md` with dated entries and rejected alternatives; separate development from production before you have anything worth losing.

*Sources:* Anthropic's Claude Code best practices (free, short); Ng's Aug 14 letter (the map itself); a diff/stack-trace/schema explainer of your choice with the agent as tutor; nothing paid.

*Don't:* put anyone else's data in it; take a course yet; believe a green test.

*Exit:* you can explain to someone who wasn't there what your system does and doesn't — and the record agrees with you.

### Tier 2 — 50 to 500 hours

Something works for you and for two people who love you.

*Learn:* evals as a method — Husain's *Evals FAQ* and *Field Guide*: read 30 of your own traces by hand, name the categories, count them, then let an agent help; build ~100 labels, knowing that a hundred gives a wide interval on any judge you check against it — say what number would tighten it; check one automated judge against them. Then how your stack fails: Kleppmann's *DDIA* chapter 1 (the vocabulary of reliability, scalability, maintainability) and chapter 2 (data models). OWASP Top 10 for LLM Applications, as your reading. A weekend of SQL against your own tables.

*Build:* a second agent that reviews the first from a fresh context, and a rule that disputes end in an experiment, not an argument — and when no experiment can settle it, a decision with a revisit date and a note that it's a guess; counters for every silent failure; a regression test for every bug; a dependency scan in CI; your first restore drill, timed.

*Sources:* Husain (hamel.dev, free); DLAI *Spec-Driven Development with Coding Agents* (1h16m, free); Kleppmann ch. 1–2; OWASP LLM Top 10; Huyen, *AI Engineering* ch. 3–4 if you want the textbook. Skip the 10- and 26-hour courses with Python labs.

*Buy:* nothing, except an hour of a domain expert if your product is in their domain.

*Don't:* run parallel agents, install every plugin, read about harnesses. Your bottleneck is verification, not throughput.

*Exit:* a labeled set of ~100 real outputs; one judge checked against your labels; three weeks of reviewing 10–20 new traces a week.

### Tier 3 — 500 to 1,500 hours, and strangers are coming

You have a product, a record, instruments, and people you don't know asking to use it. This is where the outsider's plan diverges from the engineer's, and where the two things you can't learn in time get bought.

*Before the first stranger, in order:*
1. The hygiene day — dependency audit, secret scan, static analysis, database and cloud permission review, restore drill. Results with dates.
2. A threat model you wrote, with the agent mapping it onto your code, in OWASP/ASVS vocabulary so you and the tester mean the same thing.
3. The deletion path, built and tested against a restore. Make it your learning project; it touches every table, backup, log and vendor.
4. What your vendors retain and for how long; a privacy policy the product can honor; a breach playbook — who is told, within what time. If your product touches health, money, or children, a dated answer from counsel on which laws reach it — not a guess, and not the agent's guess.
5. A paid penetration test, white-box, with the list of what was examined and found clean. Remediate every P1. A pentest is a photograph, not a guard: keep scanning on every build, and re-test whenever auth or a data boundary changes.
6. Operations: who answers at 3 a.m., a support channel, cost at ten times the users.

*Learn:* the failure classes from outside your repo — OWASP, CWE Top 25, DDIA chapter 7's anomaly names, Fowler's smells — so the agent can't teach you only what it already knows. Use a different vendor's model as tutor than the one that builds. One human engineer, one hour a month, who picks a part of your system and asks you to explain it; that hour is also how you find your peers.

*Build:* the five fitness functions (§4) and the canary suite. Treat every instrument as a component that can lie — your mutation tool, your backup verifier, your reviewer — and log the date each one did.

*Sources:* OWASP ASVS L1; Ford/Parsons/Kua, *Building Evolutionary Architectures* ch. 2; Tornhill, *Your Code as a Crime Scene* (hotspots, change coupling); Kleppmann ch. 7; Huyen ch. 5 (defensive prompting), 6, 10; Ng's Parts 2 and 3; Laycock, *Maybe We Shouldn't Be Reviewing All This Code*; the Maven evals course only if the free method stalls without office hours — the fee is about the cost of a scoped pentest, and the pentest is the better first spend.

*Don't:* copy this tier into Tier 1. "Don't read code" before the instruments, the restore drill and the record exist isn't a position yet. It's a hope. Build the floor first.

*Exit:* the stranger gate closed line by line with dates; five fitness functions failing CI on a deliberately broken branch; one outside review received, with what your instruments had and had not flagged recorded beside its findings.

### Your next ninety days *(fill in)*

The tiers say what; your ninety days say when. In the template: a weekly hour budget taken from build work, and **the build work you are naming that you will not do while you learn** — a plan with no named cost is a wish. Then three to five phases, each with hours per week, sources, and an exit criterion that someone other than you or your agents can check. Then the standing cost after ninety days — trace review is roughly two hours a week, forever. Then the named thing you have stopped.

*One builder's phases, for shape only:* hygiene day (this week) → evals (four weeks, ~4 h/wk, exit: one judge with TPR/TNR on held-out data) → security and the stranger gate (eight weeks, ~4 h/wk + build, exit: checklist closed with dates, P1s remediated, deletion tested against restore) → the machines (six weeks, exit: five functions failing CI on a broken branch) → fundamentals by interrogation (from then on, 90 min/wk, exit: predictions scored against outside review).

## 6 · Sources of instruction — the catalog, with a verdict

| Source | Verdict | Why |
|---|---|---|
| Husain, *AI Evals FAQ* (hamel.dev/blog/posts/evals-faq) + *Field Guide* (hamel.dev/blog/posts/field-guide), free | **Core** | The method; no code required for the labeling half |
| Husain & Shankar, *AI Evals for Engineers & PMs* (maven.com/parlance-labs/evals, paid) | Conditional | Office hours are the value; homework needs code; a pentest is the better first spend |
| Shankar et al., *Who Validates the Validators?* (arxiv.org/abs/2404.12272) | Read once | Criteria drift — why your labels change as you label |
| DLAI *Evaluating AI Agents* (deeplearning.ai/courses/evaluating-ai-agents, 2.5h, free) | Skim | Python labs; the FAQ is the better text |
| DLAI *Spec-Driven Development with Coding Agents* (deeplearning.ai/courses/spec-driven-development-with-coding-agents, 1h16m, free) | **Take** | Acceptance criteria are the spec form outsiders usually lack |
| DLAI *Agentic AI* (deeplearning.ai/courses/agentic-ai, 10h) | Syllabus only | Python labs; take the vocabulary from the syllabus |
| DLAI *Retrieval Augmented Generation* (deeplearning.ai/courses/retrieval-augmented-generation-rag, 26h, paid) | Defer | Until your product needs documents |
| DLAI *Claude Code: A Highly Agentic Coding Assistant* (deeplearning.ai/courses/claude-code-a-highly-agentic-coding-assistant, 2h, free) | Take, at 2× | Skill 3.5 mechanics |
| Anthropic, *Building Effective Agents* (anthropic.com/engineering/building-effective-agents); Claude Code best practices (code.claude.com/docs/en/best-practices) | **Read** | The field's verification doctrine, short |
| OpenAI, *Harness engineering* (openai.com/index/harness-engineering) | Read | Specs as acceptance criteria; repository knowledge as system of record |
| Ng, *The AI Engineering Skills Map* (deeplearning.ai/the-batch/the-ai-engineering-skills-map, Aug 14, 2026) and the detail letters: Part 1 (deeplearning.ai/the-batch/the-ai-engineering-skills-map-in-detail-building-and-deploying-ai-applications, Aug 21), Part 2 (deeplearning.ai/the-batch/the-ai-engineering-skills-map-in-detail-software-engineering-fundamentals, Aug 28), Part 3 (deeplearning.ai/the-batch/the-ai-engineering-skills-map-in-detail-using-coding-agents, Sept 4) | **Read** | The map itself |
| Huyen, *AI Engineering* (O'Reilly, 2025) ch. 3, 4, 5, 6, 10 | Read | Evals ×2, defensive prompting, RAG/agents/memory, architecture |
| Kleppmann, *Designing Data-Intensive Applications* ch. 1, 2, 7 | **Read** | Reliability/scalability/maintainability vocabulary, data models, transactions |
| OWASP Top 10 for LLM Applications (owasp.org/www-project-top-10-for-large-language-model-applications); OWASP ASVS L1 (owasp.org/www-project-application-security-verification-standard); MITRE CWE Top 25 (cwe.mitre.org/top25) | **Read** (you, not only the agent) | Threat-model and audit vocabulary |
| Ford, Parsons & Kua, *Building Evolutionary Architectures* ch. 2 | Read (Tier 3) | Fitness functions, correctly |
| Tornhill, *Your Code as a Crime Scene* | Skim (Tier 3) | Hotspots, change coupling |
| Laycock, *Maybe We Shouldn't Be Reviewing All This Code* (martinfowler.com/rachels-ramblings/code-review.html, Sept 2, 2026) | Read (Tier 3) | Systems, not diffs; half her moves need a team |
| Willison, *Agentic Engineering Patterns* (simonwillison.net/2026/Feb/23/agentic-engineering-patterns); *Vibe coding and agentic engineering are getting closer than I'd like* (simonwillison.net/2026/May/6/vibe-coding-and-agentic-engineering) | Read | The careful engineer's version of the same trade |
| A SQL primer + a weekend in your own database editor | **Do** | The one form of reading with disproportionate return |
| A short privacy-engineering text | Read (Tier 3) | Retention, deletion, DPAs |
| Fitzpatrick, *The Mom Test* | Read | The customer-conversation gap (Skill 4) |
| Torres, *Continuous Discovery Habits* | Low priority | Written for product teams |
| Beginner Python courses; "build with" tutorials; vendor certificates; AI PM credentials | Skip | Below level, code-author-oriented, or credentials for a market not entered by credentials |

## 7 · What stops *(fill in)*

A plan that adds hours without removing any fails in week three. Write down what stops: the feature that waits, the habit that substituted for the harder thing, the record you'll no longer keep without a `verified-by` column. *Sample:* "the weekly forum thread as a substitute for the monthly human hour."

## 8 · Exit criteria, collected *(fill in)*

One line per phase, each checkable by someone who isn't you and isn't your agent. The tier exits above are the defaults; replace them with your own numbers.

## 9 · Change log

Maintained in `CHANGELOG.md` in this repository — dated entries, newest first, never silent edits. The version you are reading is named in the top line of `CHANGELOG.md` and tagged as a release.
