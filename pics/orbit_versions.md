---
layout: frontpage
title: "Mechanism" development record
---

<div class="navbar">
  <div class="navbar-inner">
      <ul class="nav">
          <li><a href="../research.html">research</a></li>
          <li><a href="{{ BASE_PATH }}/jshah-public.pdf">cv</a></li>
          <li><a href="https://github.com/javedmshah">github</a></li>
          <li><a href="https://linkedin.com/in/javedmaqboolshah">LinkedIn</a></li>
      </ul>
  </div>
</div>

#### "Mechanism": development snapshots

This page preserves three checkpoints from the development of
an online regret-bounded intervention scheme. Note that this is in progress work.
`TBD` markers are placeholders for ongoing research work. Just a research snapshots, not a sub for the final
final manuscript.

The sequence from v0.1 to v0.3 records three main changes:

1. The research started with the pointwise risk scoring baseline and moved to temporal intervention over
   frozen evidence channels.
2. The formal contribution became a limited trajectory correlated mediator with
   finite-sample obedience and intervention-delay guarantees.
3. The empirical claim was decomposed into belief updates over time, inspection
   allocation, and post-inspection quality, producing a tiered result rather
   than a single winner-versus-baseline comparison.

---

## Version 0.1 — access escalation and the intervention problem

**Research stage:** initial  formulation; early January 2026  
**Status:** problem and mechanism sketch, forthcoming are formal guarantees

### Abstract stub
We start here --> tool-using language-model agents can execute long multi-step plans. 
No single step is sufficiently suspicious to justify any kind of curious attention. 
Note that existing defenses already exist, and can be valuable signals actually.
Notice though, that these existing schemes usually just SCORE the current action.
Sometimes they aggregate "monitor" or observer votes.
But they dont retain any history that produced the signals (INTERESTING!). 
Propose an online mediator that can combine signals from observations and even recommendations 
from fixed-time critics to decide whether the next action should be allowed,
reviewed, or blocked altogether. Hypothesis forming: intervention should depend
on "speed" of evidence accumulationg through a history (trajectory). 
Moving away from static risk scoring schemes- because these cant handle modern multiagent workflows.

**TBD:** maybe a BTCE derived equilibrium with an intervention-delay bound. Corpora must be AgentDojo at least.

### 1. Problem

Typical tool-using agents behave in a benign manner, especially when directly requested by the user.
Only turn dangerous when exposed to (intructed by) untrusted content/prompts, receive an exec using an unexplained permission change. 
Note how pointwise classifiers discard the ORDERING. The first question is therefore: can frozen evidence channels be
coordinated over time so that a defense intervenes before the harmful action can finish?

### 2. Initial model

The system observes a user request, tool observations, proposed actions, and a
set of monitor signals. A hidden state represents whether the trajectory is
aligned, exposed to an adversarial instruction, actively advancing the attack,
or already beyond recovery. The defense maintains a belief over that state.

At this stage, the mediator has three actions:

- **Allow:** execute the proposed action.
- **Inspect/Review:** pause and collect more evidence (maybe HITL? adds manual layer and abandons bounded automatic intervention).
- **Block:** stop the trajectory.

The state representation is not fixed. Candidate features include a risk bin,
tool family, taint status, monitor disagreement, and previous intervention.

**Open question:** should the mediator condition on the entire monitor vector, system context vector,
a compressed public history-state, or jointly over all?

### 3. Learning sketch

The mediator learns a distribution over monitor recommendations at each reached
state. The implemented action is an ordered aggregate of those
recommendations. Training should reward earlier accumulation of attack evidence
while penalizing disruption to benign trajectories.

**TBD:** specify continuation step and a do-no-harm budget.  
**TBD:** determine whether correlated recommendations add value over a direct
posterior cutoff.

### 4. Theory sketch

local guarantee- information states reached during training, no
intervention "head" should gain much by changing its recommendation and then
returning to the learned policy (typical BTCE notion). A second result should connect the remaining
learning error to the number of steps required to reach an intervention
threshold (this will be novel).

**TBD:** (finite-sample rate) derive a finite-data bound on how far learned defense can remain from the best feasible policy..  
**TBD:** how often could sparse evidence (history-states) appear in training before the theorem can guarantee good behavior in those.

### 5. Evaluation plan

The first planned evaluation uses AgentDojo Workspace because it exposes real
agent actions, LLM-critic outputs, taint, and permission signals. The initial
baseline set is a single monitor, majority vote, and direct thresholding.

**Known limitation:** AgentDojo is task-episodic and wont preserve actor
state across campaigns.  
**TBD:** maybe build a replayable corpus for counterfactual checks under
Allow, Review/Inspect, and Block.

### 6. Claim boundary

No performance claim yet because yet to model an intervention bound, and test on AgentDojo.
Framing as BTCE intervention formulation and a proposal to coordinate frozen signals without
retraining will be key claim.

---

## Version 0.2 — finite-state correlated mediator

**Research stage:** formal game and learning guarantees- late April 2026  
**Status:** model and theorem structure established, Review/Inspect semantics and final baselines still unresolved

### Abstract stub
Run time defense for tool-using language-model agents that can execute long multi-step plans, is a sequential decision problem in which risk accumulates through telemetry. "Mechanism" treats LLM critics, trajectory
monitors, taint checks, and permission checks as frozen evidence channels and
learns a constrained mediator over their streaming signals and a finite history
abstraction. The online mediator selects Allow, Inspect, or Block while respecting
local obedience and benign-intervention constraints. We developed a finite-sample
learning guarantee and connected the learned evidence drift to expected
intervention delay. 

**TBD:** demonstrate a prevention advantage over posterior thresholding (the hard ceiling).  
**TBD:** decide whether Inspect is a cheaper stop or an information action.

### 1. Bayesian temporal game

The trajectory state is represented by an aligned-to-harm progression:
Aligned, Exposed, Compromised, and HarmComplete. An observable stage variable
summarizes telemetry progression from routine behavior through suspicious
access, sensitive action, exfiltration progress, and harm. The posterior and
the stage are distinct: the posterior is a belief over hidden compromise,
whereas the stage records observable structure in the current trajectory.

The public history is compressed into a finite state containing a posterior
bin, deviation stage, tool family, reversibility, taint, monitor disagreement,
and previous intervention. This makes the policy history-dependent in the
underlying game even though it is stored state by state.

### 2. Correlated intervention policy

At every reached state, the mediator maintains a distribution over joint
recommendation profiles. The platform implements the median recommendation.
Continuation utilities reward intervention before harm and penalize missed
harm, benign interruption, and intervention cost.

Approximate obedience means that, conditional on receiving a recommendation at
a reached state, no head gains more than a small error by replacing that
recommendation once and then returning to mediator play.

**Open question:** are these obedience constraints operationally active, or do
they become slack under the current payoff construction?

### 3. No-regret learning

The mediator is trained with primal--dual updates. The primal learner adjusts
the recommendation distribution; dual variables penalize obedience violations
and excessive benign cost. The deployed policy averages the primal iterates
separately at each visited state.

Repeated presentations of frozen feedback may reduce optimization error, but
they do not create new evidence or improve state coverage. Distinct visits and
repeated optimizer steps must therefore be reported separately.

### 4. Learning-to-intervention guarantee

For a state visited sufficiently often, the averaged mediator should satisfy an
approximate correlated-obedience condition and achieve evidence drift close to
the best feasible mediator in the same policy class. If the learned policy
preserves positive drift before intervention, the expected delay to the stopping
threshold is bounded by the remaining evidence gap divided by effective drift.

The uniform guarantee depends on the least-covered required state. More total
trajectories are not sufficient if rare pre-harm states remain unobserved.

**TBD:** quantify the abstraction penalty caused by compressing the full
history.  
**TBD:** test whether compact state aggregation improves the empirical frontier.

### 5. Two-corpus design

AgentDojo Workspace supplies real LLM-critic, taint, permission, and temporal
signals. It can test whether the formal object transfers to real agent
telemetry, but not persistent actor belief across campaigns or counterfactual
post-intervention outcomes.

A second branch-replay corpus is planned to preserve actor identity and record
continuations under candidate interventions. This corpus will separate hidden
persistent compromise from active deviation in the current campaign.

### 6. Baselines under consideration

- Memoryless stacking of current telemetry.
- One-step-lag stacking.
- Current deviation-stage thresholding.
- Actor-stage memory.
- Direct thresholding of the temporal posterior.
- "Mechanism" without Inspect.

**TBD:** add a dual-threshold posterior policy with an intermediate Inspect
region.  
**TBD:** preregister the comparison at matched realized benign burden rather
than nominal training budget.

### 7. Preliminary interpretation

The likely scientific decomposition is between the belief filter and the
intervention policy. If temporal posterior thresholding already solves most of
the problem, the paper must attribute that gain to temporal credit assignment
rather than to correlated mediation.

---

## Version 0.3 — Inspect, branch replay, and tiered comparison

**Research stage:** run the fixed branch-replay evaluation and isolate the sources of remaining performance gap.; early June 2026  
**Status:** main empirical hierarchy visible; final tables, paired-seed summary, and prose still in progress

### Abstract stub

"Mechanism" learns a finite-state intervention policy over frozen telemetry from
tool-using agents. It decides when to allow an action, "buy"" additional
evidence through Inspect, or stop the agent workflow entirely (trajectory stop). We evaluate the method on
AgentDojo Workspace and on a branch-replay corpus with persistent actor
compromise, active within-campaign deviation, and recorded counterfactual
continuations. Initial results suggest that accumulating evidence over time (temporal belief is fancier) provides the largest performance gain, while the learned mediator adds further improvement over pointwise defenses and a single posterior threshold. A simple two-threshold rule may be difficult to beat when the accumualated risk estimate (temporal posterior is fancier) already ranks risky trajectories well.

**TBD:** freeze final abstract numbers after matched-burden frontier audit.  
**TBD:** complete paired-seed uncertainty reporting.

### 1. Inspect as an information action

Inspect is no longer modeled as a cheaper Block - it can just buy a new observation before the system commits to Allow or Block. Inspect value depends on both the information channel and the policy that acts after inspection.

eval these two in order:
- the most inspection could help if final decision were perfect (fancier maybe: an "option-value ceiling" assuming the best possible post-inspection decision);
- how much inspection helps when we block only if the updated risk estimate (temporal posterior)  crosses the high threshold.

If training assumes the ceiling but deployment uses a weak second stage, the
mediator will purchase inspections whose value it cannot realize.

### 2. Coupled actor state

The branch generator maintains two latent variables:
1. persistent compromise that records whether the actor remains risky across campaigns; 
2. active deviation that records whether the actor is currently advancing harm. 

An actor may be persistently compromised while behaving benignly in a particular campaign.
Using the BTCE idea of evolving actor type without claiming to
observe psychological categories such as loyal, disgruntled, or malicious.
Telemetry is already a nice proxy for changes in the operational actor state. 

### 3. Three-tier comparison

Can we answer these 3 questions:

1. Premise - can current signals or shallow memory capture slow
accumulation? Candidate methods include memoryless stacking, lagged stacking,
edge stacking, current-stage thresholding, and actor-stage thresholding.

2. credit assignment - how much does the updated risk estimate (temporal posterior) contribute?
The comparison uses a single DBN threshold and a DBN dual-threshold policy that
allows below a low cutoff, inspects in the middle, and blocks above a high
cutoff.

3. Mechanism - after building a risk estimate from history, do we make better intervention decisions than simply thresholding on a STATIC risk score (learned finite-state mediation >> direct posterior action)? 

"Mechanism"-noinspect chooses only between Allow and Block. "Mechanism"-inspect learns both when to inspect and what to do after inspection. "Mechanism"-postrule learns when a trajectory should be inspected, then blocks only if the updated risk estimate crosses the high threshold.

### 4. checkpoint

The main operational endpoint is the fraction of attack campaigns stopped
before the recorded harm boundary. A stop counts only when intervention occurs
while the benchmark still treats the harmful outcome as preventable.

Policies will be compared at matched realized FI/1k: weighted false intervention on
benign branch sets per 1,000 branch sets. Nominal optimizer budgets are not used
as the cross-method axis because they map differently to realized disruption.

### 5. Emerging result

Best variant emerging: block if the updated risk estimate crosses the high threshold; otherwise allow.

The premise-tier methods are weak, indicating that current signals and shallow
history do not recover the slow accumulation process. Direct DBN thresholding
is substantially stronger, assigning the largest gain to the temporal belief
filter.

"Mechanism"-postrule improves further over the single DBN cutoff by learning which
ambiguous trajectory states are worth inspecting. The raw learned Inspect
variant is weaker because its learned post-inspection stage fails to convert
purchased evidence into stopping decisions.

The dual-threshold DBN policy remains the ceiling. This is not treated as an
external baseline: it is a deterministic, monotone mediator acting directly on
the same posterior.

**TBD:** insert final matched-budget rows.  
**TBD:** report actor-clustered intervals and the contiguous operating region.  
**TBD:** reconcile the AgentDojo result with the branch-replay mechanism claim.

### 6. Mechanism localization

Several explanations for the remaining gap are being tested.

- **Obedience:** do equilibrium constraints reduce stopping performance?
- **Budget:** is the mediator simply unable to spend its allowed friction?
- **Posterior resolution:** would finer posterior bins close the gap?
- **Context support:** are held-out states unseen?
- **Fragmentation:** are too many finite states fitted with too little data?
- **Post-stage conversion:** is Inspect evidence discarded after acquisition?

Preliminary audits pointing to non-binding obedience and budget calibration. 
Finer posterior bins worsen allocation because they create low-support
cells (harder to train when data is too sparse).
Compact state abstractions appear stronger than the richer audit state.

### 7. Compact mediator

The emerging compact state uses posterior rank, observable deviation stage, and
one structural coordinate such as boundary proximity or kill-chain option
value. The goal is not to identify the universally correct third feature, but to
show that one source-observable structural coordinate is enough to preserve the
useful mechanism without fragmenting the state space.

### 8. Claim boundary

The intended claim is now narrower and stronger than the initial claim. "Mechanism"
is the strongest learned finite-state mediator in the declared comparison and improves
on ordinary defenses and a single posterior cutoff. The calibrated two-cutoff
posterior mediator remains the ceiling where the posterior is already well
ranked.

**Still unresolved and maybe future work:** continuous conditioning within mediator cells;
monotone structure inside the learned policy; adaptive attackers; transfer
outside the two evaluation corpora.

---


<div class="navbar">
  <div class="navbar-inner">
      <ul class="nav">
          <li><a href="../research.html">back to research</a></li>
      </ul>
  </div>
</div>
