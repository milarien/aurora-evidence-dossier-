# Current Runtime Architecture

**Status:** Locked — do not refactor without updating this document.  
**Purpose:** Plainly state the current production architecture so that
Cursor, Codex, and future contributors do not hallucinate the shape of
the system or attempt to merge its components.

---

## The Production Chain
Lens → verification flags → policy → GovernanceDecision → CanonicalScannerGateBridge → Governor/ledger

This is the live path. Every component in this chain has a distinct role.
None of them are layers of a single thing. They are separate concerns with
separate invariants.

---

## Component Roles

**Aurora**
The underlying architecture and substrate. Not directly invoked in the
runtime governance path. Do not conflate with Lens, Governor, or PEF.

**Lens**
The admissibility gate. Lens decides whether output may pass into
consequence. It produces verification flags and resolves policy. It does
not write the ledger. It does not manage persistent state.

**Governor**
The policy resolver and ledger path. Governor receives the GovernanceDecision
from Lens and writes the tamper-evident audit record via
CanonicalScannerGateBridge. It does not make admissibility decisions.
That is Lens's job.

**PEF (Persistent Existence Framework)**
The persistent substrate required for discourse-level continuity. PEF
holds state across turns. It is not a memory system. It is not a cache.
Ambiguity and hold behaviour surface here and must be visible in the
ledger.

**CanonicalScannerGateBridge**
The live production Governor + ledger path. Writes flat JSONL audit rows
with HMAC chain. This is the forensic path. It is not BuiltinBridge.

**BuiltinBridge**
In-process, test-style bridge only. Not the forensic path. Not for
production use.

---

## Why These Components Stay Separate

Lens can hold or refuse without Governor being invoked.
Governor can write a ledger record without PEF state being present.
PEF can hold ambiguity without Lens having reached a decision.

Each component can fail or hold independently. Collapsing them loses
that property. A system where admissibility, policy resolution, persistent
state, and audit writing are one blob cannot verify which part failed or
held, and cannot produce a clean audit record of the decision path.

The separation is not architectural preference. It is a forensic
requirement.

---

## Current Finished-State Principles

1. Keep the roles separate: Aurora, Lens, Governor, PEF.
2. `CanonicalScannerGateBridge` is the live production Governor + ledger
   path.
3. `BuiltinBridge` is test/in-process only.
4. Do not rename ScannerGate until this document is superseded.
5. The audit/ledger path is clean, verifiable, and boring by design.
6. PEF ambiguity and hold behaviour must be visible in the ledger.
7. The demo and README explain the actual current architecture, not a
   future ideal.

---

## What Is Parked

The compositional primitives thread is parked, not discarded. It is
lower-level Aurora substrate work. It does not belong in the current
Lens/Governor/ledger finish line.

---

## What Is Not This Document's Job

This document does not describe the future architecture.
This document does not explain Aurora's theoretical foundations.
This document does not justify design decisions beyond what is needed to
prevent collapse of the component boundaries.

For theoretical foundations see the published preprints.
For maintained roadmaps, see [Roadmap References](#roadmap-references) below.

---

## Roadmap References

- PEF/operator/forensics: `.cursor/plans/pef_operator_forensics_roadmap.plan.md`
- Structural Governor/kernel parity: `docs/STRUCTURAL_GOVERNOR_ROADMAP.md`
