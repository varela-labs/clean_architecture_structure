# Options

## Purpose

Strongly-typed options models and (optional) validators used for DI wiring.

## Typical contents

- Settings POCOs bound from configuration
- Options validation (`IValidateOptions<T>`)

## Out of scope

- Direct IConfiguration usage spread across the codebase

## Notes

Prefer POCO options + validation at startup to fail fast on misconfiguration.

## References

- <https://learn.microsoft.com/en-us/dotnet/core/extensions/options>
