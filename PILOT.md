# ANKA Stack — Pilot Package

## What This Is

A working implementation of the first AI-native epistemic coordination stack.
Four layers. Four repos. One command to prove all of them.

    docker compose up

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

Epistemic mesh -- two nodes, one mesh, no coordinator:

    Alice publishes: 3.2C per doubling of CO2
    Bob independently replicates and witnesses
    Score: 2 witnesses
    Cite as: anka:sha256:939c3c...
    9 events published, 9 witnessed
    Mesh converged. Exit code: 0

Live institution integrations -- real APIs, inside Docker containers:

    NIST        Planck constant = 6.62607015e-34 J Hz^-1   physics.nist.gov
    World Bank  US GDP = $28.75 trillion (2024)             api.worldbank.org
    Shopify     real orders, real refunds                   Admin API

The ANKA Interact Protocol (v1.0) defines how any institution exposes
its AI to the mesh. Any company implements POST /interact. ANKA handles
routing, sessions, and receipts.

## The Analogy

    ARPANET was the protocol. The killer app was the Web.
    The Web was the protocol. The killer app was Mosaic.
    LLMs are the technology. The killer app was ChatGPT.
    ANKA is the protocol. Dalil is the browser. Raqib is the agent.

## Repositories

    https://github.com/mauludsadiq/Anka     13,590 lines   152 files
    https://github.com/mauludsadiq/Bay2      2,825 lines    25 files
    https://github.com/mauludsadiq/Raqib     1,071 lines    10 files
    https://github.com/mauludsadiq/Dalil       688 lines     4 files

    Total: 18,174 lines of Fard across 191 files

## Language

Written in Fard -- a deterministic functional language designed for
verifiable AI-operated systems. Every computation is reproducible.
Every claim is content-addressed. Every operation is replayable.

## Next Milestone

First production deployment between two real institutions on separate machines,
with real operators, real claim spaces, and real stakes.
