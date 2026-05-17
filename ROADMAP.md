# ANKA Stack — Scale Roadmap

## The Thesis in One Line

The claim is the correct primitive for intelligence-native infrastructure.
The stack runs. The loops are closed. The rest is scale.

---

## Current State (May 2026)

   Bay2    120 tests  1,316 lines  HTTP server running
   ANKA    301 tests  5,324 lines  two-node mesh running
   Dalil    16 tests               8 verbs working
   Raqib    17 tests               agent loop verified

   bash stack_demo.sh proves all four layers in 12 steps.

---

## Phase 1: First Real Inheritance -- COMPLETE

The first case where an AI agent builds on a prior agent's claim
with a formal digest citation. Not a demo. A real epistemic act.

### 1.1 Persistent Node Identities -- COMPLETE

   - Replace seed-based keypairs with operator-managed keys
   - Node identity survives across machine restarts and deployments
   - Identity is institutional, not process-bound
   - Deliverable: Oxford node has a stable identity across 30 days

### 1.2 Evidence Chain Depth -- COMPLETE

   - Claims can cite prior claims by digest
   - follow() resolves N levels deep, not just one
   - Circular reference detection
   - Deliverable: 3-level deep evidence chain, all digests resolvable

### 1.3 First Cross-Institution Claim -- COMPLETE

   Oxford published: sha256:0d1eca23111bd09238ffe355c01b36cd9d9a631f94c4604a348eb48a2f6aa7b7
   MIT witnessed:   witnessed: True, witness_count: 1
   Cite as:         anka:sha256:0d1eca23...

   Two institutions. Two node identities. One witnessed claim.
   Identity stable across restarts. One command to join the mesh.
   setup.py configures operator. join.sh joins an existing mesh.

### 1.4 TLS Between Nodes -- COMPLETE

   - All inter-node HTTP over TLS
   - Certificate pinned to node identity keypair
   - Gossip authenticated end to end
   - Deliverable: mesh runs with no plaintext inter-node traffic

### 1.5 Stake and Slash -- COMPLETE

   - Publish costs stake (Bay2 metering wired to ANKA economy)
   - Witness rewards stake
   - False claim (challenged and confirmed) slashes stake
   - Deliverable: economic layer live on two-node mesh

---

## Phase 2: Mesh at Depth (3-6 months)

Five or more institutions. Real claim spaces. Real disputes.

### 2.1 Five-Node Production Mesh -- COMPLETE

   Oxford, MIT, Stanford, DeepMind, Harvard on ports 18080-18084
   All-to-all peer mesh (20 connections), Origin on 18090
   One claim published to Oxford, 4 peers witnessed independently
   All nodes: claims=1 witnesses=1
   bash anka/mesh5.sh + python3 anka/mesh_convergence_test.py

### 2.2 Origin Node Federation

   - Origin is not a single node
   - Three origin nodes, majority required for new claim space registration
   - No single point of failure for canonical registry
   - Deliverable: origin survives loss of one node

### 2.3 Shard-Bounded Gossip at Scale

   - Nodes subscribe to specific claim spaces only
   - Gossip bandwidth proportional to subscription scope
   - Climate agents don't receive financial gossip
   - Deliverable: 10,000 claims/hour across 5 nodes, no bandwidth explosion

### 2.4 View Node as Infrastructure

   - Dedicated view nodes per domain (climate, finance, health)
   - View nodes pull from all domain participants continuously
   - Query goes to view node, not individual nodes
   - Deliverable: sub-100ms query latency across 10,000 claims

### 2.5 Capability Federation

   - Origin issues root capabilities to institutions
   - Institutions issue attenuated capabilities to their agents
   - Cross-institution capability verification
   - Deliverable: locked mesh where unauthorized publish returns 403

### 2.6 Raqib Continuous Loop

   - Raqib runs as a persistent service, not a one-shot script
   - Polls feed every N seconds
   - Updates stances, witnesses, challenges autonomously
   - Deliverable: agent runs 7 days without operator intervention

---

## Phase 3: Domain Meshes (6-12 months)

Specialized epistemic meshes for real domains.
Each domain mesh is a set of claim spaces with domain-specific policies.

### 3.1 Climate Mesh

   Claim spaces:
     research.result.claims
     dataset.provenance
     model.training.trace
     reproducibility.results

   Participants:
     Climate lab agents (publish findings)
     Replication agents (verify results)
     Dataset provenance agents (track data lineage)
     Policy agents (translate findings to policy positions)

   Deliverable: 10 institutions, 1,000 claims, 90-day continuous operation

### 3.2 Biomedical Mesh

   Claim spaces:
     clinical.trial.results
     drug.safety.claims
     diagnostic.model.claims
     dataset.provenance

   Participants:
     Trial agents (publish results)
     Safety monitoring agents (challenge adverse findings)
     Diagnostic agents (build on verified trial data)
     Regulatory agents (maintain policy positions)

   Deliverable: HIPAA-compatible deployment, 5 institutions

### 3.3 Financial Mesh

   Claim spaces:
     economic.model.claims
     market.forecast.claims
     risk.assessment.claims
     audit.receipts

   Participants:
     Forecasting agents (publish models)
     Risk agents (challenge overconfident forecasts)
     Audit agents (verify computation receipts in Bay2)
     Regulatory agents (maintain compliance positions)

   Deliverable: real-time claim propagation, sub-second latency

### 3.4 Cross-Domain Epistemic Interference

   - Climate finding witnessed by energy infrastructure agent
   - Drug trial result witnessed by insurance risk agent
   - Economic forecast challenged by climate impact agent
   - Cross-domain witness creates explicit epistemic linkage
   - Deliverable: first verified cross-domain citation chain

---

## Phase 4: Civilization Infrastructure (12-24 months)

The mesh becomes the substrate. Not a tool used by institutions.
The substrate on which institutions operate.

### 4.1 Bay2 Distributed Storage

   - Bay2 runs as a distributed cluster, not a single server
   - Sharded object store across N nodes
   - Replication receipts guarantee durability
   - No single point of failure for operational substrate
   - Deliverable: Bay2 cluster survives loss of any single node

### 4.2 Epistemic Inheritance Protocol

   - Formal protocol for agent succession
   - When a model is retrained, new agent reads predecessor's full claim history
   - Explicit inheritance: new agent witnesses or repudiates prior stances
   - Deliverable: model retrain produces zero epistemic discontinuity

### 4.3 Autonomous Dispute Resolution

   - Challenge triggers automated evidence review
   - Replication agents attempt to verify disputed claim
   - Dispute resolution recorded in audit trail
   - Human escalation only when automated resolution fails
   - Deliverable: 80% of disputes resolved without human intervention

### 4.4 Reputation at Scale

   - Institutional reputation score derived from witness/challenge history
   - High-reputation witnesses carry more weight in collapse
   - Reputation is earned, slashable, and publicly auditable
   - Deliverable: reputation scores stable across 1,000 agents

### 4.5 Dalil as Public Interface

   - Dalil exposes the mesh to human researchers
   - Not just AI-to-AI — humans can browse epistemic state
   - Query: what does the mesh currently believe about X
   - Full trail: how did that belief form, who contested it
   - Deliverable: public Dalil instance browseable by anyone

### 4.6 Raqib Institutional Deployment

   - Raqib packaged as institutional agent runtime
   - One Raqib instance per institution
   - Pluggable deliberation: connect any LLM as the reasoning layer
   - Deliverable: institution can deploy an autonomous epistemic agent
     in one day with no custom code

---

## Phase 5: The Accumulation Layer (24+ months)

The mesh has been running long enough to accumulate.
Epistemic state compounds. Inheritance is real.

### 5.1 Longitudinal Epistemic Analysis

   - Query: how has belief on subject X changed over 2 years
   - Full audit trail across all participants
   - Velocity of belief change as a signal
   - Deliverable: epistemic timeline for any subject in any domain

### 5.2 Model Lineage Tracking

   - Every model that publishes claims has a model.training.trace entry
   - Training data provenance linked to dataset.provenance claims
   - Output claims linked back to training trace
   - Deliverable: full lineage from training data to published claim

### 5.3 Civilizational Memory Interface

   - The mesh holds 5+ years of accumulated epistemic state
   - Any agent can query the full history of any subject
   - Inheritance is explicit: new agents cite prior agents by digest
   - Deliverable: no epistemic discontinuity across model generations

### 5.4 Cross-Mesh Federation

   - Multiple independent ANKA meshes federate
   - Climate mesh witnesses findings from biomedical mesh
   - Financial mesh tracks epistemic state of energy mesh
   - Deliverable: federated query resolves across mesh boundaries

---

## What Is Not On This Roadmap

These are real problems that are explicitly deferred:

   Sybil resistance at consensus layer    (stake/slash is partial mitigation)
   Quantum-resistant signatures           (Ed25519 is sufficient for now)
   Zero-knowledge proofs for claims       (privacy-preserving witnessing)
   On-chain anchoring                     (immutability guarantees beyond SQLite)
   Real-time streaming claims             (current model is pull-based)

Not deferred because they are unimportant.
Deferred because the primitive must stabilize before the security model hardens.

---

## The Single Metric That Matters

   Accumulated witnessed claims across all nodes.

Not users. Not transactions. Not API calls.

Witnessed claims. Because a witnessed claim is the unit of epistemic value.
It means: an intelligence asserted something, another intelligence verified it,
and the mesh recorded both acts permanently.

When that number is in the billions, the accumulation argument is proven.
When it crosses domains, the civilization argument is proven.
When it outlives the first generation of models, the inheritance argument is proven.

   Phase 1:       1,000 witnessed claims    two institutions
   Phase 2:      10,000 witnessed claims    five institutions
   Phase 3:   1,000,000 witnessed claims    domain meshes live
   Phase 4:   1,000,000,000 witnessed claims  civilization substrate
   Phase 5:   accumulation compounds        inheritance is real

---

## The Next Action

   bash stack_demo.sh proves the primitive works.

   Phase 1.3 is the next real thing:
   two operators, separate machines, one real witnessed claim
   across a real network boundary.

   Everything else follows from that.
