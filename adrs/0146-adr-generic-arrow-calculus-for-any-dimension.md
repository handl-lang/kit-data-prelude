+++
id = "ADR-0146"
title = "ADR: Generic Arrow Calculus for Any Dimension"
status = "open"
priority = "medium"
+++

---
title: 'ADR: Generic Arrow Calculus for Any Dimension'
type: adr
date: 2026-10-16
status: proposed
status_note: Proposed.
---


# ADR: Generic Arrow Calculus for Any Dimension

## Decision

1. **Arrows are primitive; functions emerge.** There is no lambda calculus, no `λ`, no primitive functions. The only computational primitive is the **arrow**. Functions are the degenerate pure arrows (Hughes's `arr`); everything else — combinators, type constructors, grade algebras — is expressed with arrows over typed expressions.
2. **Two fundamental operators: `()` and `<>`.** The surface has exactly two application-like operators:
3. **Dimensions contain any expression.** A dimension is not restricted to types. It can contain any expression:
4. **Types are expressions; type constructors are arrows.** Types are ordinary expressions, and type constructors are arrows:
5. **Generic arrows and objects are arrow families.** Generic arrows are arrow families — arrows over dimensions:
6. **Dependent types: dependency is not restricted to types.** Expressions can depend on other expressions:
7. **Proofs are ordinary typed expressions (Curry–Howard).** P : Type p : P
8. **Graded arrows.** Grades annotate arrows:
9. **Grade algebras are ordinary structures.** Grade systems are ordinary structures rather than hard-coded language features:
10. **Arrow combinators are the computational vocabulary; Quantification is consistent with dimension binding.** See the design doc for these decisions.

## Why

We have an arrow-calculus kernel (ADR-0052) and a v0.1 surface syntax (ADR-0074, ARROW_LANGUAGE_SPEC_V0_1.md) that covers the 1-dimensional case: arrows `A ~> B`, composition `>>>`, product `***`, fan-out `&&&`, choice `|||`, and feedback `loop`/`rec`. The frontier calculus (ADR-0101) introduced 2-cell machinery and grades. ADR-0102 showed grades (session types) fit over the arrow calculus as data.

## Not doing

- none recorded — legacy record; the design doc lists what was deferred.

## Consequences

- **One composition operator.** `>>>` composes arrows, grades, and
- **One expression system.** Types, proofs, grades, algebras, values, and
- **HKT, generics, and dependent types are free.** Type constructors are
- **Grade systems are pluggable.** Algebras are ordinary structures
- **No lambda calculus.** Functions emerge from arrows; the kernel stays

## Enforcement

- `plugin-engine/src/term.rs` — where this is true.
- `plugin-engine-parse-pratt` — where this is true.

## Design

The full record (mechanism, tables, proofs, trade-offs): [`design/0146-generic-arrow-calculus-any-dimension.md`](../design/0146-generic-arrow-calculus-any-dimension.md).
