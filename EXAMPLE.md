# Worked example: error aliases accepted by a checker but not emitted correctly

This is a completed public investigation, not a new test run for this page.

The investigation, explanatory text and repair were AI-led, with agent-run
local validation. No independent human review is claimed.

## The question

After the checker change in [Hybrid #3325](https://github.com/limitlessprojects/Go-Hybrid/pull/3325),
would valid functions and closures ending in an alias of builtin `error`
survive the emitter, Go build and execution?

## Exact source and result

- Unmodified base: `a28ea1e371dc14b008b2b65d6dfbc23352f7a8bb`.
- Repair: `7f7949ffb5267ab0af8767a7442e72ea7254784c`.
- Actual local environment: macOS arm64, Rust 1.99.0 and Go 1.26.9.
- [Rust regression source](https://github.com/jhrch7/Go-Hybrid/blob/7f7949ffb5267ab0af8767a7442e72ea7254784c/compiler/crates/hyb/tests/error_alias_emission_3323.rs).
- [Local validation notes](https://github.com/jhrch7/Go-Hybrid/blob/7f7949ffb5267ab0af8767a7442e72ea7254784c/spikes/error-alias-emission-3323/RESULTS.md).

Five valid programs were checked independently. On the base, the plain-error
control built and ran, while four alias cases failed during emission or Go
assignment checking. With the repair, all five built and produced the expected
output. A non-error alias still rejected with `HYB-E2011`.

| Case | Base | With repair |
| --- | --- | --- |
| Plain `(int, error)` propagation | `0 sentinel` | Same |
| Caller returns an error alias | Emission rejects `?` | `0 sentinel` |
| Top-level callee returns an error alias | Go assignment arity fails | `callee` |
| Closure body uses a chained error alias | Emission rejects `?` | `0 sentinel` |
| Called closure returns an error alias | Go assignment arity fails | `ok` |
| Alias is `int`, not `error` | HYB-E2011 | Same rejection |

The added Rust regression file failed without the three emitter changes
(1 passing test, 1 failing test) and passed with them. Broader local checks then
passed: 2,509 workspace tests, 130/130 corpus verdicts, and 42/42 accepted
build-and-run cases plus 88/88 rejection cases in the differential loop.

## Limits retained

The first Make invocation failed because an existing runner recipe did not
quote a source path containing spaces. The remaining constituent checks were
run directly in owned scratch. The runtime's exact locked dependencies had to
be fetched before the full offline differential loop could pass. These were
reported separately from the compiler defect.

[Repair #3380](https://github.com/limitlessprojects/Go-Hybrid/pull/3380) was
submitted and its exact author, body and commit verified on 2 November 2026.
At that checkpoint hosted CI required maintainer action. This example does not
claim an upstream merge, third-party acceptance, bounty award or payment.
The checker fix in #3325 is credited to its author, dextermos-dev.

## Follow-through — 3 November 2026

The 2,509-test figures above describe the original repair checkpoint. The
[refreshed PR source](https://github.com/jhrch7/Go-Hybrid/commit/4d17b5e008cd1a25ba43ace02d483e56e688361e)
integrates upstream through `31e8806889a585093abd1003f0a5aebfd95550f0`.
On that pinned source, all 2,529 local workspace tests passed, along with
130/130 corpus verdicts, 42/42 accepted build-and-run differential cases,
88/88 rejection cases and all ten examples. The unchanged alias regressions
remain part of that result.

[Refreshed validation notes](https://github.com/jhrch7/Go-Hybrid/blob/4d17b5e008cd1a25ba43ace02d483e56e688361e/spikes/error-alias-emission-3323/RESULTS.md)
retain the toolchain pins and limits. Hosted CI on the refreshed head still
awaited maintainer approval when last observed; merge and any bounty award
remain unconfirmed. This follow-through changes neither the original baseline
results nor the distinction between local validation and upstream acceptance.

This page is original explanatory text. Linked projects and code retain their
own licences. No private report or customer data is included.
