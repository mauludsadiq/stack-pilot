# ANKA Stack — Pilot Package

**The first AI-native epistemic coordination stack.**

One command. Full stack. ~60 seconds.

    git clone https://github.com/mauludsadiq/Anka
    cd Anka
    bash demo.sh

Full suite (all four demos):

    bash demo-full.sh

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

    Step 2: State Farm  Claim approved.
                        Base cost $2,200 (2020 USD) x 1.1507 inflation factor
                        = $2,531.51 payout (net $2,031.51 after deductible).
                        Inflation: 2.95% US CPI, World Bank 2024 (live).
                        Adjuster Sarah Chen assigned, contact within 24 hours.

    Step 3: City Auto   Repair booked Thursday May 21 at 10:00 AM. Estimate $2,350.
                        Insurance billed directly. Loaner car available.

    Audit:  Every action signed, content-addressed, and permanently recorded
            in the ANKA mesh with full provenance and lineage.

From chaos to resolution — in one natural conversation, across three separate
institutions, with complete auditability.

No form-filling. No contradictory bots. No lost paperwork.
Just a capable AI acting as your verified institutional agent.

The accident demo is now hybrid — mock institutions, live economic data.
The payout is calculated using real US CPI from the World Bank API at runtime.

Run it:

    python3 anka/demos/accident_flow.py          # hybrid: mock + live CPI
    python3 anka/demos/accident_flow_dynamic.py  # dynamic: agents discovered from mesh
    python3 anka/demos/accident_followup.py       # multi-turn: mesh is the memory

The dynamic demo adds Option B — agent discovery.
The follow-up demo adds multi-turn continuity:

    Turn 1: "I was in a car accident" -> 3 institutions coordinated
    Turn 2: "What is the status of my claim?" -> answered from mesh
    Turn 3: "Can I move the repair to Friday?" -> rescheduled, recorded

    The user returned the next day.
    Different session. Same mesh. Full continuity.
    The mesh is the memory.

The dynamic demo adds Option B — agent discovery:
    Agents register capabilities as signed claims in the ANKA mesh.
    Dalil /discover/{capability} returns the highest-scored agent.
    Any agent can register. The mesh routes to the best one.

## The Functional Demo: Research Publication Verification

100% real. No mocks. Every API call is live.

User says:

    "I'm publishing a paper on climate sensitivity.
     Help me verify my key claims and find related work."

What ANKA does — four real institutions, one session:

    arXiv:      26 preprints on climate sensitivity     export.arxiv.org
    PubMed:     24,665 peer-reviewed papers             pubmed.ncbi.nlm.nih.gov
    NIST:       Stefan-Boltzmann = 5.67e-8 W m^-2 K^-4 physics.nist.gov (CODATA 2022)
    World Bank: Global GDP = $110.98 trillion (2024)    api.worldbank.org

Every data point is live. Every claim is signed.
Every citation is content-addressed and reproducible.

    arXiv search    anka:sha256:059ec13a...
    PubMed search   anka:sha256:3cd58665...
    NIST constants  anka:sha256:43c3c497...
    World Bank data anka:sha256:e4a6e4d9...

Run it:

    python3 anka/demos/research_verification_flow.py
    python3 anka/demos/clinical_trial_flow.py

The clinical trial demo generates an FDA-auditable epistemic trail:

    Trial ID: TRIAL-MRNA-*

    1. PubMed     444 papers on mRNA vaccine efficacy       anka:sha256:99e906...
    2. arXiv      312 preprints on protein folding          anka:sha256:08847b...
    3. NIST       Boltzmann + Avogadro constants (CODATA 2022) anka:sha256:c47957...
    4. World Bank life expectancy 73.48yr, population 8.14B   anka:sha256:64209d...

    Every dosage decision traceable to source paper or constant.
    Cannot be altered. Verifiable by any node. Queryable by any auditor.

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
    https://github.com/mauludsadiq/Dalil       798 lines     4 files

    Total: 18,284 lines of Fard across 191 files

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
