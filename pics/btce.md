---
layout: frontpage
title: BTCE
---


<div class="navbar">
  <div class="navbar-inner">
      <ul class="nav">
          <li><a href="exploits.html">prev</a></li>
          <li><a href="{{ BASE_PATH }}/jshah-public.pdf">cv</a></li>
          <li><a href="https://github.com/javedmshah">github</a></li>
          <li><a href="https://linkedin.com/in/javedmaqboolshah">LinkedIn</a></li>
          <li><a href="hawkes_identifiability.html">next</a></li>
      </ul>
  </div>
</div>

#### Bayesian-Temporal Correlated Equilibrium for early insider-threat intervention

**Abstract**. &mdash; <br>
Insider-threat systems often reduce trust to a risk score, but real compromise
unfolds as a sequence of choices, beliefs, opportunities, and interventions along
a kill chain. This paper develops a Bayesian-Temporal Correlated Equilibrium
(BTCE) framework for early intervention in enterprise environments. The model
represents users through latent loyalty types and behavioral states evolving over
a kill-chain dynamic Bayesian network, while a committee of certifiers receives
temporally correlated recommendations about when to observe, escalate, or
intervene. We show that the resulting mechanism satisfies temporal obedience
under local one-shot deviations, escalates in bounded expected time when evidence
accumulates with positive drift, and remains reliable under Byzantine
contamination when fewer than half of certifiers are corrupted. Experiments on
CERT insider-threat data evaluate detection timing, false-alarm control, and
graceful degradation under compromised certifiers. The central claim is that
insider risk is not a single number; it is a time-indexed pattern of evidence,
incentives, and coordinated recommendations, and preserving that structure
enables earlier and more auditable defense.

**Core idea**. &mdash; <br>
A trustworthy defense should not merely ask whether a user has a high anomaly
score. It should ask how evidence is accumulating, which stage of the kill chain
the behavior belongs to, which certifiers agree or disagree, and whether an
intervention can be justified before irreversible harm occurs.

**Contributions**. &mdash; <br>
(i) A dynamic Bayesian game model for insider-threat detection that connects
telemetry, latent user state, and staged defensive actions. (ii) A
Bayesian-Temporal Correlated Equilibrium mechanism that coordinates heterogeneous
certifiers through time without assuming a perfectly trusted central judge. (iii)
Early-detection guarantees showing bounded-time escalation under positive
evidence drift. (iv) Byzantine-resilient committee aggregation that degrades
gracefully when some certifiers are compromised.

**Status**. &mdash; <br>
<<<<<<< Updated upstream
Accepted in the oral track at <a href="https://www.gamesec-conf.org/">GameSec 2026</a>. Presenting in Oct 2026.
=======
Accepted in the oral track at <li><a href="https://www.gamesec-conf.org/">GameSec 2026</a></li>
>>>>>>> Stashed changes

**Keywords**. &mdash; <br>
Bayesian games; correlated equilibrium; insider-threat detection; dynamic
Bayesian networks; early intervention; Byzantine robustness; enterprise security.
