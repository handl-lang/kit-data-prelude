---
title: Decisions
type: index
---

# Decisions

One line per decision rule, generated from each ADR's `## Decision`
section with `host/scripts/gen-decisions.py`. The ADR is the argument;
this is the recall surface (ADR-0161 §8). Superseded records are excluded.

### Options Object Over Named Arguments

- The options argument is always the **last positional argument** — [ADR-0002](adrs/0002-options-object-over-named-args.md)
- Missing keys are treated as absent (not errors) — [ADR-0002](adrs/0002-options-object-over-named-args.md)
- null or an empty object {} is equivalent to omitting the argument — [ADR-0002](adrs/0002-options-object-over-named-args.md)
- Verb shorthands (http.get, http.post, etc.) remain positional for — [ADR-0002](adrs/0002-options-object-over-named-args.md)

### Expression Object and Array Literals

- **Array literal:** [expr, expr, ...] — [ADR-0004](adrs/0004-expression-object-array-literals.md)
- **Object literal:** { key: expr, key: expr, ... }, where a key is a bare identifier or a quoted string and a value is… — [ADR-0004](adrs/0004-expression-object-array-literals.md)
- Treat { and } as nesting tokens alongside ( and [ in argument splitting and depth tracking (split_args,… — [ADR-0004](adrs/0004-expression-object-array-literals.md)
- Add parse_array_literal and parse_object_literal to the ExprParser trait. Implementations will parse the content… — [ADR-0004](adrs/0004-expression-object-array-literals.md)
- Use the existing Expr::Value variant for object and array results; no new AST node is required because V is already… — [ADR-0004](adrs/0004-expression-object-array-literals.md)
- Update the runtime eval_arg and the typechecker parse_expr to recognize [] and {} as value expressions, evaluate/parse… — [ADR-0004](adrs/0004-expression-object-array-literals.md)

### handl-native `s.*` Schema Vocabulary

- name: a — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- name: b — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- Strings: s.min_length(n), s.max_length(n), s.length(n), s.regex(pattern) — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- Numbers/Integers: s.min_value(n), s.max_value(n), s.range(min, max), s.multiple_of(n) — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- Arrays: s.min_items(n), s.max_items(n), s.length(n) — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- Generic: s.brand(name) (for branded types; typegen can preserve the name as metadata) — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- **handl-dialect-canonical** provides SSchemaVocabulary and SSchema as the canonical implementations of… — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- **handl-typecheck-schema-s** (new crate) provides SSchemaInterpreter, implementing SchemaInterpreter by mapping s.*… — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- **handl-typegen-backend-s** (new crate) provides an SBackend that emits the canonical s schema as a JSON-serializable… — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- **handl-typegen-backend-json-schema** is rewritten as a translator from s to JSON Schema. It becomes an optional… — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- **handl-fields** removes the JSON-Schema-specific check_arg_type in computed.rs and instead compiles arg schemas… — [ADR-0005](adrs/0005-s-schema-vocabulary.md)
- **handl-compiler** default configs use SSchemaInterpreter and SBackend instead of the JSON Schema implementations — [ADR-0005](adrs/0005-s-schema-vocabulary.md)

### JSON Schema 2020-12 Reference & Composition Support in the Typechecker

- Per-field $defs: pass the field's own schema as root — [ADR-0007](adrs/0007-schema-refs.md)
- Document-level $defs: the caller builds a synthetic root object (e.g., a — [ADR-0007](adrs/0007-schema-refs.md)

### Type Aliases in `$defs`

- **Type aliases live in $defs inside $:**, with an optional typeParams — [ADR-0008](adrs/0008-type-aliases.md)
- **Aliases are type-only declarations**: they are not data fields, are not — [ADR-0008](adrs/0008-type-aliases.md)
- **References use standard $ref plus a handl args list**; args — [ADR-0008](adrs/0008-type-aliases.md)
- **No new Type variant**: the resolved $ref produces a Type (possibly — [ADR-0008](adrs/0008-type-aliases.md)

### Annotations

- **An optional annotations object is allowed on any document**; the VM — [ADR-0011](adrs/0011-annotations.md)
- **Conventional keys** are title, description, author, tags, since, — [ADR-0011](adrs/0011-annotations.md)
- **Annotations cost nothing at runtime or typecheck**; the linter may validate — [ADR-0011](adrs/0011-annotations.md)
- **Hosts may define additional conventional keys**, namespaced to avoid — [ADR-0011](adrs/0011-annotations.md)

### Custom Fields

- **User-defined fields are declared in *.field.yml files**; the core keeps — [ADR-0016](adrs/0016-custom-fields.md)
- **Core keys are** type, expr, arg, schema, inheritable, mutable — [ADR-0016](adrs/0016-custom-fields.md)
- **Field types are sugar and handler**: sugar expands to a core-language — [ADR-0016](adrs/0016-custom-fields.md)
- **A field file declares its schema and expansion**, and the resolver loads — [ADR-0016](adrs/0016-custom-fields.md)

### The `dependencies` Field

- **A built-in dependencies field lists the custom field names a document — [ADR-0017](adrs/0017-dependencies-field.md)
- **It is allowed** at the document top level, on a field declaration, in a — [ADR-0017](adrs/0017-dependencies-field.md)
- **Names are dotted**: bare (delay) for project-local fields, namespaced — [ADR-0017](adrs/0017-dependencies-field.md)
- **Resolution collects** dependencies from the document, field declarations — [ADR-0017](adrs/0017-dependencies-field.md)
- **Tooling**: handl info shows the list; handl lint may warn when a custom — [ADR-0017](adrs/0017-dependencies-field.md)

### Parameter Naming Convention

- Parameter names use snake_case — [ADR-0020](adrs/0020-parameter-naming.md)
- Names are nouns, not verbs (prefix not do_prefix) — [ADR-0020](adrs/0020-parameter-naming.md)
- Boolean parameters use is_, has_, or should_ prefixes — [ADR-0020](adrs/0020-parameter-naming.md)
- No abbreviations (config not cfg, instance not inst) — [ADR-0020](adrs/0020-parameter-naming.md)
- self — reserved for future method-like dispatch — [ADR-0020](adrs/0020-parameter-naming.md)
- host — reserved for host reflection — [ADR-0020](adrs/0020-parameter-naming.md)
- args — reserved for variadic argument access — [ADR-0020](adrs/0020-parameter-naming.md)
- name: prefix — [ADR-0020](adrs/0020-parameter-naming.md)
- name: length — [ADR-0020](adrs/0020-parameter-naming.md)

### Modality as Projection

- **A modality system built on one primitive**: project(x, K) extracts the — [ADR-0026](adrs/0026-modality-as-projection.md)
- **Six moods are uses of that projection**: indicative (strict), potential — [ADR-0026](adrs/0026-modality-as-projection.md)
- **x not K is complement projection, not Boolean negation**; Boolean — [ADR-0026](adrs/0026-modality-as-projection.md)
- **Each mood is a module** (mood.ind, mood.pot, mood.neg, mood.int, — [ADR-0026](adrs/0026-modality-as-projection.md)
- **Strict moods error on non-membership**; soft moods return null, the — [ADR-0026](adrs/0026-modality-as-projection.md)
- **Projection composes with grades and sorts** — a mood is not a separate — [ADR-0026](adrs/0026-modality-as-projection.md)

### ADR-0032 (Remaining): Types are Values — Advanced Type System Roadmap

- **data declarations for inductive types** — Define algebraic datatypes with sum-of-products structure, generating… — [ADR-0032](adrs/0032-types-as-values-remaining.md)
- **rec / termination checking** — Ensure recursive type-level definitions are total and terminating via structural… — [ADR-0032](adrs/0032-types-as-values-remaining.md)
- **Inductive families** — Enable types parameterized by values, like Vec(A, n) where n is a length index — [ADR-0032](adrs/0032-types-as-values-remaining.md)
- **Dependent pattern matching with a motive** — Pattern match on indexed types, refining the goal type based on… — [ADR-0032](adrs/0032-types-as-values-remaining.md)
- **Type inference and unification** — Infer types in expressions with _ holes; solve constraints via unification — [ADR-0032](adrs/0032-types-as-values-remaining.md)
- **Proof erasure at runtime** — ~~Remove proof terms before evaluation to reduce runtime overhead while preserving type… — [ADR-0032](adrs/0032-types-as-values-remaining.md)
- _Completed._ Built-in equality/membership proofs (type.refl, type.is_evidence) and the uninhabited type.empty are… — [ADR-0032](adrs/0032-types-as-values-remaining.md)
- **Tactics** — Provide tactic-assisted proof construction (auto, induction, rewrite, simp) for interactive type-level… — [ADR-0032](adrs/0032-types-as-values-remaining.md)

### `vau` as a Typed Escape

- **Add Scheme::Vau { params, body }**: children are bound as unevaluated — [ADR-0045](adrs/0045-vau-as-a-typed-escape.md)
- **The body may** eval a bound expression, inspect the AST, or transform it — [ADR-0045](adrs/0045-vau-as-a-typed-escape.md)
- **Add a vau keyword and grammar rule** in canonical language data; the — [ADR-0045](adrs/0045-vau-as-a-typed-escape.md)
- **vau is the only escape** from structured compositional evaluation; every — [ADR-0045](adrs/0045-vau-as-a-typed-escape.md)
- **Capability discipline covers it**: a language with vau advertises — [ADR-0045](adrs/0045-vau-as-a-typed-escape.md)

### Computed Object Keys via Bracket Syntax

- An array literal is never followed by : in expression position (the — [ADR-0057](adrs/0057-computed-object-keys.md)
- The entry node's key slot is the only place this reinterpretation — [ADR-0057](adrs/0057-computed-object-keys.md)

### Predicates as Types — Unified Dependent Typing Without a Sublanguage

- To verify x: T = e, normalize T(e) — [ADR-0068](adrs/0068-predicates-as-types.md)
- If normalization succeeds and yields true, accept statically — [ADR-0068](adrs/0068-predicates-as-types.md)
- If normalization yields false, reject — [ADR-0068](adrs/0068-predicates-as-types.md)
- If normalization is blocked (effect, non-termination, opaque value), — [ADR-0068](adrs/0068-predicates-as-types.md)
- It cannot infer A and B from an opaque function body soundly — [ADR-0068](adrs/0068-predicates-as-types.md)
- It reintroduces a type-level operation as a special form, breaking the — [ADR-0068](adrs/0068-predicates-as-types.md)
- It does not resolve the type-of-type regress (it just renames it) — [ADR-0068](adrs/0068-predicates-as-types.md)

### Failure-Tracking Arrows for Backtracking Parsers

- inl branch: wp assumes the success invariant and propagates the — [ADR-0071](adrs/0071-failure-tracking-arrows.md)
- inr branch: wp assumes the error invariant and propagates into — [ADR-0071](adrs/0071-failure-tracking-arrows.md)

### State Machine Invariants via Fixpoint Discovery

- Each transition atom has a **conditional contract**: — [ADR-0073](adrs/0073-state-machine-invariants.md)
- state.dec : Int → Int — [ADR-0073](adrs/0073-state-machine-invariants.md)
- requires: Le(0, input) — can only decrement if ≥ 0 — [ADR-0073](adrs/0073-state-machine-invariants.md)
- guarantee: Le(0, output) — result is ≥ 0 — [ADR-0073](adrs/0073-state-machine-invariants.md)
- The state machine is a loop: — [ADR-0073](adrs/0073-state-machine-invariants.md)
- The inference engine runs the fixpoint: — [ADR-0073](adrs/0073-state-machine-invariants.md)
- I₀ = body's guarantee (includes Le(0, output) from state.dec) — [ADR-0073](adrs/0073-state-machine-invariants.md)
- wp(body, I₀) = the precondition needed to preserve I₀ — [ADR-0073](adrs/0073-state-machine-invariants.md)
- For state.dec: wp = Le(0, input) (the precondition) — [ADR-0073](adrs/0073-state-machine-invariants.md)
- I₁ = I₀ ∧ wp(body, I₀) = Le(0, output) ∧ Le(0, input) — [ADR-0073](adrs/0073-state-machine-invariants.md)
- Fixpoint: the invariant Le(0, count) (Count ≥ 0) is discovered — [ADR-0073](adrs/0073-state-machine-invariants.md)
- The guarantee includes the invariant: Le(0, output) — [ADR-0073](adrs/0073-state-machine-invariants.md)
- **Data invariants**: properties of the state value itself (Count ≥ 0, — [ADR-0073](adrs/0073-state-machine-invariants.md)
- **Conditional transitions**: atoms with preconditions (can only — [ADR-0073](adrs/0073-state-machine-invariants.md)
- **Termination**: if the event stream is finite (consumed via the side — [ADR-0073](adrs/0073-state-machine-invariants.md)
- **Concurrency invariants**: "the buffer is never accessed by two — [ADR-0073](adrs/0073-state-machine-invariants.md)
- **Liveness properties**: "the counter eventually reaches zero" — this — [ADR-0073](adrs/0073-state-machine-invariants.md)
- **Global invariants**: properties spanning multiple state machines — — [ADR-0073](adrs/0073-state-machine-invariants.md)

### Arrow Surface Syntax v0.1 — Redesign

- **Correction 1 — Destructuring renaming.** A pattern element may use source: local to bind a source field/position to a… — [ADR-0074](adrs/0074-arrow-syntax-v0_1-surface-redesign.md)
- **Correction 2 — rec as a recursive region (Paterson-style).** rec **does not define a recursive arrow**. It introduces… — [ADR-0074](adrs/0074-arrow-syntax-v0_1-surface-redesign.md)
- **Addendum — Control-flow and construction sugar.** The v0.1 draft specified if, match, and rec as the only… — [ADR-0074](adrs/0074-arrow-syntax-v0_1-surface-redesign.md)
- **What is accepted unchanged from the draft.** The following from the v0.1 draft are accepted as-is: — [ADR-0074](adrs/0074-arrow-syntax-v0_1-surface-redesign.md)

### Traits as Arrow Signatures — Graph-Based Interfaces and Contracts

- **Primary mode: trait inference (default).** The user writes a graph. The system derives: — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)
- **Secondary mode: explicit declarations (optional).** When the user wants to **name** a law pattern — for… — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)
- **The open trait catalog.** Trait inference does not magically derive unknown laws from nothing. It indexed catalog.… — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)
- **Catalog storage: abstract interface, SQLite implementation.** The trait catalog is persisted in a storage backend.… — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)
- **Type parameter syntax: angle brackets, not square brackets.** Type application uses **angle brackets** F<A>, not… — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)
- **Impl declaration (graph layer — annotation-free).** An impl is a graph assignment for each operation in the trait's… — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)
- **Generic code with trait bounds.** A function may declare trait bounds on its type parameters. The bound is a… — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)
- **Supertraits as signature inclusion.** A supertrait bound trait T : U means Σ_T requires Σ_U to be satisfied first.… — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)
- **Associated types via dependent types.** A trait may declare an associated type using the dependent-type machinery… — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)
- **Blanket impls via ArrowApply; Law verification: the CutElim connection; Trait resolution: catalog search (fallback);… — [ADR-0075](adrs/0075-traits-as-arrow-signatures.md)

### Decoupled Trait Layer — Laws, Bundles, and Handlers

- **Law on an arrow.** A law is a standalone declaration that an arrow satisfies an equation. It attaches to any arrow —… — [ADR-0076](adrs/0076-decoupled-trait-layer.md)
- **Bundle.** A **bundle** is a named record of arrows plus laws over them. It is only needed when a law spans multiple… — [ADR-0076](adrs/0076-decoupled-trait-layer.md)
- **Handler.** A **handler** injects an arrow or bundle at a scope boundary. This is dependency injection over effect… — [ADR-0076](adrs/0076-decoupled-trait-layer.md)
- **How they compose.** The three features are independent. No combination is mandatory. The "trait" pattern emerges when… — [ADR-0076](adrs/0076-decoupled-trait-layer.md)
- **= in laws.** Inside a law context, = means extensional equality of arrows (both sides produce the same output for all… — [ADR-0076](adrs/0076-decoupled-trait-layer.md)
- **Resolution: handlers primary, catalog fallback.** 1. **Primary: explicit handle ... with** — names the impl,… — [ADR-0076](adrs/0076-decoupled-trait-layer.md)
- **What this replaces from ADR-0075.** with laws attached). No keyword. installation). No keyword. attachable to any… — [ADR-0076](adrs/0076-decoupled-trait-layer.md)
- **What this preserves from ADR-0075.** set. Unchanged. default). handle site. Unchanged in mechanism. normalization,… — [ADR-0076](adrs/0076-decoupled-trait-layer.md)

### Value Types as Data — Composable Capabilities and Target Representations

- **Three new data fragment types.** Extend the Language data schema (ADR-0044) with three new fragment sets, each loaded… — [ADR-0078](adrs/0078-value-types-as-data.md)
- **Value Types (value_types.yaml).** A value type declares: — [ADR-0078](adrs/0078-value-types-as-data.md)
- **Capabilities (capabilities.yaml).** A capability declares: — [ADR-0078](adrs/0078-value-types-as-data.md)
- **Target Representations (representations.yaml).** A representation declares how a value type is concretely represented… — [ADR-0078](adrs/0078-value-types-as-data.md)
- **How the compiler uses this.** The compilation pipeline becomes: — [ADR-0078](adrs/0078-value-types-as-data.md)
- **Type inference: gradual + runtime profiling, gated by language policy.** To specialize, the compiler needs to know… — [ADR-0078](adrs/0078-value-types-as-data.md)
- **Monomorphization.** Yes — the compiler monomorphizes generic operations. When sum<T: Addable + Zero> is called with T… — [ADR-0078](adrs/0078-value-types-as-data.md)
- **Relationship to TaggedValue (the handl-value crate).** TaggedValue is the **dynamic fallback representation** — the… — [ADR-0078](adrs/0078-value-types-as-data.md)
- **Relationship to ADR-0076 (Decoupled Trait Layer).** ADR-0076 decoupled traits into laws + bundles + handlers. This… — [ADR-0078](adrs/0078-value-types-as-data.md)

### Unify Arrow Dialects — Graph Blocks, No `let`, No `in`

- **Graph blocks replace let..in and x = y in body:** — [ADR-0079](adrs/0079-unify-dialects-no-let-in.md)
- **Contextual {} parsing (ADR-0074 ID.11):** { after ~>, if cond, else, match val parses as a _block_… — [ADR-0079](adrs/0079-unify-dialects-no-let-in.md)
- **eval_block binds assigns:** The tree-walk evaluator's eval_block pushes a scope, binds each assign child (x = y) as a… — [ADR-0079](adrs/0079-unify-dialects-no-let-in.md)
- **Unified grammar (overlay approach):** The arrow DSL language is built on top of the canonical language: arrow_lang.rs… — [ADR-0079](adrs/0079-unify-dialects-no-let-in.md)
- **>>> semantics:** Canonical uses App (host-call) for >>>; the arrow overlay replaces it with Seq (arrow composition)… — [ADR-0079](adrs/0079-unify-dialects-no-let-in.md)
- **Remove let and in:** Delete grammar.let.prefix and grammar.arrow.in.infix after all files are converted — [ADR-0079](adrs/0079-unify-dialects-no-let-in.md)

### Inductive Types as Desugared Predicates

- **A predicate** (the type) that recognizes values built by the constructors — [ADR-0082](adrs/0082-inductive-types.md)
- **Constructors** as ordinary values (tagged records or functions) — [ADR-0082](adrs/0082-inductive-types.md)
- **A recursor** as an ordinary library function the checker recognizes for — [ADR-0082](adrs/0082-inductive-types.md)

### Arrow Macros — Type-Safe Compile-Time Metaprogramming

- **Macros are arrows that transform arrows.** A macro is an arrow Ast ~> Ast (or more generally Scheme A B ~> Scheme A'… — [ADR-0084](adrs/0084-arrow-macros.md)
- **The macro declaration form.** A new top-level declaration, alongside op/handl/cap/const: — [ADR-0084](adrs/0084-arrow-macros.md)
- **Hygiene.** Macro hygiene prevents variable capture: a macro that introduces a variable x must not capture a caller's… — [ADR-0084](adrs/0084-arrow-macros.md)
- **Type safety.** Macros are typechecked in two phases: — [ADR-0084](adrs/0084-arrow-macros.md)
- **Compile-time execution.** Macros run at compile time, not runtime. The execution model: — [ADR-0084](adrs/0084-arrow-macros.md)
- **Quotation and splicing.** Two syntax forms for building AST in macros: — [ADR-0084](adrs/0084-arrow-macros.md)
- **Pattern matching on AST.** Macros pattern match on AST structure. With ADR-0081 (child roles) and ADR-0082 (inductive… — [ADR-0084](adrs/0084-arrow-macros.md)
- **What macros cannot do.** runtime with no fs/net/libc capabilities. A macro cannot read a file, make a network call,… — [ADR-0084](adrs/0084-arrow-macros.md)
- **Relationship to const (ADR-0083 §5.1).** const is the simplest macro — a nullary macro that produces a literal value: — [ADR-0084](adrs/0084-arrow-macros.md)
- **Relationship to data (ADR-0082).** data declarations (inductive types) are desugared to predicates, constructors, and… — [ADR-0084](adrs/0084-arrow-macros.md)

### The Frontier Calculus

- **Term gains the frontier constructors** — CellId, CellCompV, — [ADR-0101](adrs/0101-frontier-calculus.md)
- **Surface syntax exposes them as data** (the Option B grammar), not as — [ADR-0101](adrs/0101-frontier-calculus.md)
- **Engine semantics**: cells compose vertically and horizontally, whiskers — [ADR-0101](adrs/0101-frontier-calculus.md)
- **Serialization is the same as every Term** — the constructors are JSON — [ADR-0101](adrs/0101-frontier-calculus.md)
- **Relation to existing ADRs**: this is the concrete term layer for ADR-0100 — [ADR-0101](adrs/0101-frontier-calculus.md)
- **Frontier support is optional**: a model declares whether it interprets — [ADR-0101](adrs/0101-frontier-calculus.md)

### Session Types as Grades

- **Introduce grade Session** with !T (send), ?T (receive) and End; — [ADR-0102](adrs/0102-session-types-grades.md)
- **Duality dual : Session -> Session** flips every action (!T ↔ ?T, — [ADR-0102](adrs/0102-session-types-grades.md)
- **Sequential composition is grade multiplication** — !Int ; ?Bool ; End — [ADR-0102](adrs/0102-session-types-grades.md)
- **Channel operations are graded arrows** whose grade is a Session object — [ADR-0102](adrs/0102-session-types-grades.md)
- **Sessions are checked like any grade** — no separate session type system — [ADR-0102](adrs/0102-session-types-grades.md)

### Type-Level Total Evaluation of handl Expressions

- Substitute the concrete call-site type and value arguments into the function's declared return type — [ADR-0118](adrs/0118-type-level-total-evaluation.md)
- Reduce the resulting handl expressions by evaluating them in a **total** interpreter: no effects, no while/do-while… — [ADR-0118](adrs/0118-type-level-total-evaluation.md)
- Compare the reduced indices during unification. If the reduced values differ and neither side is a metavariable, report… — [ADR-0118](adrs/0118-type-level-total-evaluation.md)
- Leave expressions that cannot be reduced (because they contain unresolved variables or metavariables) in normal form… — [ADR-0118](adrs/0118-type-level-total-evaluation.md)

### Language data assembly in the `lang` repo

- crates/handl-kit-data-canonical — the fragment merger and the canonical — [ADR-0130](adrs/0130-language-data-assembly.md)
- the .hnl packages it pins (query, command, event, …) — [ADR-0130](adrs/0130-language-data-assembly.md)

### ADR: Generic Arrow Calculus for Any Dimension

- **Arrows are primitive; functions emerge.** There is no lambda calculus, no λ, no primitive functions. The only… — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
- **Two fundamental operators: () and <>.** The surface has exactly two application-like operators: — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
- **Dimensions contain any expression.** A dimension is not restricted to types. It can contain any expression: — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
- **Types are expressions; type constructors are arrows.** Types are ordinary expressions, and type constructors are… — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
- **Generic arrows and objects are arrow families.** Generic arrows are arrow families — arrows over dimensions: — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
- **Dependent types: dependency is not restricted to types.** Expressions can depend on other expressions: — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
- **Proofs are ordinary typed expressions (Curry–Howard).** P : Type p : P — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
- **Graded arrows.** Grades annotate arrows: — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
- **Grade algebras are ordinary structures.** Grade systems are ordinary structures rather than hard-coded language… — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
- **Arrow combinators are the computational vocabulary; Quantification is consistent with dimension binding.** See the… — [ADR-0146](adrs/0146-generic-arrow-calculus-any-dimension.md)
