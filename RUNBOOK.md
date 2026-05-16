# RUNBOOK — Deployment and Recovery

## Prerequisites

- macOS or Linux
- fardrun installed and on PATH
- curl, python3 available
- Ports 18080, 18081, 19000 available

## Quick Start

    git clone https://github.com/mauludsadiq/Raqib
    git clone https://github.com/mauludsadiq/Anka
    git clone https://github.com/mauludsadiq/Bay2
    git clone https://github.com/mauludsadiq/Dalil

    cd Raqib
    bash stack_demo.sh

Expected runtime: 30-45 seconds. Expected output: 12 verified steps.

## Manual Deployment

### 1. Start Bay2

    cd ~/Downloads/Bay2
    mkdir -p out/bay2
    fardrun run --program bay2/src/server.fard --out out/bay2

Verify: curl http://localhost:19000/health
Expected: {"ok":true,"kind":"bay2_server","object_count":0,"op_count":0}

### 2. Start ANKA Oxford Node

    cd ~/Downloads/Anka
    mkdir -p out/node
    fardrun run --program anka/src/node_process.fard --out out/node

Verify: curl http://localhost:18080/health
Expected: {"ok":true,"node_id":"ed25519:...","claim_count":0,"witness_count":0}

### 3. Start ANKA MIT Node

    cd ~/Downloads/Anka
    fardrun run --program anka/src/node_process_b.fard --out out/node

Verify: curl http://localhost:18081/health

### 4. Connect Nodes as Peers

    curl -X POST http://localhost:18080/peer \
      -H "Content-Type: application/json" \
      -d '{"address":"http://localhost:18081"}'

    curl -X POST http://localhost:18081/peer \
      -H "Content-Type: application/json" \
      -d '{"address":"http://localhost:18080"}'

### 5. Start View Node (optional)

    mkdir -p out/view
    fardrun run --program anka/src/view_process.fard --out out/view

Verify: curl http://localhost:18085/health

## Docker Deployment

    cd ~/Downloads/Raqib
    docker-compose up

Services start in dependency order: Bay2 first, then ANKA nodes.
Persistent volumes preserve state across restarts.
Health checks gate service startup.

## Publishing a Claim

    curl -X POST http://localhost:18080/publish \
      -H "Content-Type: application/json" \
      -d '{
        "claim_space": "research.result.claims",
        "subject": "my-finding",
        "predicate": "reported_finding",
        "object": "the finding value",
        "evidence_refs": [],
        "timestamp_unix_secs": 1775720000
      }'

Returns: {"ok":true,"digest_hex":"sha256:...","gossip":{...}}

## Querying a Claim

    curl http://localhost:18080/query/research.result.claims/my-finding

Returns the highest-scored claim with full provenance.

## Audit Trail

    curl http://localhost:18080/audit/trail/sha256:DIGEST

Returns: published_count, witness_count, trail events, reconstructable flag.

## Recovery

State is persisted to SQLite. After restart, all claims are recoverable:

    curl http://localhost:18080/claim/sha256:DIGEST

## Claim Spaces

Nine canonical claim spaces registered at origin:

    anka.invariant.crypto
    anka.invariant.compute
    anka.interpretive.econ
    anka.interpretive.science
    fard.execution.receipts
    dataset.provenance
    model.training.trace
    research.result.claims
    reproducibility.results

## Ports

    18080   ANKA Oxford node
    18081   ANKA MIT node
    18085   View node (materialized projections)
    18090   Origin node (canonical claim spaces)
    19000   Bay2 server

## Troubleshooting

Node hangs on startup: check port conflicts with lsof -ti:18080 | xargs kill -9
Publish fails: verify node is running with curl http://localhost:18080/health
Witness not recording: check /sync endpoint for witness_count
Bay2 not receiving: verify Bay2 is running on :19000 before starting ANKA
