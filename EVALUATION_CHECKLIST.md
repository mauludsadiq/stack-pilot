# EVALUATION CHECKLIST

Work through this checklist to verify the stack independently.
Each item tells you what to run and what to expect.

---

## Setup

- [ ] Clone all four repos into ~/Downloads/
        git clone https://github.com/mauludsadiq/Bay2
        git clone https://github.com/mauludsadiq/Anka
        git clone https://github.com/mauludsadiq/Dalil
        git clone https://github.com/mauludsadiq/Raqib

- [ ] Verify fardrun is installed
        fardrun --version

- [ ] Run the full stack demo
        cd ~/Downloads/Raqib
        bash stack_demo.sh

  Expected: 12 steps, all green checkmarks, "Stack demo complete."

---

## Layer 1: Bay2

- [ ] Start Bay2 independently
        cd ~/Downloads/Bay2
        mkdir -p out/bay2
        fardrun run --program bay2/src/server.fard --out out/bay2

- [ ] Verify health
        curl http://localhost:19000/health
  Expected: {"ok":true,"kind":"bay2_server","object_count":0,"op_count":0}

- [ ] Store an object
        curl -X POST http://localhost:19000/object \
          -H "Content-Type: application/json" \
          -d '{"kind":"test","payload":{"value":42},"author_id":"eval","timestamp_unix_secs":1000,"tags":["test"]}'
  Expected: {"ok":true,"digest":"sha256:...","stored":true}

- [ ] Retrieve the object by digest
        curl http://localhost:19000/object/sha256:DIGEST
  Expected: {"ok":true,"object":{"kind":"test",...}}

- [ ] Verify replay log
        curl http://localhost:19000/replay
  Expected: {"ok":true,"ops":[...],"count":1}

- [ ] Run Bay2 test suite (120 tests)
        cd ~/Downloads/Bay2
        fardrun test --program bay2/tests/test_object.fard
        fardrun test --program bay2/tests/test_stream.fard
        fardrun test --program bay2/tests/test_capability.fard
        fardrun test --program bay2/tests/test_pubsub.fard
        fardrun test --program bay2/tests/test_monotone_index.fard
        fardrun test --program bay2/tests/test_view.fard
        fardrun test --program bay2/tests/test_replication.fard
        fardrun test --program bay2/tests/test_policy.fard
        fardrun test --program bay2/tests/test_replay.fard
        fardrun test --program bay2/tests/test_metering.fard
        fardrun test --program bay2/tests/test_anka_bridge.fard

---

## Layer 2: ANKA

- [ ] Start ANKA node
        cd ~/Downloads/Anka
        mkdir -p out/node
        fardrun run --program anka/src/node_process.fard --out out/node

- [ ] Verify health
        curl http://localhost:18080/health
  Expected: {"ok":true,"node_id":"ed25519:...","claim_count":0,"witness_count":0}

- [ ] Publish a claim
        curl -X POST http://localhost:18080/publish \
          -H "Content-Type: application/json" \
          -d '{"claim_space":"research.result.claims","subject":"eval-test","predicate":"reported_finding","object":"test value","evidence_refs":[],"timestamp_unix_secs":1775720000}'
  Expected: {"ok":true,"digest_hex":"sha256:..."}

- [ ] Retrieve the claim by digest
        curl http://localhost:18080/claim/sha256:DIGEST
  Expected: {"ok":true,"envelope":{"claim":{...},"digest_hex":"sha256:...","issuer_signature_hex":"..."}}

- [ ] Verify the signature is valid
  The issuer_signature_hex should verify against the node's public key.
  The digest_hex should match sha256(canonical_json(claim)).

- [ ] Query with collapse
        curl http://localhost:18080/query/research.result.claims/eval-test
  Expected: {"ok":true,"single_winner":{"winner_value":"test value","winner_score":0}}

- [ ] Witness the claim
        curl -X POST http://localhost:18080/witness \
          -H "Content-Type: application/json" \
          -d '{"digest_hex":"sha256:DIGEST","witness_node_id":"eval-witness","validation_type":"structural","timestamp_unix_secs":1775721000}'
  Expected: {"ok":true}

- [ ] Verify witness count increased
        curl http://localhost:18080/query/research.result.claims/eval-test
  Expected: winner_score: 1

- [ ] Check audit trail
        curl http://localhost:18080/audit/trail/sha256:DIGEST
  Expected: published_count: 1, witness_count: 1, reconstructable: true

- [ ] Stop and restart node, verify claim still present
        # Stop: Ctrl+C
        # Restart: fardrun run --program anka/src/node_process.fard --out out/node
        curl http://localhost:18080/claim/sha256:DIGEST
  Expected: same claim returned

- [ ] Run ANKA test suite (301 tests)
        cd ~/Downloads/Anka
        fardrun test --program anka/tests/test_anka_layer1.fard
        # ... (run all test files in anka/tests/)

---

## Layer 3: Dalil

- [ ] Run Dalil test suite (16 tests, requires ANKA on :18080)
        cd ~/Downloads/Dalil
        fardrun test --program dalil/tests/test_dalil.fard
  Expected: 16 passed

- [ ] Verify browse
  browse() should return node_id, claim_spaces, peer_count, claim_count

- [ ] Verify read returns cite_as
  cite_as should be "anka:sha256:..." — permanent content-addressed reference

- [ ] Verify trail returns full epistemic history
  trail() should return issuer, published_at, witnesses, reconstructable

- [ ] Verify follow resolves evidence_refs
  Publish claim A, then publish claim B with evidence_refs: [A.digest_hex]
  follow(B.digest_hex) should resolve A's trail

---

## Layer 4: Raqib

- [ ] Run Raqib test suite (17 tests, requires ANKA on :18080)
        cd ~/Downloads/Raqib
        fardrun test --program raqib/tests/test_raqib.fard
  Expected: 17 passed

- [ ] Verify step changes memory
  The live test publishes a claim and runs one agent step.
  Memory should go from empty to witnessed: 1

- [ ] Run multi-agent demo
        fardrun run --program raqib/src/demo.fard --out out/demo
        cat out/demo/result.json
  Expected: Oxford and MIT agents both have published:1, witnessed:1, stances:1
  Mesh should show witness_count:1, replication confirmed

---

## Cross-Layer Verification

- [ ] Publish via Dalil, read back via ANKA
  compose() should produce a digest_hex
  GET /claim/{digest} on the ANKA node should return the same claim

- [ ] Witness via Raqib, verify via Dalil
  step() should record witness in memory
  read() should show increased score

- [ ] Store execution receipt in Bay2, verify independently
  POST /object to Bay2 with kind:"fard.execution.receipt"
  GET /object/{digest} should return the receipt

- [ ] Verify gossip convergence
  Publish to Oxford, fetch to MIT
  MIT claim_count should increase

- [ ] Verify competing claims coexist
  Publish two claims to same claim_space and subject from different nodes
  Query should return one winner with score, plural should show both

---

## What a Successful Evaluation Looks Like

All 454 tests pass across four repos.
bash stack_demo.sh completes 12 steps with all green checkmarks.
Claims are recoverable after node restart.
Witnesses are federated across nodes in the audit trail.
Competing claims coexist in interpretive spaces.
Cite_as addresses are stable and content-addressed.
Bay2 stores objects and maintains a causal replay log.
Raqib agents update memory from unseen to witnessed autonomously.
