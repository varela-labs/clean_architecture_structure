# Authorization

## Purpose
Authorization policies at the edge (roles/claims mapping, policy setup).

## Typical contents
- Policy definitions (e.g., AddAuthorization options)
- Claims transformation and mapping (if needed)

## Out of scope
- Hard-coded authorization rules inside controllers (prefer delegating to Application policy)

## Notes
Where feasible, treat authorization decisions as application policy and enforce them in use cases.


