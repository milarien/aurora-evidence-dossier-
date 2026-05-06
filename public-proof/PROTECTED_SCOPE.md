# Protected Scope

## Public materials

This public-proof package may describe:
- category boundary
- runtime architecture at component level
- production chain names
- admissibility and lawful continuation concepts
- audit and forensic purpose
- what reviewers may evaluate from public material

## Protected materials

This package must not expose:
- production runtime code
- private schemas
- private policy matrices
- customer or deployment logic
- evaluator algorithms
- HMAC keys, secrets, credentials, or environment variables
- protected PEF internals
- deployment-sensitive architecture
- commercial integration details

## Reason for boundary

The purpose of this package is to make the architecture legible without disclosing protected implementation materials.

Public review may evaluate the category, component separation, forensic posture, and admissibility-governance claim.

Production evaluation requires separate written agreement.
