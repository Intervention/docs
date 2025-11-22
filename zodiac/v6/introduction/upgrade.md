---
title: "Upgrade Guide"
subtitle: "Upgrade from Intervention Zodiac 5 to 6"
lead: "Learn how to migrate from Intervention Zodiac version 5 to version 6. See what new features are available and what changes have been made in the update."
sort: 2
---

[TOC]

## New Features

Intervention Zodiac 6 has been rewritten from the ground up with very little code carried
over from the previous version. There is the following key feature that further improves the library.

- [Support for chinese zodiac sign calculation](/v6/api/calculator)

## API Changes

- `ZodiacInterface::class` has been renamed to `SignInterface::class`
- [Calculator::zodiac()](/v5/api/calculator) is now handled by [Calculator::fromString()](/v6/api/calculator), [Calculator::fromDate()](/v6/api/calculator) and [Calculator::fromUnix()](/v6/api/calculator)
- [Calculator::compare()](/v5/api/calculator) has a slightly different signature with renamed parameter names
- [ZodiacInterface::localized()](/v5/api/zodiac#localized-title) has been renamed to [SignInterface::localize()](/v6/api/sign#localized-title)

## Removed Features

- `ZodiacInterface::start()` no longer exists
- `ZodiacInterface::end()` no longer exists
