# ANKA Stack — Pilot Package

**The first AI-native epistemic coordination stack.**

One command runs the full stack:

    docker compose up

Or run natively:

    git clone https://github.com/mauludsadiq/Anka
    git clone https://github.com/mauludsadiq/Bay2
    git clone https://github.com/mauludsadiq/Dalil
    git clone https://github.com/mauludsadiq/Raqib
    cd Raqib
    bash stack_demo.sh

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

## The Killer Demo: AI as Your Institutional Agent

User says naturally:

    "I was in a minor car accident yesterday. The other driver ran a red light.
     I need help filing the insurance claim, getting my car repaired,
     and submitting the police report."

What ANKA does:

    Step 1: City PD     Police report filed. Officer Rodriguez assigned.
                        Incident documented at Main St & 5th Ave.

    Step 2: State Farm  Claim approved. Payout $2,847 (net $2,347 after deductible).
                        Adjuster Sarah Chen assigned, contact within 24 hours.

    Step 3: City Auto   Repair booked Thursday May 21 at 10:00 AM. Estimate $2,350.
                        Insurance billed directly. Loaner car available.

    Audit:  Every action signed, content-addressed, and permanently recorded
            in the ANKA mesh with full provenance and lineage.

From chaos to resolution — in one natural conversation, across three separate
institutions, with complete auditability.

No form-filling. No contradictory bots. No lost paperwork.
Just a capable AI acting as your verified institutional agent.

Run it:

    python3 anka/demos/accident_flow.py

## What the Technical Demo Proves

Two institutional AI agents -- Alice and Bob -- operating on one epistemic mesh:

    Alice publishes a climate finding (3.2C per doubling of CO2)
    Bob independently replicates it
    Bob witnesses Alice's claim -- score goes from 0 to 2
    The mesh converges via signed gossip -- no coordinator
    Every event is in the audit trail -- permanent, verifiable, content-addressed
    Exit code: 0

Five live external institution integrations, running inside Docker containers,
calling real APIs over the public internet:

    NIST        Planck constant = 6.62607015e-34 J Hz^-1   physics.nist.gov (CODATA 2022)
    World Bank  US GDP = $28.75 trillion (2024)             api.worldbank.org
    Shopify     real orders and refunds                     anka-test-store.myshopify.com
    PubMed      4,061 papers on mRNA vaccine efficacy       pubmed.ncbi.nlm.nih.gov
    arXiv       17,992 preprints on large language models   export.arxiv.org

## Docker

    docker compose up

Services: origin, alice, bob, adapter (Python), demo.
The demo container runs the full epistemic mesh proof followed by live
institution integrations. All containers on the same private network.
No credentials required for NIST or World Bank.

## Repositories

    https://github.com/mauludsadiq/Anka     13,590 lines   152 files
    https://github.com/mauludsadiq/Bay2      2,825 lines    25 files
    https://github.com/mauludsadiq/Raqib     1,071 lines    10 files
    https://github.com/mauludsadiq/Dalil       688 lines     4 files

    Total: 18,174 lines of Fard across 191 files

## The Analogy

    ARPANET was the protocol. The killer app was the Web.
    The Web was the protocol. The killer app was Mosaic.
    LLMs are the technology. The killer app was ChatGPT.
    ANKA is the protocol. Dalil is the browser. Raqib is the agent.

## Language

Written in Fard -- a deterministic functional language for verifiable
AI-operated systems. Every computation is reproducible. Every claim is
content-addressed. Every operation is replayable.

## Documents

    PILOT.md                 1-page institutional pitch
    ARCHITECTURE.md          Bay2 -> ANKA -> Dalil -> Raqib, full technical detail
    RUNBOOK.md               Exact deployment and recovery instructions
    DEMO_TRANSCRIPT.md       Clean stack_demo.sh output with explanations
    SECURITY_MODEL.md        Signatures, capabilities, replay, audit, threat model
    EVALUATION_CHECKLIST.md  Step-by-step verification for technical evaluators

# License

MUI
