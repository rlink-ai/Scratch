# AI Project Executive
## A State-Driven, OODA-Based Architecture for Project Management

**Concept document for further review**
**Revised:** November 4, 2026

---

## Summary in Plain Language

**The problem.** Most project tools only record what people type in: tasks,
dates, owners. Working out what it all *means* and what to do next is left to a
person. Many people running projects aren't trained project managers, so that
work often doesn't get done.

**The idea.** An AI that acts like an experienced project manager on the team.
Instead of waiting to be asked, it keeps track of the project and works out what
needs attention.

**How it thinks.** It starts with one question: *what does it take to finish this
project, and what's still missing?*

1. **Agree on what "done" means.** The AI suggests a short list of outcomes, such
   as "customers can use the new feature in production". It draws on the
   project's goals, what was said in meetings, and what similar projects usually
   need. The owner confirms or adjusts the list. It isn't fixed and gets updated
   when plans change.
2. **Find the gaps.** For each outcome, it checks what's needed and whether that
   exists yet: work nobody has planned, decisions nobody has made, questions
   nobody has asked, tasks with no owner, approvals nobody has scheduled. A risk
   is just an outcome that might not happen.
3. **Focus on what matters now.** Early on almost everything is a gap, so it
   ranks them by urgency and saves the rest for later instead of listing
   everything.
4. **Check what's still true.** It also watches for things the project is
   counting on that have stopped being true, like a vendor running late or a
   person being reassigned.

**How it stays ahead without being noisy.** Deadlines, expectations and
assumptions all have dates attached. The AI rechecks them on a schedule, so it
notices problems coming even when nothing has happened yet. Most checks are
simple and cheap; the AI only does deeper thinking when something actually
looks off. It speaks up when it matters and stays quiet otherwise.

**How it stays trustworthy.**
- It keeps a clear record of what it believes and why. It only changes its mind
  when there's new evidence, and it says what changed.
- If the team says "on track" and the AI disagrees, it shows the disagreement
  and the evidence rather than quietly overriding anyone.
- It never changes project records on its own. It *proposes* changes ("add these
  six items to the plan"), the person reviews and approves them, and the system
  makes the change in a way that can be undone. It starts with only adding new
  items and earns more freedom over time.

**How people use it.** Mostly through a planning conversation. You chat with the
AI, and a panel beside the chat shows the draft list of outcomes and plan items
as they take shape. You can edit the list directly or just talk.

**Who it's for.**
- **Experienced project managers:** it does the constant tracking and shows its
  reasoning so they can check it.
- **Everyone else:** it supplies the project-management know-how they don't
  have, in plain language, with clear recommendations instead of lists of
  options.

**How you'd know it's working.** It notices changes quickly, and gaps get closed
*before* they hold the project up.

**What's set aside for later.** Coordinating across many projects, specialised
AI models, and having the AI retrain itself.

> **In one line:** the AI Project Executive keeps asking "what will it take to
> finish, and what's missing?", and helps you close those gaps before they
> become problems.

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

Sections 1–18 describe the shared architecture; longer-range extensions are
collected under **Future Directions**. **Sections A and B** then describe how the
product should behave differently for each audience.

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

- What does finishing require that we don't yet have?
- What changed?
- What was completed?
- What was expected but did not happen?
- What do those changes mean relative to goals and plans?
- What is now at risk or newly possible?
- What work should happen next?
- What should be stopped or deferred?
- What decisions require human judgment or authority?
- What should simply be watched?

The first question is the anchor. The Executive's orientation is measured as
**distance to done, expressed as gaps** (§6a–§6b): what completing the project
requires, and what is still missing. Guarding against risk is one case of that
question, not its core.

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

The Project Executive operates using an ongoing OODA model.

OODA is often described as a competitive loop — out-cycling an adversary — but
its core, in Boyd's own framing, is **re-orientation**: keeping one's
understanding matched to a changing environment. No adversary is required. A
project drifting from its plan, a scope that shifts, a dependency that quietly
goes stale — these are exactly the changing environment OODA is built for. The
measure of the loop is therefore not raw speed but **how quickly the Executive's
understanding catches up with reality** (see Candidate Metrics, §F).

The loop is entered from two directions: when the world changes, and when the
Executive's own forward view — its completion conditions, gaps, and expectations
— says something needs attention even though nothing has "happened." Section 6
explains why these are really one mechanism.

```text
   PROJECT STATE / WORLD              COMPLETION CONDITIONS, GAPS,
   (something changed)                EXPECTATIONS (re-checked on schedule)
             |                                      |
             +------------------+-------------------+
                                |
                                v
                             OBSERVE  <---------------------------------+
                  (changes AND anticipated futures)                     |
                                |                                       |
                                v                                       |
                             ORIENT                                     |
           (1. what does finishing require that is missing?             |
            2. what are we counting on that is no longer true?)         |
                                |                                       |
                                v                                       |
                             DECIDE                                     |
                                |                                       |
      +----------+----------+---+------+-----------+                    |
      |          |          |          |           |                    |
      v          v          v          v           v                    |
     ACT       WATCH      HUMAN     INITIATE   INVESTIGATE              |
             (expect-    DECISION   (close a   (obtain                  |
              ation)                 gap)      missing info)            |
      |          |          |          |           |                    |
      +----------+----------+----+-----+-----------+                    |
                                 |                                      |
                                 v                                      |
                  PROJECT STATE + NEW EXPECTATIONS                      |
                                 |                                      |
                                 +---- outcomes observed (feedback) ----+

   Routine cases take a shortcut:  ORIENT --(learned policy)--> ACT
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
Orientation asks two questions, in order:

1. **What does finishing require, and what is missing?** Measured against the
   project's completion conditions (§6a), orientation identifies gaps — missing
   work, decisions, information, owners, inputs, approvals (§6b). This is the
   primary question, and it drives the Executive's agenda.
2. **What are we counting on that is no longer true?** Observations are checked
   against current beliefs, expectations, and completion conditions; a mismatch
   is a signal to re-orient (§7a).

Both are interpreted relative to the current plan, dependencies, assumptions,
constraints, resources, commitments, historical experience, organizational
policy, and human authority. Guarding against risk is part of the first
question, not a separate one: a risk is a completion condition that might not
be met.

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

### Two features carried over from Boyd

- **Implicit guidance — Orient straight to Act.** A well-oriented actor handles
  routine situations directly, without full deliberation. Here, situations that
  match learned policy (§18 — Context → Memory → Policy) go straight to action,
  and the full Decide step is reserved for novel or consequential cases. This is
  also how the loop stays affordable.
- **Feedback.** The outcomes of Decide and Act are themselves observations. The
  Executive learns whether its own interventions worked, not only whether the
  project did.

---

## 6. Proactivity as One Mechanism: Future-Dated Objects, Re-checked

A purely event-driven system is fundamentally **reactive** — something must
happen in the world before the Executive thinks. A real project executive does
not wait to be poked. It **looks ahead**, **goes looking for problems before
they surface**, **initiates work and inquiry on its own authority**, and
**anticipates what should happen next**. Foresight — not reaction — is the
defining behavior of management.

It is tempting to describe this as two separate drives: a proactive, goal-driven
one and a reactive, event-driven one. In practice they are **one mechanism**.
Proactivity does not need a separate "think ahead" engine; it comes from *what
the Executive stores*:

- **completion conditions** (§6a) and the **gaps** against them (§6b);
- **expectations** — what should happen, by when, including watches (§7);
- **assumptions** with a re-validation date;
- **milestones, dependencies, and resource windows** with dates attached.

Every one of these is a **future-dated object**. Re-checking them on a schedule
is what "reasoning forward" means in practice: an expectation nearing its date,
an assumption reaching its re-check date, a gap that will soon block a
condition, a milestone whose upstream work is not positioned. None requires an
external event — each surfaces because the object itself says *now is the time
to look*.

**Events** — task completed, email received, document changed, meeting
concluded, decision recorded, an expected event that did *not* occur, or a
periodic heartbeat — remain valuable. But an event does **not** prescribe an
action, and the absence of events does **not** imply the absence of management.
An event simply **accelerates** a re-check the schedule would have reached
anyway.

> **The Executive maintains future-dated completion conditions, gaps, and
> expectations, and re-checks them continuously. Events accelerate that
> re-checking; they are not the only reason the Executive thinks.**

### Triage before reasoning

Continuous LLM reasoning over every project is neither affordable nor necessary.
Most cycles should be **deterministic**: date arithmetic, threshold tests,
expectation status, gap-ranking rules. The model is called for orientation only
when one of those checks produces a signal that needs interpretation. Cheap
checks decide *where* to think; the model decides *what it means*.

**Proactive does not mean constantly acting.** No-op, defer, watch, and stop are
valid decisions; do not interrupt humans needlessly. Proactivity governs
*attention and anticipation*, not *action volume*. Constant foresight, selective
action.

This is what separates an *Executive* from an *automation*. An automation waits
for a trigger and fires a rule. An Executive maintains a forward view of what
the project needs in order to finish, and acts on its own reading of it — using
events to sharpen, not to summon, its attention.

---

## 6a. Completion Conditions — Defining "Done"

The Executive's orientation starts from an explicit definition of **done**: a
small set of **completion conditions**. Each is phrased as a *checkable outcome*,
not a task — "customers can request instant payouts in production," not "build
payouts" — and each states *how we would know it is true*.

**Elicitation: suggest first, ask where needed.** People react to a list far more
easily than they produce one. The Executive therefore *suggests* conditions,
each showing its source:

- the project's objectives, scope, and success criteria;
- what was said in meetings and documents ("the customer needs a demo," "Legal
  must sign off");
- general knowledge of what this kind of project usually requires (a launch
  usually needs testing, training, and a rollback plan).

It then *asks* a few sharpening questions — only where nothing can be inferred,
or where the project-specific answer matters most ("Who has to approve this
before it's done?"). To avoid rubber-stamping, suggestions are kept few and
specific to this project; for the most consequential ones, the Executive asks a
sharpening question rather than offering a plain "accept."

**Progressive breakdown.** Top-level conditions are set up front. Each one is
broken down only when it becomes relevant — it is approaching in time, or
someone asks — using the same suggest-and-ask pattern at each level ("What does
'training complete' mean here?"). The Executive goes only as deep as the next
decision or the next piece of work someone could start.

**A living definition.** Completion conditions are beliefs, not fixed
requirements. Signals of scope change — a dropped requirement, a new stakeholder,
a passed milestone — prompt the Executive to revisit what done includes. A change
in "done" is itself a signal: it retires work that served a removed condition
(§16) and triggers fresh gap analysis.

---

## 6b. Gap Analysis — Orientation as Distance to Done

For each completion condition, the Executive works out what it requires and
compares that with what exists. Whatever is required but absent is a **gap**:

- **Missing work** — a requirement with no task behind it.
- **Missing decision** — work blocked on a choice nobody has made.
- **Missing information** — a needed estimate, spec, or answer nobody has asked
  for.
- **Missing owner** — work or a decision nobody is accountable for.
- **Missing input** — a dependency nobody has planned to supply.
- **Missing approval** — an authority step nobody has scheduled.
- **Missing criteria** — something marked done with no definition of done.

**A risk is a completion condition that might not be met.** Guarding against
risk is therefore part of gap analysis, not a separate discipline.

**Missing work versus missing data.** "I don't see a test plan" may mean testing
has not been planned — or that it has been and was never recorded. The Executive
resolves this by *asking in plain language* ("Is testing planned somewhere?").
The answer either fills in the graph or confirms a real gap.

**Ranking.** Early in a project nearly everything is a gap; showing all of them
is just a to-do list nobody reads. Gaps are ranked by how soon they block a
condition, how much depends on them, and whether anyone could act on them today.
"Nobody has planned cutover" does not matter in week 1 but is urgent in week 10.
A gap that does not matter yet is watched — it becomes an expectation (§7) —
rather than surfaced.

**Dismissed gaps.** An owner may say a gap is not needed. The dismissal is
recorded with a date to raise it again, not forgotten. This respects the owner's
authority while still protecting non-PMs from their own blind spots.

**The second question: mismatch.** Once "what's missing?" is answered,
orientation asks "is anything we're counting on no longer true?" — whether
observations contradict current beliefs, expectations, or completion conditions
(§7a).

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

**Watch and Expect are the same object.** A "watch" is simply an expectation with
a trigger: *vendor delivers by Friday; if not, reopen the vendor decision.* Every
Decide outcome other than "act now" — watch, defer, ask a human, investigate —
leaves an expectation behind for a later cycle to check. This keeps the
Executive's entire forward view in one kind of object.

---

## 7a. Explicit, Stable Orientation

The situation model is made concrete as a set of **beliefs** — "launch is
achievable," "the vendor is reliable," "Susan is available through the 22nd" —
each with a confidence level, its evidence, and a last-checked date. Completion
conditions (§6a) are beliefs too. Re-orientation means changing beliefs, with the
change recorded.

**Stability.** An Executive that re-orients continuously with a language model
can flip-flop — the same state judged "at risk" on Tuesday and "fine" on
Wednesday with nothing changed. For a user that is worse than silence. Beliefs
therefore change only on new evidence, and every change carries a reason: *"I was
confident in the Oct 15 date; I'm less so because the vendor spec slipped."* That
record of changes is also the most natural explanation to show a non-PM — more
useful than a reasoning trail.

**Team orientation as a signal.** People hold their own beliefs about the
project. When the team's view ("on track") and the Executive's beliefs disagree,
the Executive shows the disagreement and its evidence rather than silently
overriding it: *"The team's last update says on track; here's why I'm less
sure."* The gap between orientations is often the most valuable signal there is.

**Breaking down and rebuilding.** Boyd's "destruction and creation": periodically,
and at milestones, the Executive deliberately questions the goal and the
definition of done — is this still the right outcome, is this work still worth
doing — rather than only tracking against them.

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

In the completion-oriented framing (§6a–§6b), most new work comes from **closing
gaps**: a condition that needs work nobody has planned, a decision nobody has
made, information nobody has asked for. The Executive does not write that work
into the project directly. It proposes it (§10a), usually through the planning
conversation (§10b).

---

## 10a. Writing Back — Proposals, Not Writes

The Executive never writes project records directly. It produces **typed
proposals** drawn from a small, fixed set of actions; deterministic code checks
each proposal, and the system's ordinary write path applies it.

- **Additive first.** The initial set is create-only: milestones, action items
  (with owner and due date), pending decisions, and links between items and
  milestones or completion conditions. Changes to existing records come later,
  behind a before-and-after preview. Deletes come last, if at all.
- **Batch confirmation.** Planning proposals collect in a draft and are confirmed
  as a set — *"Add these 6 items to the plan"* — because plan items make sense
  together. Per-item approval remains for one-offs.
- **Checked on approval, not on generation.** IDs, access, field values, and
  *staleness* — has the underlying state changed since the proposal was made? —
  are checked when the user approves. Stale proposals are regenerated, not
  applied.
- **Provenance and undo.** Every write records the approving person and the
  proposal it came from, so a batch can be listed and reversed.
- **Links to "done."** Every created item is linked to the completion condition
  it serves. These requirement-to-work links are exactly the graph structure
  §14a notes is missing from today's data. **Building the plan builds the
  graph.**
- **Guardrails.** Check proposals against existing items for duplicates; limit
  how many items a single proposal can contain; prefer the next actionable layer
  over a full breakdown; and use real accounts for owners where possible, so
  "who owns this" is not guesswork.
- **A trust ladder.** Write capability widens with track record: additive with
  batch approval first, then updates with preview, and only much later any
  autonomous writes, for proven kinds of action.

There are two kinds of write, with different levels of caution. **Graph writes**
— links, confidence, confirmations — record the system's own beliefs; a wrong one
skews later reasoning but changes nobody's records, so these can be lighter-touch.
**Project-record writes** — action items, dates, owners, decisions — belong to
people and always require approval.

One remaining risk: a one-click "yes" from a non-PM can become rubber-stamping.
A typed preview keeps the change visible, but for consequential changes it may be
worth slowing that click down on purpose.

---

## 10b. The Planning Conversation — Interaction Model

Defining done and building the plan happen in a **dedicated chat persona** within
the product, separate from the question-and-answer personas. It is a guided
conversation with a goal and a structured result.

- **A conversation plus a live draft.** The chat is the dialogue. A panel beside
  it shows the draft completion conditions and proposed plan items, updated
  through the model's tool calls — never by parsing its prose. The user can edit
  the panel directly or by talking. Without the panel, users end up typing data
  entry into a chat box.
- **A structured flow, carried by the prompt:** gather context, suggest, ask one
  or two sharpening questions per turn, confirm. Never a form.
- **A prompt variant per audience.** The non-PM variant leads with suggestions in
  plain language; the PM variant allows direct authoring and challenge in PM
  terms. Same tools, same draft, different prompt (Sections A and B).
- **A persistent session** per project for this persona, so revisiting "done"
  picks up what was agreed and why.
- **System-started re-entry.** When signals suggest scope has changed, the
  product invites the user back into this conversation with context already
  loaded — *"A meeting last week dropped the export requirement; want to revisit
  what done includes?"* — keeping the user in control while still being
  proactive.

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

### Top-down derivation: the goal implies structure

Inference from ambient communication works *bottom-up*, from records toward
structure. It has a natural complement that works *top-down*: start from the
project's completion conditions (§6a), derive the structure they *require* — the
work, decisions, inputs, owners, and approvals each condition depends on — and
check that expected structure against what the records show. Where they match,
the graph gains a confirmed edge; where something is required but absent, the
result is a gap (§6b); where the records are simply silent, the Executive asks.

This makes **planning and graph construction the same activity.** Each time the
planning conversation (§10b) proposes work for a condition and a person accepts
it, a requirement-to-work edge is created (§10a) — precisely the structure this
section notes is missing from today's data. The planning conversation is
therefore a primary surface for building the graph, alongside inference from
meetings, email, and documents.

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

Completion conditions (§6a) make this concrete. Work created through the
planning conversation is linked to the condition it serves (§10a); when a
condition is removed or changed, every item linked to it becomes a candidate for
stopping or re-scoping — a lookup, not an investigation.

---

## 17. Learning Across Projects

Every significant OODA cycle can become a structured decision episode
(observation, prior state, orientation, assumptions, options, decision, action,
expected outcome, actual outcome, human correction, lesson). Across many
projects the organization learns patterns — which vendors are optimistic, which
work is underestimated, which mitigations work under which conditions. This
becomes **organizational experience**, not generic PM knowledge.

---

## 18. Context, Memory, Policy, and Model Evolution

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
become candidates for model adaptation. Learned policy is also what powers the
loop's fast path from Orient straight to Act (§5). The deepest layer — adapting
model weights — is a longer-range direction (see Future Directions).
(Governance, explainability, and epistemic transparency — the original Sections
21–23 — are retained in Appendix G and continue to apply to both audiences.)

---

## Future Directions

These extensions follow naturally from the core architecture but are not needed
to prove it. They are set aside here to keep the core — completion conditions,
gaps, expectations, beliefs, and re-orientation — in focus.

### Nested Project and Portfolio Executives

The OODA model can be hierarchical: a Portfolio Executive orienting across
multiple Project Executives. If Project A needs Sarah for another week and
Project B depends on her for a critical milestone, neither Project Executive
resolves the conflict alone — the Portfolio Executive orients across both and
either allocates under delegated authority or prepares the decision for a human
portfolio owner. This provides natural escalation across organizational levels.

### Specialist Small Language Models

The Executive can orchestrate narrow-domain SLMs — Schedule, Risk, Resource,
Requirements, Financial, and Stakeholder — rather than relying on one model for
every cognitive task. The Executive combines their outputs and maintains
authority over the overall orientation.

### Model Adaptation

The final step of the learning hierarchy (§18) — turning stable, generalizable
skills into model capability — requires the governance described in Appendix G:
evidence-based, versioned, evaluated, and reversible change. It should follow,
not precede, a working Context → Memory → Policy loop.

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

1. **The Executive is oriented toward completion. It continuously maintains
   what "done" requires, identifies what is missing, and works to close those
   gaps. Guarding against risk is one case of this, not its core. The absence of
   change is not the absence of management.**
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
18. **Done is a living, confirmed set of checkable outcomes** — suggested by the
    system, confirmed by people, and revised as scope changes.
19. **The model proposes; code writes.** All write-back is typed, validated,
    previewed, attributable, and reversible.
20. **Orientation is explicit and stable.** Beliefs carry confidence, evidence,
    and a check date; they change only on new evidence, and every change records
    why.

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

- Is the core ontology — completion conditions, gaps, expectations, and beliefs
  — sufficient, and what else must be explicit rather than inferred?
- How should significance and attention be scored beyond gap ranking (§6b)?
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
  producing more activity? (See Candidate Metrics below.)
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

New questions raised by the completion-oriented framing:

- How much general project-type knowledge should shape suggested completion
  conditions before it becomes confidently wrong for a specific project?
- What is the right cadence and trigger for revisiting "done"?
- How should dismissed gaps be weighted for non-PM owners compared with trained
  PMs?
- What is the minimum write vocabulary that makes the planning conversation
  useful?

### Candidate Metrics

- **Time to re-orient** — how long between a change in reality and the
  Executive's beliefs reflecting it. This measures what OODA is actually for.
- **Gaps closed before they blocked** — the share of gaps closed before they held
  up a completion condition, compared with gaps discovered only after.

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
