# Persistent AI Executive Layer

OODA, Oversight, Information Governance, Human Attention, and Model Evolution

*Conversation synthesis for further review • September 10, 2026*

Purpose: capture and organize the concepts developed in the conversation into a coherent architecture. This is a synthesis rather than a verbatim transcript; it preserves the major arguments, distinctions, examples, and open design questions.

## 1. Core Thesis: From Event-Driven AI to State-Driven Executive Cognition

Most AI interactions are episodic: an event or human prompt initiates reasoning, the model or agent acts, and the episode ends. The proposed architecture adds a persistent Executive Layer that repeatedly assesses what changed, what was completed, what remains unresolved, what decisions are emerging, and what work is now justified.

Events do not have to specify the next prompt. Instead, events signal that it may be time to re-orient. Persistent state, goals, expectations, constraints, history, and authority determine what deserves attention.

### Conceptual flow:

```text
Events / state changes → Observe → Orient → construct attention/agenda → Decide → delegate / ask / watch / no-op → Act → evaluate outcome → update state → repeat
```

## 2. Executive Layer vs. Agents vs. Oversight

A useful separation emerged between goal-achieving machinery and goal-governing machinery.

| Layer | Primary Question | Role |
| --- | --- | --- |
| Executive | What should happen next? | Prioritize, frame, authorize, delegate, escalate, defer, watch. |
| Agent | How do I accomplish this objective? | Execute bounded work, often using its own ReAct/OODA loop. |
| Oversight | Did reality match intention? | Evaluate results, constraints, quality, consequences, and recurring failure. |

The Executive is forward-looking; Oversight closes the loop. Oversight's findings become new observations for the Executive.

## 3. OODA as the Executive Backbone

OODA (Observe, Orient, Decide, Act) is a strong conceptual backbone, provided it is treated as a persistent control loop over the work system rather than as a rigid four-step prompt template.

| OODA Stage | Executive Interpretation |
| --- | --- |
| Observe | What changed? What completed? What failed? What expected event did not occur? |
| Orient | What does this mean relative to goals, plans, assumptions, dependencies, resources, constraints, history, and authority? |
| Decide | What deserves attention now: act, delegate, ask, replan, watch, defer, ignore, stop, or escalate? |
| Act | Execute directly or instantiate a bounded subordinate agent; establish expectations for the result. |

The Orient stage is the center of gravity. A weak architecture reacts directly to events; a stronger one first updates its situation model and decides whether the event matters at all.

## 4. Expectations: Detecting When 'Nothing Happened'

The system should model expected future states, not just observed facts. This allows absence to become meaningful. For example, 'customer response expected by Thursday' becomes an actionable discrepancy when Thursday passes without a response.

A significant action should create an expectation: expected effect, expected response, expected time, and a rule for what happens if the expectation is violated. Act therefore plants the seeds for future Observe.

### OODA can therefore be extended conceptually to:

```text
Observe → Orient → Decide → Act → Expect → Observe
```

## 5. Attention and Agenda Construction

The Executive should maintain an attention surface rather than reason deeply over everything it knows. Items rise or fall based on combinations of importance, urgency, change, uncertainty, opportunity, consequence, and reversibility.

A cycle need not produce an action. Valid outputs include: no-op, delegated work, a human decision, a watch, a replan, an escalation, or termination of work that is no longer justified.

## 6. How Past OODA Cycles Inform Future Cycles

Each loop should produce two kinds of output: an operational result and learning about the world or the Executive's own judgment. Past cycles can improve future loops in several distinct ways.

**State learning:** Update what is believed to be true now, including newly discovered dependencies.

**Causal learning:** Learn recurring relationships: what tends to cause delays, failures, opportunities, or downstream effects.

**Policy learning:** Learn which interventions tend to work under which conditions.

**Calibration learning:** Compare predicted probabilities, durations, costs, or confidence with actual outcomes.

**Preference/objective learning:** Infer stable human or organizational tradeoffs from repeated decisions and overrides.

**Metacognitive learning:** Learn the Executive's and specialist agents' own strengths, blind spots, and systematic biases.

The architecture therefore contains an inner operational OODA loop and a slower outer learning loop. The outer loop reviews episodes, compares expectations with outcomes, detects recurring patterns, and updates assumptions, policies, confidence, preferences, and model-selection behavior.

## 7. Structured Decision Episodes as Executive Memory

Rather than retaining only conversational history, each meaningful OODA cycle can be stored as a structured decision episode.

```text
Episode fields: time; trigger/observation; prior state; orientation; assumptions; options; decision; rationale; action; expected outcome; actual outcome; human intervention; correction; confidence; lesson; and provenance.
```

This creates an experience corpus from which the Executive can retrieve structurally similar decision situations, not merely semantically similar text.

## 8. Information Governance: Inject, Reject, or Defer

A persistent Executive will know far more than should enter any one orientation. The central problem becomes not just memory, but information admission: what information is allowed to shape this cycle?

A fact may be true and still be harmful to inject if it is stale, weakly applicable, distracting, anchoring, or associated with an unrelated objective.

| Disposition | Meaning |
| --- | --- |
| Inject | Likely to materially change framing, ranking, risk, authority, or decision. |
| Reject from current cognition | Not relevant now; retain if it may matter later. |
| Hold / Defer | Potentially relevant but below its activation threshold. |
| Quarantine | Unreliable, contradicted, or insufficiently validated. |
| Retire / Supersede | Once valid but now obsolete; preserve provenance. |

Retrieval should therefore optimize for decision relevance rather than semantic similarity alone. Relevant dimensions include causal, resource, constraint, goal, historical, authority, temporal, and counterfactual relevance.

## 9. Activation Conditions and Latent Knowledge

Information can remain dormant until a condition makes it decision-relevant. For example, another project's claim on the same engineer need not enter an Alpha testing discussion until Alpha's forecast extends into the competing commitment.

Past loops can therefore leave behind conditional knowledge: not only 'what we learned,' but 'under what conditions should this lesson be allowed to influence us?'

This supports an Information Governor beneath the Executive: a first-class component that manages relevance, applicability, confidence, provenance, contradiction, scope, recency, activation conditions, and expiry.

## 10. Human in the Loop: Enter at Maximum Leverage

Human involvement should not mean approving every action. The Executive should request human cognition where it has higher expected value than continued autonomous work, while preserving human authority over consequential judgment.

| Stage | Human Contribution | Example |
| --- | --- | --- |
| Observe | Reality correction | The AI is missing a material fact or social signal. |
| Orient | Framing / values | The AI is optimizing the wrong objective. |
| Decide | Preference / tradeoff | Delay launch or reduce scope? |
| Act | Authority | Approve a consequential commitment. |
| Evaluate | Qualitative judgment | Is the result actually acceptable? |
| Learn | Policy confirmation | Should this repeated preference become a standing rule? |

Escalation should consider uncertainty, consequence, irreversibility, and authority. Confidence and authority are separate: a model can be highly confident about an action it is not authorized to take.

The Executive should also manage a human attention budget: consolidate issues, do preparatory reasoning, identify the exact type of contribution needed (information, preference, judgment, authority, decision, exception, correction), and interrupt only when justified.

## 11. Learning from Human Intervention

A human response should produce more than an immediate action. It may update orientation and create a learning candidate. The system should distinguish whether the human's instruction was situational, contextual, or general before promoting it into reusable policy.

Repeated human corrections can progressively expand the autonomy envelope, but some domains may remain permanently reserved to human authority.

## 12. Context vs. Memory vs. Policy vs. Model Weights

Introducing narrow-domain Small Language Models (SLMs) creates a deeper learning layer. The critical architectural question is where a learned item should live.

| Layer | Example | Lifetime | Changeability | Best Use |
| --- | --- | --- | --- | --- |
| Context | Supplier is 3 days late | One/few cycles | Very high | Situation-specific facts |
| Memory / knowledge | Supplier A often slips after holidays | Many cycles | High | Mutable world knowledge |
| Explicit policy | Check historical variance before accepting lead-time claims | Long | High / auditable | Rules and procedures |
| Model weights | Recognize sparse-data lead-time risk patterns | Long | Lower | Stable skills and reasoning capability |

A useful heuristic is: facts tend toward memory; explicit requirements tend toward policy; stable, generalizable reasoning skills may eventually belong in model weights.

## 13. Promotion Pipeline for Learning

Model adaptation should be the slowest and most evidence-demanding form of learning. Individual OODA episodes are noisy and should not directly alter weights.

```text
OODA episode → episodic memory → validated semantic knowledge → policy/skill candidate → curated training corpus → candidate SLM → held-out evaluation → shadow operation → promote or reject
```

The deeper the learning mechanism, the higher the evidence threshold. This provides stability and makes changes inspectable and reversible.

## 14. OODA Episodes as Training Data for Specialist SLMs

The architecture naturally produces unusually rich supervision: state, observations, relevant context, orientation, assumptions, options, decision, action, expected outcome, actual outcome, human corrections, and lessons.

Potential learning signals include outcome supervision, human correction, Executive correction, comparative intervention outcomes, calibration error, recurring blind spots, and specialist-agent performance.

Narrow SLMs make this tractable because adaptation can be localized. A scheduling SLM can learn scheduling biases without modifying a contract SLM or the stable Executive model.

## 15. Model Governance and Self-Improvement

The Executive can eventually run an OODA loop over its own cognitive components: observe a specialist's recurring error, orient around distribution shift or bias, decide whether adaptation is warranted, train a candidate, evaluate it, and promote only after evidence.

Candidate models should be evaluated against the incumbent on historical episodes, held-out cases, edge cases, calibration, regressions, and safety/authority constraints. Shadow mode allows a candidate to answer real work without controlling production decisions.

A relatively stable Executive LLM combined with more plastic domain SLMs is an attractive architecture: the Executive preserves continuity and governance while specialist models accumulate domain expertise.

## 16. Important Failure Modes

- Context explosion: dumping all memory into every cycle instead of governing admission.
- Anchoring from history: retrieving similar past failures and causing the system to assume the same cause.
- Compulsive action: treating every observation as requiring an intervention.
- Over-escalation: converting every uncertainty into a human question.
- Premature weight updates: training directly from isolated episodes or unvalidated human overrides.
- Outcome bias: assuming a successful outcome proves the prior decision was good.
- Preference/ground-truth confusion: treating human preference as objective truth, or vice versa.
- Organizational pathology crystallization: embedding repeated bad habits into policies or model weights.
- Authority leakage: allowing competence/confidence to be mistaken for authorization.

## 17. Consolidated Architecture

The conversation converged on a layered persistent-agent architecture:

```text
WORLD / EVENTS
    ↓
Perception & significance gate
    ↓
EXECUTIVE OODA
    ↔ Information Governor (context / memory / applicability)
    ↔ Human Attention Manager (judgment / authority / correction)
    ↓
Agents + domain SLMs
    ↓
Actions / outcomes / expectations
    ↓
OVERSIGHT
    ↓
State + episodic memory + semantic knowledge + explicit policy
    ↓
Outer learning / calibration / training pipeline
    ↓
Validated model or policy evolution
    ↺ future Executive OODA
```

## 18. Design Principles Emerging from the Discussion

- Events trigger attention; they do not necessarily prescribe action.
- State determines relevance; goals determine what constitutes work.
- Orientation should precede action.
- No-op, defer, watch, and stop are legitimate Executive decisions.
- Every significant action should establish an expected future state.
- Past experience should inform future judgment without automatically dominating it.
- Information admission is a governance problem, not just a retrieval problem.
- Human attention is a scarce resource to be allocated at points of maximum leverage.
- Human authority is distinct from model confidence or capability.
- Learning should consolidate progressively: context → memory → policy → model capability.
- Weight changes should be evidence-heavy, evaluated, versioned, and reversible.
- The persistent entity is not the prompt or agent invocation; it is the evolving governed model of state, experience, expectations, and policy.

## 19. Open Questions for Further Review

- What is the minimum state schema needed for a useful Executive without creating an unmanageable ontology?
- How should significance and attention scores be computed: rules, learned models, or both?
- How can decision-relevance retrieval be measured independently of semantic similarity?
- What should be the boundary between the Information Governor and the Executive's Orient function?
- How are contradictions, stale knowledge, and applicability conditions represented and resolved?
- How should the system determine that repeated human corrections represent a stable policy rather than local exceptions?
- What evidence threshold should be required before promoting knowledge into an SLM training corpus?
- How should decision quality be separated from outcome quality when generating training labels?
- How should specialist SLM competence and calibration affect delegation and oversight?
- Which authorities should be permanently human-reserved versus dynamically delegable?
- How should multiple Executive layers negotiate conflicting goals, resources, and policies?
- What audit trail is necessary to reconstruct why a future Executive decision was made and which past learning influenced it?

## 20. Compact Summary

The proposed system is a persistent Executive control architecture built around OODA. It observes state changes and unmet expectations, orients using selectively admitted context and accumulated experience, decides what deserves attention, delegates bounded work to agents and specialist SLMs, and evaluates outcomes through Oversight. Past cycles create structured episodes that feed memory, calibration, policy, and—only after validation—model adaptation. Human involvement is treated as a governed source of judgment and authority rather than a universal approval gate. The resulting architecture aims to evolve from prompt-driven assistance toward persistent, inspectable, learning executive cognition.
