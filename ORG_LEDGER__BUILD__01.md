# ORG LEDGER BUILD 01 — SV-Co-Pilot

Status: APPARATUS FILED; GENESIS REQUESTED (manifest-directed; execution route below)
Authority: NONE (contracts and records only; no ledger write is claimed by this record)
Instruction: the owner's build instruction of 2026-11-04 — build the same
organization ledger for SV-Co-Pilot as the three verified Orgs hold.
Designation: BRIDGE_ORG__DESIGNATION__01.md (this repository, 2026-11-03).

## 1. What the same ledger is, in a working Org

Each verified Org (SV-LLM, StegVerse-org, StegVerse-Labs) holds its ledger on
the dedicated git ref `refs/stegverse/organization-ledger` in its own
.github repository: an ORGANIZATION chain (HEAD.json + receipts/) and a
REPOSITORY chain in the same ref's subtree
(repository-ledger/<Org>/.github/HEAD.json + its receipts), published by one
fast-forward push under ORGANIZATION_LEDGER_LOCK. The default branch carries
the contracts and emitter at .stegverse/transition-ledger/; appends execute
only through the Org's runtime substrate (org-kernel/ + resident-runtime/)
on a checkout — manifest-directed, never by direct ref edits. Receipts
verify under the canonical rule: SHA-256 of the canonical JSON of the body
without receipt_sha256 equals the receipt's filename address and its stored
receipt_sha256; chains walk previous_receipt_sha256 to genesis (null).

## 2. Filed by this build (commit 6c238bde4fc2a8f52562b502bd0d1c45c6eb87ff)

- .stegverse/transition-ledger/org-contract.json — sha256
  a1b181bec7e396f027c9a000ac1a72e1af8ec42d1a81038966c1eedbe1e38f17.
  Designates refs/stegverse/organization-ledger in SV-Co-Pilot/.github as
  this Org's ledger root (ORGANIZATION level; consumes repo and canonical
  state-transition receipts; write mode MANIFEST_DIRECTED_APPEND; lock
  ORGANIZATION_LEDGER_LOCK; propagation target master-records/.github,
  records-and-reconstruction only). Parameterized from the StegVerse-Labs
  contract: only the Org-designating fields differ (organization, ledger
  repository, propagation remote, designation source).
- .stegverse/transition-ledger/contract.json — sha256
  dfd8621d9537923399062df580901ee866232afde6190923e962ca248a1295bb.
  The REPOSITORY contract for SV-Co-Pilot/.github: its chain lives in the
  ref subtree repository-ledger/SV-Co-Pilot/.github, published by the same
  push under the same lock; repository replay never reads an organization
  receipt.
- .stegverse/transition-ledger/emit.py — sha256
  33a665ea35d3dc41c0844dcb6c67fb0fca301180846189632c0bfe815d456536,
  byte-identical to the working Orgs' emitter. It requires the runtime
  substrate at execution time (org-kernel/kernel.py for the heartbeat
  reference; resident-runtime/ledger_store.py for the store) and binds
  state hashes from the materializer — supplied, never derived from the
  host. The runtime substrate is NOT copied into this Org by this build:
  in the working Orgs it is the Org's own resident runtime, and here it is
  supplied by the executing environment (see §3), not vendored from another
  Org's runtime.

All three files read back from the repository byte-identical after commit.

## 3. Genesis request (manifest-directed; the remaining execution)

The ledger ref does not exist yet in this repository. Creating it is a
git-ref act under ORGANIZATION_LEDGER_LOCK on a checkout — the coordinator's
connector exposes branch writes only (refs/heads/*) and no create-ref or
push for a non-heads ref, so genesis executes on a git-capable surface: the
Org's designated builder (GitHub Copilot's coding-agent environment) or the
owner's git client, identically:

1. In a checkout of SV-Co-Pilot/.github with the runtime substrate present
   (org-kernel/ and resident-runtime/, as in a working Org), run the
   repository genesis through the emitter with the store addressed by the
   contract's locator —
   STEGVERSE_REPO_LEDGER_ROOT =
   git+SV-Co-Pilot/.github#refs/stegverse/organization-ledger:repository-ledger/SV-Co-Pilot/.github
   — transition: the DESIGNATION of this Org (evidence:
   BRIDGE_ORG__DESIGNATION__01.md, sha256 d5e89169… as filed; designation
   commit 2e88741f…; this build's apparatus commit 6c238bde…). The store's
   first append (expected HEAD = none) creates the ref and publishes the
   repository chain's genesis HEAD. Predecessor/successor state hashes are
   bound by the materializer at execution, per the emitter's rule.
2. Mint the ORGANIZATION genesis through the org ingest path under the same
   lock: the same designation transition at ORGANIZATION level, consuming
   the repository genesis receipt — emitting
   stegverse.organization-transition-receipt/v1 with
   previous_receipt_sha256 = null, and publishing the org HEAD.json.
3. Verify before reporting: walk both chains HEAD→genesis under the
   canonical rule (0 breaks, 0 orphans; each chain's walk independent —
   repository replay never reads an organization receipt), then file the
   result with both head receipt digests on StegVerse-Labs/.github #3402
   and as an addendum to this record. Until that filing, this Org's ledger
   state is: DESIGNATED, APPARATUS FILED, GENESIS NOT EXECUTED — and no
   receipt, admission, or runtime effect may be claimed for it.

## 4. Standing rules carried from the verified Orgs

- Appends only via the runtime under ORGANIZATION_LEDGER_LOCK, from
  manifest-directed requests; the ref is never edited by hand.
- Master-records propagation is records/reconstruction only; it never
  gates this Org's runtime reality.
- The genesis SV-Co-Pilot's ledger will certify is its designation — the
  same class of first transition the namespace genesis awaits in SV-LLM.
