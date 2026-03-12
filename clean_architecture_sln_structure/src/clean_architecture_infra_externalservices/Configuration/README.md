# Configuration

## Purpose

POCO settings models for external clients (base URLs, timeouts, credentials references).

## Typical contents

- ClientSettings classes
- Timeout and retry configuration defaults

## Out of scope

- Secret storage implementation
- Direct IConfiguration reads from inner layers

## Notes

Keep actual binding/registration in Infra-IoC/Presentation; this folder holds models and defaults only.

## References

- <https://learn.microsoft.com/en-us/dotnet/core/extensions/options>
