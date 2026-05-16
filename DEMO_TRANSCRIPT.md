# DEMO TRANSCRIPT

Full output of bash stack_demo.sh against a clean environment.
Recorded: May 2026. Fard runtime. macOS.

---

    $ bash stack_demo.sh

    ── 1. Starting Bay2
      ✓ Bay2 running on :19000

    ── 2. Starting ANKA (Oxford :18080, MIT :18081)
      ✓ Oxford node running on :18080
      ✓ MIT node running on :18081

    ── 3. Dalil: Browse Both Nodes
      ✓ Oxford: ed25519:a1e573adfaf7f7961d0ec2f4...
      ✓ MIT:    ed25519:26146089de93ef9f175bca0b...

    ── 4. Cross-Node Gossip
      ✓ Oxford <-> MIT peer mesh established

    ── 5. Competing Claims (Interpretive Space)
      ✓ Oxford published: 3.2C (sha256:21921be27b6334de4...)
      ✓ MIT published: 3.4C (sha256:108cd4fb24f2c4618...)
      ✓ Both claims survive -- interpretive space, no central arbiter

    ── 6. Cross-Node Gossip Convergence
      ✓ MIT claim_count after gossip: 2 (converged)

    ── 7. Raqib: Witness Oxford Claim
      ✓ Raqib witnessed Oxford claim (unseen -> witnessed)

    ── 8. Executable Claim: Computation Result to Bay2
      ✓ Execution result written to Bay2: sha256:07e5514ef292d359111a59987...
      ✓ Computation: checksum(sha256:9b15d0d83c5f9c8da370b9145a4b29...)

    ── 9. Verified Query with Reputation Threshold
      ✓ Query resolved: 3.4C per doubling of CO2
      ✓ Score: 1 witnesses (above threshold)
      ✓ Cite as: anka:sha256:108cd4fb24f2c46186e1debd72e9c535c...

    ── 10. Bay2 Sync Verification
      ✓ Bay2 object_count: 2
      ✓ Bay2 op_count: 2

    ── 11. Shutdown and Restart (Durability)
      ✓ Oxford stopped
      ✓ Oxford restarted

    ── 12. Recovery: All Claims Fetchable After Restart
      ✓ Oxford claim recoverable: sha256:21921be27b6334de4baf31b87...
      ✓ MIT claim recoverable: sha256:108cd4fb24f2c46186e1debd7...

    ── Summary

      Bay2      object_count=2  op_count=2
      ANKA      Oxford + MIT nodes, 2 claims converged via gossip
      Dalil     winner="3.4C per doubling of CO2"  score=1  cite_as=anka:sha256:108cd4fb24f2c4618...
      Raqib     unseen -> witnessed (Oxford claim)
      Compute   execution receipt in Bay2: sha256:07e5514ef292d3591...
      Recovery  both claims fetchable after restart

    Stack demo complete. All layers verified.

      Shutting down stack...
      Stack stopped.

---

## What Each Step Proves

1.  Bay2 is the operational substrate. It stores objects, records operations,
    and maintains a causal replay log.

2.  Two ANKA nodes start independently. Each has its own identity keypair.
    Neither knows about the other until connected as peers.

3.  Dalil browses both nodes. Each node has a stable Ed25519 identity.

4.  The peer mesh is established. Claims will now propagate via signed gossip.

5.  Oxford publishes 3.2C. MIT publishes 3.4C. Same subject, same claim space.
    Both survive. Interpretive spaces allow plural claims. No arbiter decides.

6.  MIT fetches Oxford's claim. MIT now has 2 claims. The mesh converged
    without a coordinator — pure signed gossip.

7.  A Raqib agent witnesses Oxford's claim. The agent's memory updates from
    unseen to witnessed. The witness is recorded on the ANKA node.

8.  A computation result — a dataset checksum — is written directly to Bay2
    as an executable claim receipt. Bay2 is the substrate for verifiable compute.

9.  Policy collapse returns the highest-scored claim with full provenance.
    The cite_as address is permanent and content-addressed.

10. Bay2 has received objects and recorded operations. The replay log
    is the tamper-evident history of all operations.

11. The Oxford node stops and restarts. State is persisted to SQLite.
    No data is lost.

12. Both claims — Oxford's and MIT's — are fetchable after restart.
    The digest is the identity. Content-addressed storage is permanent.
