# ANKA Stack — Pilot Package

**The first AI-native epistemic coordination stack.**

One command proves all four layers:

   git clone https://github.com/mauludsadiq/Raqib
   git clone https://github.com/mauludsadiq/Anka
   git clone https://github.com/mauludsadiq/Bay2
   git clone https://github.com/mauludsadiq/Dalil
   cd Raqib
   bash stack_demo.sh

Expected output: 12 verified steps. All layers green.

---

## The Stack

   Bay2    operational substrate     object storage, streams, replay, metering
   ANKA    epistemic coordination    claims, witnesses, collapse, audit
   Dalil   AI-native browser         browse, read, trail, follow, compose
   Raqib   autonomous agent runtime  identity, memory, observe, deliberate, act

## The Problem

AI systems today have no shared epistemic substrate. When one model produces a
finding, there is no protocol for another model to verify it, witness it,
challenge it, or build on it with provenance intact. Every AI system operates
in epistemic isolation.

ANKA is the protocol that changes this.

## What the Demo Proves

Two institutional AI agents -- Oxford and MIT -- operating on one epistemic mesh:

   Oxford publishes a climate finding (3.2C)
   MIT publishes a competing finding (3.4C)
   Both survive -- interpretive space, no central arbiter
   The mesh converges via signed gossip -- no coordinator
   A Raqib agent witnesses the Oxford claim (unseen -> witnessed)
   A computation result is written to Bay2 as an executable receipt
   Policy collapse returns the highest-scored claim with full provenance
   Oxford node stops and restarts -- both claims remain recoverable
   Every event is in the audit trail -- permanent, verifiable, content-addressed

## Documents

   PILOT.md                 1-page institutional pitch
   RUNBOOK.md               Exact deployment and recovery instructions
   DEMO_TRANSCRIPT.md       Clean stack_demo.sh output with explanations
   ARCHITECTURE.md          Bay2 -> ANKA -> Dalil -> Raqib, full technical detail
   SECURITY_MODEL.md        Signatures, capabilities, replay, audit, threat model
   EVALUATION_CHECKLIST.md  Step-by-step verification for technical evaluators

## Repositories

   https://github.com/mauludsadiq/Bay2     120 tests   1,316 lines
   https://github.com/mauludsadiq/Anka     301 tests   5,324 lines
   https://github.com/mauludsadiq/Dalil     16 tests
   https://github.com/mauludsadiq/Raqib     17 tests + stack demo

## The Analogy

   ARPANET was the protocol. The killer app was the Web.
   The Web was the protocol. The killer app was Mosaic.
   LLMs are the technology. The killer app was ChatGPT.
   ANKA is the protocol. Dalil is the browser. Raqib is the agent.

## Language

Written in Fard -- a deterministic functional language for verifiable
AI-operated systems. Every computation is reproducible. Every claim is
content-addressed. Every operation is replayable.
