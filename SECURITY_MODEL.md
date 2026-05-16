# SECURITY MODEL

## Threat Model

The ANKA stack is designed for adversarial epistemic environments:
nodes may lie, claims may be forged, and gossip may be manipulated.
The security model ensures that no claim can be accepted without
cryptographic proof of origin, and no operation can be silently dropped.

---

## 1. Signatures

Every claim envelope is signed by the issuing node:

    claim = { claim_space, subject, predicate, object,
              evidence_refs, issuer_node_id, timestamp_unix_secs }
    digest_hex = sha256(canonical_json(claim))
    issuer_signature_hex = ed25519_sign(node_secret, digest_hex)

A claim is rejected if:
- The digest does not match the canonical JSON of the claim
- The signature does not verify against the issuer's public key
- The issuer_node_id does not match the signing key

Witnesses are also signed:
    witness = { digest_hex, witness_node_id, validation_type, timestamp_unix_secs }
    body_digest_hex = sha256(canonical_json(witness_body))
    witness_signature_hex = ed25519_sign(node_secret, body_digest_hex)

Challenges follow the same pattern.

---

## 2. Content-Addressed Storage

The digest IS the identity. A claim's address is a function of its content.
Mutating a claim produces a different digest — a different object.
There is no update operation. There is only publish.

This means:
- Claims cannot be silently modified after publication
- The cite_as address (anka:sha256:...) is permanent
- Any node can verify any claim independently

---

## 3. Capability-Scoped Access

Nodes can operate in open mode (no capabilities required) or
locked mode (capabilities required per claim space).

A capability is a signed bearer token:

    capability = { issuer_node_id, holder_node_id, claim_space,
                   rights, expires_unix_secs, nonce }
    digest_hex = sha256(canonical_json(capability))
    signature_hex = ed25519_sign(issuer_secret, digest_hex)

Rights: publish | witness | challenge | admin
Scope:  specific claim_space, or "*" for all spaces

Capabilities can be attenuated — a holder can issue a sub-capability
with equal or narrower scope, never broader.

Capabilities can be revoked. Revocation is recorded locally.

When locked, a publish to an unauthorized claim space returns 403.

---

## 4. Replay Log

Bay2 maintains a causal operation log. Every operation is:
- Assigned a digest (sha256 of its content)
- Linked to its predecessor by parent_op_digest
- Appended to the log — never modified

This gives:
- Any gap in the log is detectable
- Any reordering of operations is detectable
- Any insertion of a forged operation is detectable
- Given initial state + log, any past state is reproducible exactly

---

## 5. Federated Audit Trail

ANKA's archive records every publish, witness, and challenge event
per claim digest. The audit trail is federated:

    GET /audit/trail/{digest}
      -> queries local trail
      -> queries each peer's /audit/trail/local/{digest}
      -> merges by event_kind and timestamp
      -> deduplicates

This means:
- No single node controls the audit trail
- A node that drops its trail loses nothing — peers hold it too
- The reconstructable flag indicates whether the claim can be
  reproduced from the audit trail alone

---

## 6. Monotone Indexes

Bay2's monotone index is append-only. Entries are added, never removed.
This gives stable reads, no cache invalidation, and conflict-free merges.

Two index snapshots from different nodes can be merged deterministically:
- Union of all entries
- Deduplication by digest
- No ordering conflicts

---

## 7. Gossip Authentication

Gossip announcements carry the issuer's node_id and signature.
A node will not accept a gossip announcement unless:
- The claimed issuer_node_id matches the signing key
- The digest in the announcement matches the actual claim

Gossip is scoped to registered claim spaces. Nodes only propagate
announcements for claim spaces they have registered interest in.

---

## 8. Persistence and Recovery

State is persisted to SQLite after every request:
- node_state (claims, witnesses, challenges, known_digests)
- peers
- registry
- subscriptions
- archive (audit trail)
- bay2_store (object store state)
- capability_store

After restart, the full state is restored. No claim is lost.
The node_id is deterministic from the seed — stable across restarts.

---

## 9. What Is Not Yet Implemented

- TLS between nodes (all communication is currently plaintext HTTP)
- Stake and slash (economic enforcement — primitives exist in Bay2/ANKA)
- Cross-institution capability issuance (origin node issues, not yet federated)
- Sybil resistance (no proof-of-work or proof-of-stake at mesh level)
- Rate limiting across nodes (rate limiting exists per-node)

These are the next production hardening items.
