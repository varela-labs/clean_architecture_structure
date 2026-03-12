# Controllers/_Shared

## Purpose

Shared controller utilities kept small and focused (base controller, shared helpers).

## Typical contents

- BaseController (common helpers like correlation ID access)
- Shared response mapping helpers (thin)

## Out of scope

- A large inheritance hierarchy with hidden behavior

## Notes

Prefer composition over deep controller inheritance.


