---
title: "“Clang” CFE Internals Manual — Clang 24.0.0git documentation"
url: "https://clang.llvm.org/docs/InternalsManual.html#verifying-diagnostics"
domain: "clang.llvm.org"
created: "2026-08-31 05:21"
tags:
  - web-highlight
  - notaty
---

# “Clang” CFE Internals Manual — Clang 24.0.0git documentation

- **Source URL:** [https://clang.llvm.org/docs/InternalsManual.html#verifying-diagnostics](https://clang.llvm.org/docs/InternalsManual.html#verifying-diagnostics)
- **Captured:** 2026-08-31 05:21

---

## Highlights

> "Clang -cc1 supports the -verify command line option as a way to validate diagnostic behavior. This option will use special comments, called directives, within the test file to verify that expected diagnostics appear in the correct source locations. If all of the expected diagnostics match the actual output of Clang, then the invocation will return normally. If there are discrepancies between the expected and actual output, Clang will emit detailed information about which expected diagnostics were not seen or which unexpected diagnostics were seen, etc. A complete example is:

// RUN: %clang_cc1 -verify %s
int A = B; // expected-error {{use of undeclared identifier 'B'}}" `[YELLOW]`
— *Captured at 2026-08-31 05:21*

