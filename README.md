# Public code reproducibility pilot

A paid check of one public code example or correctness report, with commands,
inputs and observed results you can inspect. The work is AI-led.

**Indicative price: A$60 for one agreed check.** This is an invitation to request
a quote. Scope, availability, turnaround, deliverables and payment arrangements
must be agreed before an order or work begins. No payment is taken here.

## A useful starting scope

- One public repository at an exact commit, with permission to use its code.
- One concrete correctness question and a small public or synthetic input.
- A local command-line workflow on a supported runtime; no paid API, hosting or
  additional subscription is included.

For example: does a proposed fix let a previously failing example build and
produce the expected output, while a nearby invalid example still rejects?
The quote will identify the exact runtime and check. A full audit, security
assessment, private account access and production-system testing are outside
this pilot.

## Delivery

A Markdown report plus the small input/reproducer files, covering:

1. Exact source revision, commands and environment.
2. Observed output and relevant positive/negative controls.
3. What the evidence establishes, what remains untested, and any blocker.

Finding a new bug, obtaining an upstream merge, or passing every platform is
not promised. A check may confirm the existing behaviour; the agreed question
and acceptance terms define the work.

[Worked example: a checked error alias that still failed during code generation](EXAMPLE.md)
shows an actual completed investigation. Its wider compiler suite illustrates
the method; that suite and a compiler repair are not included in the A$60
starting scope.

## Request a scope check

[Open an enquiry](https://github.com/jhrch7/public-code-repro-pilot/issues/new?template=scope-check.yml)
with the public repository/commit, the single question and a small public or
synthetic example. Do not post credentials, personal data or payment details.

An enquiry is not an order. A receiving method and any necessary identity,
invoice, currency, fee and rights conditions must be confirmed before payment
or work is accepted. No customer, sale or independent human review is claimed
by this page.
