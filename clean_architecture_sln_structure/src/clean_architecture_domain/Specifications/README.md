# Specifications

## Purpose
Reusable business predicates/criteria expressed without depending on a specific persistence technology.

## Typical contents
- ISpecification<T>
- Specification combinators (And/Or/Not)
- Business rules as predicates

## Out of scope
- EF Core-specific Expression building that leaks provider concerns (unless you explicitly accept it)

## Notes
If you later decide to implement specifications via LINQ Expressions for EF, document that exception in an ADR.


