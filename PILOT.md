# ANKA Stack — Pilot Package

## What This Is

A working implementation of the first AI-native epistemic coordination stack.
Four layers. Four repos. One command to prove all of them.

    bash stack_demo.sh

## The Problem It Solves

AI systems today have no shared epistemic substrate. When one model produces a
finding, there is no protocol for another model to verify it, witness it,
challenge it, or build on it with provenance intact. Every AI system operates
in epistemic isolation.

ANKA is the protocol that changes this. It gives AI systems a shared,
verifiable, tamper-evident layer for coordinating claims about the world.

## The Stack

    Bay2    operational substrate     object storage, streams, replay, metering
    ANKA    epistemic coordination    claims, witnesses, collapse, audit
    Dalil   AI-native browser         browse, read, trail, follow, compose
    Raqib   autonomous agent runtime  identity, memory, observe, deliberate, act

## What It Demonstrates

Two institutional AI agents — Oxford and MIT — operating on one epistemic mesh:

- Oxford publishes a climate sensitivity finding
- MIT independently publishes a competing finding
- Both claims survive — interpretive space, no central arbiter
- The mesh converges via signed gossip — no coordinator
- An autonomous Raqib agent observes the Oxford claim and witnesses it
- A computation result is written directly to Bay2 as an executable claim
- Policy collapse returns the highest-scored claim with full provenance
- The Oxford node is stopped and restarted — both claims remain recoverable
- Every event is in the audit trail — permanent, verifiable, content-addressed

## The Analogy

    ARPANET was the protocol. The killer app was the Web.
    The Web was the protocol. The killer app was Mosaic.
    LLMs are the technology. The killer app was ChatGPT.
    ANKA is the protocol. Dalil is the browser. Raqib is the agent.

## Repositories

    https://github.com/mauludsadiq/Bay2    120 tests  1,316 lines
    https://github.com/mauludsadiq/Anka    301 tests  5,324 lines
    https://github.com/mauludsadiq/Dalil    16 tests
    https://github.com/mauludsadiq/Raqib    17 tests + stack demo

## Language

Written in Fard — a deterministic functional language designed for
verifiable AI-operated systems. Every computation is reproducible.
Every claim is content-addressed. Every operation is replayable.

## Next Milestone

First production deployment between two real institutions on separate machines,
with real operators, real claim spaces, and real stakes.
