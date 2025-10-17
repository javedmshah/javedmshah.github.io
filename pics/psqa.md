---
layout: frontpage
title: PSQA
---


<div class="navbar">
  <div class="navbar-inner">
      <ul class="nav">
          <li><a href="qlyapunov.html">prev</a></li>          
          <li><a href="{{ BASE_PATH }}/jshah-public.pdf">cv</a></li>
          <li><a href="https://github.com/javedmshah">github</a></li>
          <li><a href="https://linkedin.com/in/javedmaqboolshah">LinkedIn</a></li>
          <li><a href="emotion_agency.html">next</a></li>          
      </ul>
  </div>
</div>

#### Proposing a theory of policy-subversive algorithms to improve quantum anomaly detection

**Abstract**. &mdash; <br>
We develop a theory of policy-subversive quantum algorithms (PSQAs): circuits
that employ a policy-defined violation oracle to discover prohibited state–action pairs
while attempting to evade detection. Our contributions are threefold. (i) We formalize a provenance model that cryptographically binds an oracle to a policy grammar and enforces a Reflection API for state-reflection primitives. (ii) We design and analyze two policy-grade detectors. Detector D1 is a compile-/trace-level test that recognizes Grover-like discovery via structural alternation between the signed violation oracle and registered state-reflections; under the API constraints, we prove completeness (no false negatives on amplitude amplification/estimation) and give exponentially decaying false-positive bounds. Detector D∗2 is a quantum-native spectral test that uses short amplitude estimation on the composed iterate Q = R ∗ ψUV to
certify the presence of marked-set dynamics; we quantify its query complexity for distinguishing k = 0 versus k ≥ k ∗ min. (iii) We prove an impossibility result: without provenance and reflection constraints, any black-box detector distinguishing Grover-like discovery from non-amplifying behavior with constant bias requires Ω(√N/k) queries, i.e., as hard as unstructured search. We also give policy-subversive constructions (QSVT/LCU packing, fixed-point schedules, and variational camouflage) and discuss how D2 defeats them.
