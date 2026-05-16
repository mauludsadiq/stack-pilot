# ARCHITECTURE

## Overview

The ANKA stack is four layers. Each layer depends on the one below.
No layer knows about the layer above it.

    Bay2    <- operational substrate
    ANKA    <- epistemic coordination protocol
    Dalil   <- AI-native browser / navigation layer
    Raqib   <- autonomous agent runtime

---

## Bay2 — Operational Substrate

Bay2 provides the operational primitives that everything else runs on.

    object.fard           Digest-addressed immutable storage
    stream.fard           Causal append-only event log
    capability.fard       Scoped bearer tokens with attenuation
    pubsub.fard           Pattern-matched subscriptions
    monotone_index.fard   Append-only indexes (kind/author/time/tag)
    view.fard             Materialized projections over streams
    replication.fard      Signed receipts, durability reporting
    policy.fard           Allow/deny rules, namespace-scoped
    replay.fard           Operation log, checkpoint replay
    metering.fard         Compute and storage costs per operation
    anka_bridge.fard      ANKA-Bay2 translation layer

Key property: everything in Bay2 is digest-addressed, signed, replayable,
causal, monotone, and verifiable. Nothing is implicit. Nothing is mutable.

Bay2 HTTP server: port 19000
Endpoints: POST /object, GET /object/{digest}, GET /objects,
           GET /replay, POST /meter/credit, POST /meter/charge,
           POST /pubsub/subscribe, GET /summary

---

## ANKA — Epistemic Coordination Protocol

ANKA is the protocol for AI-to-AI coordination of claims about the world.

Core primitives:

    claim.fard              Signed, content-addressed claim envelopes
    witness.fard            Structural and semantic witnessing
    weighted_collapse.fard  Reputation-weighted claim collapse
    archive.fard            Federated audit trail
    capability_store.fard   Scoped publish/witness/challenge access
    view_node.fard          Cross-node materialized views
    bay2_store.fard         In-process Bay2 adapter
    bay2_http_store.fard    Networked Bay2 HTTP adapter

Claim spaces:

    Invariant (single-winner):   anka.invariant.crypto, anka.invariant.compute,
                                 dataset.provenance, reproducibility.results
    Interpretive (plural):       anka.interpretive.econ, anka.interpretive.science,
                                 research.result.claims, model.training.trace

Node API (port 18080/18081):

    POST /publish              Publish a claim to a claim space
    GET  /claim/{digest}       Fetch a specific claim by digest
    GET  /query/{space}/{subj} Query with policy collapse
    POST /witness              Record a witness attestation
    POST /challenge            Record a challenge
    POST /fetch                Fetch and witness from a peer
    POST /peer                 Register a peer node
    GET  /peers                List known peers
    GET  /sync                 Node state summary
    GET  /graph/claim/{digest} Full claim graph (witnesses, challenges)
    GET  /audit/trail/{digest} Federated audit trail
    GET  /known                All known claim digests
    POST /capability           Register a capability token
    GET  /capabilities         Capability store status
    GET  /health               Node health

---

## Dalil — AI-Native Browser

Dalil is to ANKA what Mosaic was to HTTP. It makes the mesh navigable.

    dalil.browse(node_address)
      Navigate to a node. See claim spaces, peer count, claim inventory.

    dalil.explore(node_address, claim_space)
      Browse a claim space. See subjects, counts, scores.

    dalil.read(node_address, claim_space, subject)
      Read a finding with full epistemic context.

    dalil.trail(node_address, digest)
      Pull full epistemic history: who published, witnessed, challenged.

    dalil.follow(node_address, digest)
      Follow citation chain. Resolve evidence_refs to source claims.

    dalil.compose(node_address, claim_space, subject, finding, refs, ts)
      Publish a new claim with evidence.

    dalil.subscribe(node_address, claim_spaces, subscriber_id)
      Declare interest in claim spaces.

    dalil.feed(node_address, claim_spaces, since_timestamp)
      Pull new claims since a timestamp.

Dalil is stateless. Every call is a fresh traversal. The mesh is the state.

---

## Raqib — Autonomous Agent Runtime

Raqib provides the execution loop that turns Dalil into a persistent agent.

    raqib.make_identity(name, institution, node_address)
    raqib.empty_memory()
    raqib.update_stance(memory, stance)
    raqib.get_stance(memory, claim_space, subject)
    raqib.default_deliberate(claim, memory, config)
    raqib.observe(dalil, identity, memory, claim_spaces, since_ts)
    raqib.act(dalil, identity, memory, deliberation, timestamp)
    raqib.step(dalil, identity, memory, config, since_ts, timestamp)
    raqib.publish(dalil, identity, memory, claim_space, subject, finding, refs, ts)

The agent loop:

    observe -> deliberate -> act -> update memory -> repeat

The deliberation function is a slot. Replace default_deliberate with any
reasoning system: an LLM call, a logic engine, a trained classifier.

---

## Data Flow

    Agent calls dalil.compose()
      -> POST /publish to ANKA node
      -> ANKA creates signed claim envelope
      -> ANKA records to SQLite (persistent)
      -> ANKA shadow-writes to Bay2 object store
      -> ANKA records operation in Bay2 replay log
      -> ANKA broadcasts gossip to peers
      -> Peer nodes receive digest announcement
      -> Peer nodes fetch and verify claim
      -> Peer nodes witness and record

    Agent calls dalil.read()
      -> GET /query/{space}/{subject} to ANKA node
      -> ANKA applies weighted collapse over local claims
      -> Returns highest-scored claim with provenance
      -> Agent receives: finding, score, cite_as, witnesses

---

## Identity and Keys

Every ANKA node has a stable Ed25519 keypair generated from a seed.
The node_id is the hex-encoded public key prefixed with "ed25519:".
All claims, witnesses, challenges, and capabilities are signed.
No operation is accepted without a valid signature.

---

## Persistence

ANKA nodes persist state to SQLite. After restart, all claims, witnesses,
challenges, peers, subscriptions, and the Bay2 store are fully restored.
State is keyed by node_id, which is deterministic from the seed.

---

## Repositories

    Bay2    https://github.com/mauludsadiq/Bay2
    ANKA    https://github.com/mauludsadiq/Anka
    Dalil   https://github.com/mauludsadiq/Dalil
    Raqib   https://github.com/mauludsadiq/Raqib
