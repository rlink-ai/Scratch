# AI Project Executive
## A State-Driven, OODA-Based Architecture for Project Management

**Concept document for further review**
**Revised:** September 10, 2026

---

## 0. Reading This Document — Two Audiences, One System

This system serves two very different kinds of users, and much of its product
success depends on serving both without forcing either to become the other.

- **Trained project managers** — people fluent in schedules, dependencies,
  risk, and governance. For them the AI Project Executive is a force multiplier:
  it offloads the continuous cognitive work of maintaining an accurate picture
  of a project so they can focus on judgment, stakeholders, and strategy.

- **People who are *not* trained project managers** — engineers, founders,
  functional leads, and operators who own projects without formal PM training.
  For them the AI Project Executive is not an assistant that helps them do PM
  work faster; **it supplies the project-management competence they do not
  have.** It is, in effect, the project manager.

The **internal architecture is the same for both** — the same situation model,
the same OODA loop, the same governance. What differs is the **surface**: how
much project-management machinery is exposed, how prescriptive the guidance is,
and how much the system does *for* the user versus *with* them.

A guiding principle throughout:

> **The sophistication belongs inside the system. The surface a user sees
> should match how much project-management expertise that user actually has.**

Sections 1–20 describe the shared architecture. **Sections A and B** then
describe how the product should behave differently for each audience.

---

## 1. Executive Summary

Traditional project-management software is primarily a **system of record**. It
stores tasks, dates, owners, milestones, risks, documents, and status updates,
but generally relies on humans to interpret what those facts mean and decide
what should happen next.

The proposed **AI Project Executive** changes that role. It is a persistent AI
persona with authorized access to the project's operating information and
responsibility for continuously maintaining an understanding of the project.

Rather than waiting for a human to formulate the next prompt — or even waiting
for something to happen — the Project Executive is **proactive**: it
continuously reasons forward from the project's goals and plan, anticipating what
needs attention. It uses an ongoing **OODA loop — Observe, Orient, Decide, Act**,
entered both reactively (when the world changes) and, primarily, proactively (on
its own initiative, looking ahead), to assess:

- What changed?
- What was completed?
- What was expected but did not happen?
- What do those changes mean relative to goals and plans?
- What is now at risk or newly possible?
- What work should happen next?
- What should be stopped or deferred?
- What decisions require human judgment or authority?
- What should simply be watched?

The resulting product is less a conventional project-management application with
an AI assistant and more a **Project Operating System with an AI Executive**.

> **Traditional PM software records what the team says the state of the project
> is. An AI Project Executive continuously constructs, tests, and updates its
> own understanding of the project — and manages what should happen next.**

**Why the two audiences matter to the thesis.** For a trained PM this is a
better cockpit. For a non-PM it is something more fundamental: access to
management competence they would otherwise have to hire, learn, or go without.
The second audience is larger and has a sharper unmet need — and it is the one
most easily under-served by a product designed by and for experts.

---

## 2. From Project Tracking to Project Management

A conventional PM system might contain:

```text
Task 147
Owner: Susan
Due: September 10
Status: In Progress
```

An AI Project Executive could understand the same task as:

```text
Task 147
Owner: Susan
Due: September 10
Status: In Progress

Dependency:
Vendor specification

Expected vendor specification:
September 7

Actual receipt:
September 9

Resource constraint:
Susan moves to Project Beta on September 14

Historical duration for similar work:
4.2 days

Current estimate:
~3 days remaining

Downstream dependency:
Task 151 cannot begin until Task 147 completes

Milestone:
September 16

Executive interpretation:
The milestone has approximately 1–2 days of remaining slack.
```

The system therefore moves from storing **declared project state** to
maintaining a **computed situation model**.

Note that the interpretation ("about 1–2 days of slack") is the part a trained
PM could derive themselves and a non-PM usually cannot. The system computes it
either way; the difference is only whether it is shown as raw analysis (for the
PM) or translated into a plain consequence (for the non-PM) — see Sections A
and B.

---

## 3. The AI Project Executive Persona

The AI should be treated as a persistent project participant rather than merely
a chat interface.

For example:

```text
PROJECT TEAM

Jane       Product
Sam        Engineering
Maria      Design
Alex       Customer
Atlas      AI Project Executive
```

The Project Executive might own responsibility for:

- project-state integrity;
- dependency awareness;
- expectation tracking;
- risk identification;
- unresolved decision tracking;
- commitment tracking;
- schedule reasoning;
- cross-project conflicts;
- project memory;
- retrospective learning;
- preparation of human decision packages; and
- orchestration of specialist agents and models.

Users can then ask questions such as:

- Why did launch risk increase?
- What changed since Monday?
- What are we waiting for?
- Which commitments are overdue and actually consequential?
- What decisions need attention?
- What assumptions are becoming questionable?
- What work no longer makes sense?
- What are you watching but not acting on yet?

The persona answers from the same persistent situation model it uses to manage
the project.

---

## 4. Information Available to the Executive

Subject to permissions and governance, the Project Executive could have access
to:

- project objectives and success criteria;
- tasks, milestones, dependencies, and schedules;
- historical schedule performance;
- resource assignments and availability;
- budgets, forecasts, and expenditures;
- specifications and project documents;
- meeting notes and transcripts;
- decisions and decision history;
- project-related email and collaboration messages;
- issues and risks;
- change requests;
- customer and stakeholder feedback;
- commitments made by team members;
- assumptions;
- expected future events;
- agent activity and results;
- organizational policies and authority limits; and
- previous OODA episodes and lessons.

A crucial design principle is:

> **Universal authorized access does not imply universal attention.**

The AI may be permitted to access a large information universe while admitting
only a small, relevant subset into any individual reasoning cycle.

---

## 5. OODA as the Project Management Control Loop

The Project Executive operates using an ongoing OODA model. Critically, the loop
is entered from **two directions**: reactively, when the world changes; and
proactively, when the Executive's own forward reasoning identifies something that
warrants orientation even though nothing has "happened."

```text
     PROJECT STATE / WORLD                GOALS / PLAN / FORECAST
   (reactive: something changed)      (proactive: looking ahead on
              |                          the Executive's own initiative)
              |                                    |
              +---------------------+--------------+
                                    |
                                    v
                                 OBSERVE
                       (changes AND anticipated futures)
                                    |
                                    v
                                  ORIENT
                                    |
                                    v
                                  DECIDE
                                    |
               +----+----+---------+----------+---------+
               |         |         |          |         |
               v         v         v          v         v
              ACT      WATCH     HUMAN      INITIATE   INVESTIGATE
                                 DECISION   (start     (go obtain
               |         |         |         work)     missing info)
               +---------+---------+----------+---------+
                                    |
                                    v
                              PROJECT STATE
                                    |
                                    +------> repeat (and keep looking ahead)
```

### Observe
Determine what changed **and what is coming**. Reactive observation includes
task completion; missed dates; document changes; new messages; meeting outcomes;
agent results; budget changes; resource changes; new risks; decision outcomes;
and expected events that failed to occur. **Proactive observation** includes
approaching dependencies and milestones, resource windows opening or closing,
assumptions aging past their validation horizon, and risks trending toward
realization — none of which require an external event.

### Orient
Interpret the observation relative to project goals; current plan; dependencies;
assumptions; constraints; resources; commitments; historical experience;
organizational policy; and human authority. Orientation asks not only "what does
this change mean?" but "given where the project is heading, what is forming that
we should get ahead of?"

### Decide
Determine what deserves attention. A decision may be to act; delegate;
investigate; replan; ask a human; escalate; watch; defer; ignore; stop existing
work; **proactively initiate work to preempt a future problem**; **go obtain
information the Executive does not yet have**; or take no action.

### Act
Execution may be performed by the Project Executive itself or delegated to a
bounded agent or specialist system. Action includes proactive moves — starting
preparatory work, requesting an estimate before it is overdue, or validating an
assumption before it fails — not only responses to things that already broke.

---

## 6. A Dual-Drive Control Model: Proactive First, Event-Aware Second

A purely event-driven system is fundamentally **reactive** — something must
happen in the world (a task completes, an email arrives, a deadline nears)
before the Executive thinks. That is necessary but insufficient. A real project
executive does not wait to be poked. It **looks ahead**, **goes looking for
problems before they surface**, **initiates work and inquiry on its own
authority**, and **anticipates what should happen next**. Foresight — not
reaction — is the defining behavior of management.

The Project Executive is therefore driven by **two forces**, with the proactive
force primary:

**1. Proactive / goal-driven (primary).** On its own initiative, continuously
and without any triggering event, the Executive reasons *forward* from goals,
plans, dependencies, and expectations:

- What is coming that the project is not yet ready for?
- Which dependencies, resource windows, or milestones are approaching, and is
  the upstream work positioned to meet them?
- Which assumptions have gone stale and should be re-validated *before* they
  fail?
- Where is risk *forming* — not yet realized, but trending toward realization?
- What work should start *now* to prevent a future problem or preserve a future
  option?
- What has quietly stopped mattering and should be reconsidered?
- What information is missing that the Executive should go and obtain rather than
  wait to receive?

None of these require an event. They arise from the Executive's own
forward-looking agenda: a continuous scan of the project's *future* state
against its goals.

**2. Reactive / event-aware (secondary).** Events remain valuable inputs. The
underlying software can and should be event-driven at the infrastructure level:
task completed, task overdue, email received, document changed, meeting
concluded, decision recorded, new issue raised, agent completed work, budget
changed, deadline approaching, dependency changed, an expected event that did
*not* occur, or a periodic heartbeat.

But an event does **not** prescribe an action, and — more importantly — the
absence of events does **not** imply the absence of management. An event is an
*additional* signal that may **accelerate** a re-orientation the Executive would
have reached on its own; it is not the sole trigger for thought.

> **The Executive continuously reasons forward from goals and anticipates what
> needs attention. Events are additional signals that may accelerate that
> reasoning — not the only reason the Executive thinks.**

**Proactive does not mean constantly acting.** The discipline described
elsewhere in this document — no-op, defer, watch, and stop are valid decisions;
do not interrupt humans needlessly — still holds. Proactivity governs *attention
and anticipation*, not *action volume*. The Executive is always thinking ahead
and hunting for what matters; it still exercises judgment about whether to act,
watch, or wait. Constant foresight, selective action.

This dual-drive model is what separates an *Executive* from an *automation*. An
automation waits for a trigger and fires a rule. An Executive maintains a
forward view of the project and acts on its own reading of what the project
will need — using events to sharpen, not to summon, its attention.

---

## 7. Expectations as First-Class Project Objects — the Machinery of Foresight

Project management depends heavily on expected future states. Expectations are
the **primary infrastructure of proactivity**: by explicitly recording what
*should* happen and by when, the Executive can manage the future rather than only
audit the past, and can detect problems by their *absence* rather than waiting
for a problem to announce itself.

```text
ACTION
Send proposal to customer

EXPECTED EFFECT
Customer receives proposal

EXPECTED RESPONSE
Acceptance, questions, or rejection

EXPECTED BY
September 15

IF EXPECTATION IS VIOLATED
Return the item to Executive attention
```

This allows the system to detect meaningful cases where **nothing happened** —
the difference between expected and observed state creates the signal, with no
external trigger required. It also lets the Executive act *before* the deadline:
as an expected-by date approaches, the Executive can proactively check progress,
nudge, or prepare a contingency rather than waiting to discover a miss after the
fact. OODA therefore extends to a forward-looking cycle:

> **Observe → Orient → Decide → Act → Expect → (anticipate) → Observe**

Every significant action creates an expected future state, and every expected
future state becomes something the Executive actively watches toward — the
mechanism by which a proactive Executive keeps its attention pointed at what is
coming, not only at what has occurred.

---

## 8. Commitments as Managed Objects

Projects contain large numbers of informal human commitments ("I'll get that to
you Tuesday," "I'll ask Legal"). The Executive can convert these into structured
objects:

```text
COMMITMENT
Who: Sam
What: Provide revised estimate
To whom: Project team
Expected: Tuesday
Source: Engineering meeting
Status: Open
```

When Tuesday passes, the system should not automatically generate a reminder. It
first asks:

> **Does this unmet commitment matter yet?**

If no downstream work depends on the estimate until Thursday, the Executive may
defer attention. This differentiates Executive management from simple reminder
automation.

---

## 9. Meetings Become State Changes, Not Dead Documents

A meeting statement such as "Let's keep the existing vendor unless they slip
past Friday" can be extracted as:

```text
DECISION      Retain vendor
CONDITION     Unless delivery slips past Friday
AUTHORITY     Jane
EXPECTATION   Vendor delivery by Friday
IF VIOLATED   Re-open vendor decision
```

If Friday passes without delivery, the system recognizes that the condition
underlying Jane's decision is no longer true, and the vendor decision is
reopened for orientation — considerably more useful than storing a meeting
summary.

---

## 10. Constructing Work Rather Than Waiting for Prompts

One of the most important capabilities is the Executive's ability to construct
the next unit of work.

```text
Observed:            API delivery is two days late
Dependency chain:    API -> Integration -> System Test -> Acceptance -> Launch
Historical:          Typical integration duration 3.8 days
Plan allowance:      2 days
Constraint:          Integration engineer unavailable September 15
```

The Executive may orient that the API delay alone does not yet threaten launch,
but another 24–36 hours would push integration into the engineer's unavailable
period. It may then decide to obtain a revised vendor estimate, identify
alternate coverage, set a 24-hour watch, and **avoid interrupting a human until
a meaningful threshold is crossed.** This is active management rather than
tracking.

---

## 11. The Information Governor

Giving the AI access to all project information creates an attention problem.
The solution is an **Information Governor** that determines what should
influence each OODA cycle, scoring relevance, applicability, provenance,
recency, confidence, dependency, causality, authority, and contradiction.

Information can be **injected** (materially relevant now), **deferred**
(potentially relevant, below threshold), **rejected from current cognition**
(irrelevant now but retained), **quarantined** (unreliable or contradicted), or
**retired/superseded**.

The goal is **decision-relevance retrieval**, not merely semantic similarity.

---

## 12. Human Attention Management

The human should not be required to approve every action. The Executive asks:

> **At what point does human judgment or authority have greater expected value
> than continued autonomous work?**

Human involvement can occur at any stage — correcting reality (Observe), framing
or assumptions (Orient), preferences and tradeoffs (Decide), authority for
consequential action (Act), qualitative success (Evaluate), or whether a lesson
should become policy (Learn). Escalation considers uncertainty, consequence,
reversibility, authority, and strategic judgment.

The Executive manages a **human attention budget**, consolidating issues into
concise decision packages rather than repeatedly asking open-ended questions.

**This section is where the two audiences diverge most sharply**, because a
"decision package" that a trained PM can adjudicate may be exactly what a non-PM
cannot. How escalation and decisions are presented is addressed in Sections A
and B.

---

## 13. Executive Dashboards

A traditional dashboard emphasizes counts (72% complete, 4 overdue, 3 risks). An
Executive dashboard answers management questions instead:

- **What changed** — integration is two days behind; customer accepted the
  revised workflow; Legal approved the contract.
- **What it means** — launch remains achievable, but slack fell from eight days
  to three.
- **What the AI is doing** — obtaining a revised vendor estimate; modeling
  alternate coverage; monitoring the acceptance dependency.
- **What humans need to do** — one decision: approve temporary engineering
  reassignment by Thursday.
- **What the AI is watching** — vendor delivery Friday; test failure rate;
  customer sign-off.
- **What the system has learned** — integration on this product family has
  historically run ~35% longer than initial estimates.

The dashboard becomes an answer to:

> **How is the project actually doing, and what deserves attention?**

The *content* is the same for both audiences; the *language and prescriptiveness*
differ (Sections A and B).

---

## 14. Project Graph Rather Than Task List

The information model should be a graph of project relationships — goals,
milestones, tasks, decisions, requirements, risks, metrics, people, commitments,
resources, dependencies, documents, meetings, customers, expectations, agents,
and events — rather than a flat task table. The Executive reasons over these
relationships to discover effects not obvious from individual records.

---

## 14a. Constructing the Project Graph — the Hardest and Most Important Problem

The entire value of this system rests on the project graph existing. The
Executive's foresight, its cross-cutting reasoning, its ability to see that a
stale decision is blocking a milestone or that an assumption has been quietly
contradicted — all of it depends on a rich, connected graph of tasks,
dependencies, decisions, assumptions, commitments, expectations, requirements,
resources, goals, and authority.

**That graph does not exist in most project systems today, and it cannot be
built the obvious way.** Conventional tools capture tasks, dates, owners, and
perhaps basic schedule dependencies — roughly the information in a Gantt chart.
They do not capture decisions and their conditions, assumptions and their
validity horizons, informal commitments, expectations, requirement-to-work
links, or cross-project resource conflicts. The graph the Executive needs is
mostly *not in the data*.

This is the central feasibility problem, and it is worth stating plainly:

> **Constructing and maintaining the project graph is a harder and more important
> problem than the reasoning that consumes it. The reasoning is downstream of a
> graph that, today, must be built.**

### Why manual capture is the wrong answer

The tempting solution is to add fields and forms and ask users to record
dependencies, decisions, assumptions, and commitments. This is precisely the
approach that fails in practice, and it fails hardest for the audience this
product most wants to serve:

- It is tedious, and tedious data decays. Rich structured entry is abandoned
  under deadline pressure.
- It requires exactly the project-management discipline that non-PMs lack. A
  non-PM will not diligently record "this task assumes Susan is available through
  the 22nd" or "this decision is conditional on vendor delivery."
- Every PM tool already offers rich-data entry; almost none achieves rich data,
  because the burden falls on humans who have better things to do.

Manual capture would make the graph an aspiration, not a reality.

### The core bet: infer the graph from how people already work

The graph should be **inferred and confirmed, not authored.** People already
produce the raw material from which the graph can be extracted — they hold
meetings, send email, exchange chat messages, write documents, and create tasks.
Buried in that ambient communication are the dependencies, decisions,
commitments, assumptions, and expectations the graph needs.

The Executive's job therefore includes **constructing the graph** by extracting
structure from unstructured sources:

- **Meetings and transcripts** yield decisions, conditions, authority,
  commitments, and expectations (see §9 — "Let's keep the vendor unless they slip
  past Friday" becomes a conditional decision with an expectation and an
  if-violated edge).
- **Email and chat** yield commitments ("I'll get that to you Tuesday"), emerging
  risks, and stakeholder expectations.
- **Documents and specifications** yield requirements and the claims that must be
  satisfied by work.
- **Existing tasks and their language** yield implied dependencies and
  assumptions that were never formally recorded.

This inference-over-entry approach is not merely a convenience. It is:

1. **What makes the graph real** rather than aspirational — it is built from work
   that already happens, not from data-entry that mostly does not.
2. **What makes the product viable for non-PMs** — they cannot and will not
   author the graph, but they *do* talk, write, and message. The AI extracts the
   structure they cannot articulate. This is the concrete mechanism behind the
   non-PM promise that "the AI constructs the project structure for them."
3. **The differentiator and the moat** — "enter all your dependencies and we will
   reason over them" is what every tool promises and none delivers. "We infer the
   project graph from how you already work, so you get the reasoning without the
   data-entry burden" is a categorically stronger and harder-to-copy proposition.

### Inference must be epistemically honest

An inferred graph is only as trustworthy as the extraction that produced it, and
a wrong inferred edge can mislead the Executive into confident, incorrect
foresight — which is worse than no foresight, especially for a non-PM who cannot
catch the error. Graph construction must therefore carry the same epistemic
discipline the system applies to its conclusions (Appendix G), applied now to the
*graph itself*:

- **Confidence** — how sure is the Executive that this dependency, decision, or
  commitment is real and correctly linked?
- **Provenance** — where was it extracted from (which meeting, which email, which
  document), so a human can trace and verify it?
- **Confirmation of the consequential** — high-stakes inferred edges (a
  dependency that puts a milestone at risk, a decision that blocks compliance)
  should be surfaced for lightweight human confirmation in plain language ("It
  sounds like the payout work can't start until the vendor spec arrives — is that
  right?"). The user *validates* rather than *authors* — a far lower burden, and
  one even a non-PM can bear.
- **Decay and revalidation** — inferred structure ages; assumptions and
  dependencies extracted weeks ago may no longer hold and must be revisited.

### The cold-start and sparse-source problem

Inference requires source material. A project with rich communication — regular
meetings, active email and chat, living documents — offers a great deal to
extract from. A project that is sparse, siloed, or early may offer little, and
the graph will be correspondingly thin.

Open questions the design must answer:

- What is the **minimum viable input** from which a useful graph can be built?
- How does the Executive **bootstrap** a graph when little unstructured material
  exists — by asking a small number of high-value plain-language questions,
  rather than demanding structured entry?
- How does the graph **grow incrementally** as more communication accumulates, so
  the system becomes more capable over the life of the project rather than
  requiring completeness up front?
- How does the Executive **signal the thinness of its own graph** — telling the
  user, honestly, "I don't yet have enough about this project to reason well
  about X"?

### Implication

The concept should be read with this correction in mind: wherever earlier
sections treat the project graph as available input, that availability is not
free. **A first-class capability of the Project Executive is to build and
maintain the graph itself, by inference from the way people already work,
confirmed lightly where it matters, and honest about its own confidence and
gaps.** This is simultaneously the concept's largest feasibility risk and its
strongest source of differentiation.

### A pragmatic path: recommend from partial data, let review complete the graph

The full inference approach above is powerful but advanced. There is a more
pragmatic path that dramatically lowers the feasibility bar and can serve as the
starting point.

Today, teams typically capture tasks, dates, owners, and Gantt-style schedule
dependencies. That is not the full graph — but it is enough to reason *partially*.
Rather than requiring a complete graph before it can act, the Executive can:

1. **Reason over the information at hand** — tasks, dates, dependencies, and
   whatever notes and context exist — even though the picture is incomplete.
2. **Make recommendations from that partial picture**, expressed with explicit
   confidence and an honest account of what it is assuming or missing.
3. **Let the human review** each recommendation — and use that review as the
   mechanism that *completes and corrects the graph over time.*

This inverts the dependency between graph and reasoning. Instead of *"build the
complete graph, then reason,"* it becomes *"reason from what exists, recommend,
and let human review enrich the graph as a byproduct."* Every recommendation a
human confirms, rejects, or refines teaches the graph — a confirmed dependency
becomes a known edge, a corrected assumption updates state, an added piece of
context fills a gap. The graph **emerges through use** rather than being entered
up front. Teams effectively *back into* the richer dependency structure through
Gantt-level data plus the Executive's suggestions, refined by review.

This is a gentler on-ramp: it works from data teams already keep, it produces
value on day one instead of after a graph-building project, and it makes the
human the graph-completion loop rather than the data-entry clerk.

**It also raises genuine technical and UX questions that the design must
answer:**

- **Confidence under incompleteness.** How does the Executive express that it is
  reasoning over partial data — "I believe X, but I'm missing Y" — so a human
  weights the recommendation appropriately rather than trusting it uniformly?
- **Review as graph-building.** When a human confirms or corrects a
  recommendation, does that action *update the graph* — turning an inferred guess
  into a confirmed edge, or removing a wrong one? The feedback loop is the
  construction mechanism, and it must be designed as such, not as a throwaway
  approval.
- **Surfacing the unknowns.** How much should a recommendation reveal about what
  the Executive *doesn't* know — e.g., "this assumes the vendor task blocks
  integration; confirm?" — so review also closes the most consequential gaps?
- **Review friction.** How is review kept lightweight — a glance and a click —
  especially for non-PMs, so it does not become manual data entry wearing a
  different hat? If reviewing is as tedious as entering, the approach fails for
  the same reason manual capture fails.
- **Recommend versus ask.** With thin data, when should the Executive make a
  recommendation anyway (and flag its uncertainty) versus first ask a short
  clarifying question? Too many questions is data entry; too few is confident
  guessing.
- **Trust calibration over time.** As the human confirms good recommendations and
  corrects bad ones, how does the system earn increasing autonomy — reviewing
  less as its graph and track record improve?

The recommend-and-review model is therefore both a pragmatic starting point
*and* a graph-construction engine: it delivers value from Gantt-level data
immediately, while the human review loop quietly builds the richer graph that
enables the deeper reasoning described throughout this document.

---

## 15. Project Debt

The Executive can identify **project debt**: unresolved cognitive or
organizational structure that accumulates during execution — undocumented
decisions, stale assumptions, unanswered questions, ambiguous ownership,
commitments without dates, requirements without implementation, unverified
completed work, decisions whose assumptions changed, unclosed risks, and
temporary workarounds that became permanent.

It periodically asks:

> **What unresolved structure is accumulating, and when will it become
> consequential?**

For non-PMs especially, surfacing project debt is high-value: they are the least
likely to notice it accumulating.

---

## 16. Knowing When to Stop Work

Conventional systems are completion-biased. An Executive repeatedly asks:

> **Does this work still contribute to an active goal?**

If Customer X withdrew the requirement that justified a task, the Executive
should recommend cancellation rather than continuing work merely because the
task exists.

---

## 17. Nested Project and Portfolio Executives

The OODA model can be hierarchical: a Portfolio Executive orienting across
multiple Project Executives. If Project A needs Sarah for another week and
Project B depends on her for a critical milestone, neither Project Executive
resolves the conflict alone — the Portfolio Executive orients across both and
either allocates under delegated authority or prepares the decision for a human
portfolio owner. This provides natural escalation across organizational levels.

---

## 18. Specialist Small Language Models

The Executive can orchestrate narrow-domain SLMs — Schedule, Risk, Resource,
Requirements, Financial, and Stakeholder — rather than relying on one model for
every cognitive task. The Executive combines their outputs and maintains
authority over the overall orientation.

---

## 19. Learning Across Projects

Every significant OODA cycle can become a structured decision episode
(observation, prior state, orientation, assumptions, options, decision, action,
expected outcome, actual outcome, human correction, lesson). Across many
projects the organization learns patterns — which vendors are optimistic, which
work is underestimated, which mitigations work under which conditions. This
becomes **organizational experience**, not generic PM knowledge.

---

## 20. Context, Memory, Policy, and Model Evolution

| Layer | Example | Role |
|---|---|---|
| Context | Vendor is three days late | Influences the current cycle |
| Memory | Vendor historically slips after holidays | Mutable organizational knowledge |
| Policy | Compare vendor estimates with historical performance | Explicit, inspectable procedure |
| Model weights | Recognizing complex schedule-risk patterns | Stable learned capability |

The learning hierarchy is:

> **Context → Memory → Policy → Model capability**

Movement deeper into the system requires progressively stronger evidence.
Individual experiences enter episodic memory first; repeated, validated patterns
can become semantic knowledge or policy; only stable, generalizable skills
become candidates for model adaptation. (Governance, explainability, and
epistemic transparency — the original Sections 21–23 — are retained in Appendix
G and continue to apply to both audiences.)

---

# Part Two — Designing for Two Audiences

The shared architecture above produces a single situation model and a single set
of conclusions. What must differ is **how the product presents itself** to users
with very different levels of project-management expertise. The same underlying
Executive drives both experiences; only the surface changes.

---

## A. For Trained Project Managers — the Executive as Force Multiplier

**Who they are.** Professional or experienced project managers who already think
in terms of critical path, slack, dependencies, risk exposure, and governance.
They can read a schedule, challenge an estimate, and adjudicate a tradeoff.

**What the AI is to them.** A tireless analyst and co-pilot that maintains the
continuous, accurate situation model they would otherwise maintain by hand —
freeing them for stakeholder work, negotiation, and strategic judgment.

**Design implications:**

1. **Expose the reasoning, not just the conclusion.** Trained PMs want to see
   the dependency chain, the slack math, the alternatives evaluated, and the
   confidence. The epistemic breakdown (known / believed / predicted / assumed /
   watching) and the auditable reasoning trail are *features* for this audience —
   they let the PM verify and challenge the AI's work.

2. **Present options, respect authority.** For a PM, "here are three viable
   options with tradeoffs; you decide" is respectful and correct. They have the
   judgment to choose. The decision-package format (recommendation + alternatives
   + tradeoff + confidence) is well suited to them.

3. **Let them steer the machinery.** Allow adjustment of thresholds, watch
   conditions, escalation sensitivity, and how aggressively the AI acts versus
   asks. A PM benefits from tuning the Executive to their style and risk
   tolerance.

4. **Speak the domain language.** Terms like slack, critical path, forecast
   error, and project debt are precise and welcome. No translation needed.

5. **Collaborate on correction.** When the PM corrects the AI's orientation, it
   should update state and reorient — and the correction can, over time, become
   candidate policy. The PM is a trusted teacher of the system.

**In short:** for trained PMs, show the work, offer the choices, expose the
controls, and use the vocabulary. The AI amplifies expertise the user already
has.

---

## B. For Users Who Are *Not* Trained Project Managers — the Executive as the Project Manager

**Who they are.** Engineers, founders, functional leads, operators, and small-
team owners who are responsible for a project but have no formal PM training.
They do not think in critical paths or slack; they think in "is this on track
and what do I need to do?" They often start from an **unstructured mess** — no
clear objectives, informal tasks, undocumented decisions, implicit dependencies.

**What the AI is to them.** Not an assistant that helps them do PM work — **the
project-management competence itself.** For this audience the AI *is* the project
manager. This is the larger market and the sharper unmet need: they cannot do
this work well, and today they either wing it, learn painfully, or hire someone.

**Design implications — these are different from Part A, not merely simpler:**

0. **Lead with foresight — this is the competence they lack most.** Of every
   gap a non-PM has, *anticipation* is the widest: they are worst at seeing
   problems coming. A reactive tool tells them "this just broke." A proactive
   Executive tells them "this is *about to* break — here is how to prevent it,"
   or "this milestone is at risk two weeks out, and here is what we should start
   now." The proactive, forward-looking behavior described in Sections 5–7 is not
   a general nicety for this audience; it is the single most valuable thing the
   product does for them, because it supplies the foresight they cannot supply
   themselves. Present the future, not just the present.

1. **Hide the PM machinery; surface plain meaning.** The user should never have
   to understand "orientation," "slack," or a "decision package." Internally the
   system does all of it; externally it says, in plain language: *"The vendor is
   running late. If they don't deliver by Friday, your launch is at risk. Here's
   what I'd do."* The sophistication stays inside; the surface is ordinary
   language and consequences, not PM constructs.

2. **Be prescriptive, not deliberative.** A trained PM wants options; a non-PM
   wants a recommendation. "Here are four options, you decide" is precisely what
   this user is bad at and does not want. Lead with **"Do this, because…"**, make
   saying *yes* a single click, and offer the alternatives only if they ask.
   Deliberation is a burden here, not a courtesy.

3. **Guide the decision, don't just request it.** The document rightly separates
   *authority* from *AI confidence* — but a non-PM often holds authority without
   the judgment to exercise it well. When a decision is theirs, the AI must not
   only ask; it must **help them decide**: what it recommends, why, what happens
   if they don't, and what similar teams typically choose. The escalation must
   carry the reasoning *and* the guidance, in plain terms.

4. **Construct structure from the mess — this is the core value.** Non-PMs
   rarely arrive with a clean project graph. The highest-value capability for
   this audience is the AI **building the project structure for them**: inferring
   the plan, surfacing implicit dependencies, turning informal notes and chats
   into tracked commitments and decisions, and asking a few plain clarifying
   questions rather than demanding a structured input. For this user, "make sense
   of my chaotic project" is worth more than any single analysis.

5. **Build trust for people who can't audit the logic.** A non-PM cannot tell
   whether "integration usually takes 3.8 days" is right, or whether the AI's
   orientation is sound. So trust cannot depend on the user checking the
   reasoning. Instead: use **conservative defaults**, act reversibly, flag
   low-confidence conclusions plainly ("I'm not sure about this — worth a human
   look"), fail gracefully, and earn trust through visibly-correct outcomes over
   time rather than through auditability the user can't use.

6. **Protect them from their own gaps.** Non-PMs are the most likely to let
   project debt accumulate, keep doing work that no longer matters, or miss a
   quietly-broken assumption. The Executive should proactively surface these in
   plain language ("You're still building the export feature, but the customer
   who needed it dropped out — should we stop?") because the user won't catch it
   themselves.

7. **Onboarding is a first-class problem.** The system must get value from a
   messy, partial starting point and improve as it learns the project — not
   require the user to first become organized. The AI meets them where they are.

**In short:** for non-PMs, hide the machinery, lead with a plain recommendation,
guide the decision, build the structure they lack, and earn trust through
outcomes rather than audit trails. The AI does not amplify expertise the user
has — **it provides the expertise the user lacks.**

---

## C. One System, Two Surfaces — Summary

| Dimension | Trained PM | Non-PM |
|---|---|---|
| The AI is… | A force multiplier | The project manager |
| Reasoning | Exposed and challengeable | Hidden; plain consequences shown |
| Guidance style | Options + tradeoffs | A clear recommendation, one-click yes |
| Decisions | User adjudicates | AI guides the user to a good decision |
| Vocabulary | Full PM domain language | Ordinary language, no jargon |
| Starting point | A structured project | A messy, partial one the AI structures |
| Trust basis | Auditable reasoning | Conservative defaults + good outcomes |
| Highest value | Continuous accurate situation model | Making sense of chaos + supplying competence |

The internal Executive, situation model, OODA loop, Information Governor, and
learning system are **identical**. Only the presentation layer adapts. Building
the sophisticated core is necessary but not sufficient; **the non-PM surface is
where the larger market is won or lost**, and it is the surface most at risk of
being neglected by a team that naturally designs for the expert it understands.

---

## D. Core Design Principles

1. **The Executive is proactive first: it reasons forward from goals and
   anticipates what needs attention, rather than only reacting to events. The
   absence of change is not the absence of management.**
2. Events trigger and accelerate attention; they do not necessarily prescribe
   action, and they are not the only reason the Executive thinks.
3. State determines relevance; goals determine what constitutes work.
4. Orientation should precede action.
5. No-op, defer, watch, and stop are valid management decisions; proactivity
   governs attention and anticipation, not action volume.
6. Every significant action should create an expected future state, and every
   expectation becomes something actively watched toward.
7. Universal access should be paired with selective cognition.
8. Past experience should inform future judgment without automatically
   dominating it.
9. Human attention is a scarce project resource.
10. Human authority is distinct from AI confidence or capability.
11. Manage commitments, assumptions, expectations, and decisions as first-class
    objects.
12. Learning consolidates from context to memory to policy to model capability.
13. Model adaptation should be governed, evaluated, versioned, and reversible.
14. Every important conclusion should have an inspectable reasoning and evidence
    trail — surfaced to trained PMs, held in reserve for non-PMs.
15. The persistent entity is the evolving project situation model, not the
    individual prompt or agent invocation.
16. **The sophistication belongs inside the system; the surface should match the
    user's project-management expertise.** *(the two-audience principle)*
17. **For users who are not trained PMs, the product's job is to supply
    project-management competence — most of all foresight — not merely to assist
    it.** *(the non-PM principle)*

---

## E. Product Proposition

> **Traditional project-management software records and organizes project
> information. An AI Project Executive continuously interprets that information
> in relation to goals, expectations, dependencies, experience, and authority —
> then determines what deserves attention and what should happen next.**

For trained PMs, this is a force multiplier for expertise they already have. For
the far larger group who are **not** trained project managers, it is something
more consequential: **management competence made available to people who would
otherwise go without it.**

The transformation is therefore:

```text
PASSIVE SYSTEM OF RECORD
          |
          v
ACTIVE SITUATION MODEL
          |
          v
PERSISTENT EXECUTIVE OODA
          |
          v
AI-MEDIATED PROJECT MANAGEMENT
          |
          v
LEARNING PROJECT / PORTFOLIO OPERATING SYSTEM
```

The long-term opportunity is not simply to make existing project-management
software easier to query. It is to create software that **participates in
management itself** — surfacing as a co-pilot for the expert and as the manager
for the non-expert — while remaining governed by explicit information controls,
human authority, inspectable reasoning, and accumulated organizational
experience.

---

## F. Questions for Further Design

Original open questions (still relevant to both audiences):

- What is the minimum viable project-state ontology?
- Which project objects should be explicit versus inferred dynamically?
- How should significance and attention be scored?
- How should decision-relevance retrieval differ from conventional RAG?
- How should the Executive distinguish facts, assumptions, predictions, and
  preferences?
- What authority model should govern autonomous actions?
- How should cross-project Executive agents negotiate shared resources?
- How should human corrections become candidate policies without
  over-generalization?
- How should project episodes be selected and labeled for specialist SLM
  training?
- How should decision quality be distinguished from outcome quality?
- What metrics establish that the Executive improves outcomes rather than merely
  producing more activity?
- What level of explanation is necessary for different classes of decisions?
- How should privacy and access boundaries constrain an Executive that sees
  communication, documents, schedules, and financials?
- How should the Executive detect and prevent organizational bad habits from
  becoming learned policy or model behavior?

New questions raised by the two-audience framing:

- How does the system detect which kind of user it is serving — by role, by
  behavior, by explicit setting — and can a single project have both?
- How much prescriptiveness is right for a non-PM before it becomes
  over-automation that erodes their understanding or ownership?
- What are the plain-language equivalents of the core PM constructs (slack,
  critical path, dependency risk) that preserve meaning without jargon?
- For non-PMs, how does the AI build project structure from unstructured input
  without an onerous setup burden?
- What conservative defaults and reversibility guarantees are needed so a non-PM
  can trust the system without auditing its reasoning?
- How does the product move a user *along* the expertise spectrum over time —
  can it teach, so a non-PM gradually becomes more capable, if they wish?

---

## G. Appendix — Governance, Explainability, and Epistemic Transparency

*(These retain the substance of the original document's Sections 21–23 and apply
to both audiences, with the presentation caveats noted in Parts A and B.)*

**Model governance.** Model changes should be evidence-based, versioned,
evaluated against held-out episodes, tested for regressions, calibrated, run in
shadow mode where appropriate, auditable, and reversible. A relatively stable
Executive model combined with more adaptive specialist SLMs balances continuity
and learning.

**Explainability and auditability.** Every consequential recommendation should be
traceable to project state — the slip, the forecast move, the resource
unavailability, the resulting buffer, the alternatives evaluated, the confidence,
and the information used. A human should be able to challenge any node in the
reasoning chain; a correction updates state and causes reorientation. *For
trained PMs this trail is a primary interface; for non-PMs it is held in reserve,
surfaced only when they ask "why?"*

**Epistemic status.** The AI should expose distinctions between what it knows,
believes, predicts, assumes, recommends, and is watching. *For trained PMs these
distinctions are shown directly; for non-PMs they are translated into plain
confidence cues ("I'm fairly sure" / "I'm guessing — worth checking").* This
makes the Executive understandable, correctable, and trustworthy rather than a
persona presenting conclusions with uniform certainty.