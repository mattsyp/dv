# Shoal Repository Evaluation

## Executive Summary

**Repository:** `shoal-main`  
**Evaluation lens:** Personal proof-of-concept / learning project  
**Primary question:** Does this repository provide evidence of Senior Software Engineer or higher hands-on technical capability?  
**Git history:** Not available in the supplied ZIP  
**Primary technologies:** Python, SQLite, Lagoon semantic scoring  
**Approximate Python size:** ~6,000 lines total, including ~3,275 source lines and ~2,200 test lines  
**Collected tests:** 208  
**Executed locally without Lagoon dependency:** 78 parser, storage and vocabulary tests, all passing

### Overall assessment

Shoal provides **strong evidence of current Senior Software Engineer hands-on capability**.

The strongest signal is not simply that it wraps Lagoon. It takes Lagoon's semantic output and builds a nontrivial retrieval system around it with its own document model, hierarchical parsing, chunk storage, corpus-relative selectivity, query-time scoring, custom-vocabulary learning, result diversity and diagnostic tooling.

The implementation also shows iterative problem solving. `phase2_notes.txt` records specific retrieval failures, hypotheses about root causes, experiments, changes and measured improvements. That is meaningful repository evidence of debugging and engineering reasoning even though Git history is unavailable.

The project is clearly experimental. Its own documents call it a proof of concept and test bed. That context matters. Stale documentation, incomplete Phase 3 work and some missing production hardening should not be interpreted as evidence against Senior-level capability.

There are, however, two important correctness defects in the current retrieval implementation:

1. The custom-word "lightning rod" candidate path does not apply the caller's `tags` or `min_confidence` constraints before its results are merged with standard results.
2. The standard reef-overlap path divides directly by `reef_l2_norm` despite a module-level `_L2_NORM_FLOOR` intended to prevent short, low-norm chunks from receiving inflated scores. The separate lightning-rod scoring path applies the floor correctly.

Those are real flaws because they affect search semantics. They are also the kind of defects I would expect a Senior engineer to be able to recognize and repair quickly once pointed out. In a personal POC, they should be used as targeted interview probes rather than as production-readiness failures.

### Level signal

**Repository-only hands-on level demonstrated:**  
**Strong Senior Software Engineer, with some Senior+/Staff-style experimentation in retrieval design and semantic-system integration.**

I would not call this Staff evidence by itself because the repository does not demonstrate organizational technical influence or large-scale production ownership. It does, however, demonstrate the kind of technical breadth, experimental method and cross-layer reasoning often expected of strong Senior engineers.

### Rust vs. loss of hands-on depth

Shoal strongly supports the **rusty Senior Engineer** hypothesis.

The implementation is too concrete and too detailed to fit the pattern of someone who can only talk architecture. The engineer is working through SQL retrieval formulas, corpus statistics, parser edge cases, vocabulary-learning mechanics, score calibration and testable quality hypotheses.

---

# 1. Repository Context

Shoal describes itself explicitly as a proof-of-concept retrieval engine and the retrieval component of a possible RAG system.

`README.md:1-5` states that its purpose is to stress-test Lagoon's reef-based semantic scoring on real documents. It ingests documents, parses hierarchical sections, chunks them using topic-shift detection, scores chunks against semantic reefs and stores structured metadata in SQLite.

The design intentionally avoids vector databases and embedding retrieval. Instead, Shoal treats Lagoon's named semantic "reefs" as structured retrieval features that can be stored and queried relationally.

The repository currently contains:

- package API and CLI
- Markdown and plaintext parsing
- hierarchical section modeling
- Lagoon-based semantic chunking
- structured SQLite storage
- reef-overlap retrieval
- corpus-level reef IDF
- quality gating
- result diversity
- learned custom vocabulary
- custom-word candidate retrieval
- query diagnostics
- retrieval-quality experiments
- corpus acquisition scripts

The README status table at `README.md:88-105` is stale. It says Phase 2 vocabulary extension is planned and claims 68 tests. The repository actually contains a substantial Phase 2 implementation and 208 collected tests.

This is documentation drift, not missing implementation.

The supplied archive contains no `.git` directory, so authorship, commit sequences and code evolution cannot be established through Git history.

**Evidence strength: Strong context**

---

# 2. Architecture and System Decomposition

Shoal has clear boundaries that map well to the problem:

- `_models.py`: shared domain structures
- `_parsers.py`: document structure extraction
- `_ingest.py`: orchestration of parsing, analysis, vocabulary learning and chunk persistence
- `_vocab.py`: custom vocabulary discovery and injection
- `_storage.py`: relational persistence and SQL retrieval
- `_retrieve.py`: query-level retrieval policy
- `_engine.py`: top-level public orchestration
- `_cli.py`: command-line interface

The decomposition is purposeful rather than decorative.

`README.md:218-264` describes Lagoon as the semantic-analysis dependency and SQLite as the structured retrieval backend. The code follows that boundary. Lagoon owns word scoring and document analysis. Shoal owns corpus interpretation, persistence, learned vocabulary and retrieval policy.

This is important because the engineer does not reimplement Lagoon internals inside Shoal. Instead, Shoal consumes the existing abstraction and adds the missing system behavior around it.

## Strong example: retrieval split between storage and policy

`src/shoal/_storage.py:485-587` contains the SQL mechanics for reef-overlap scoring.

`src/shoal/_retrieve.py:53-205` owns higher-level query behavior:

- stop-word detection
- quality gate
- custom-word detection
- candidate generation
- lightning-rod boosting
- standard retrieval
- deduplication
- diversity filtering
- query diagnostics

That boundary is sensible. Storage knows how to retrieve and score rows. Retrieval knows why different retrieval paths should be combined.

## Strong example: vocabulary extension is isolated

`src/shoal/_vocab.py:30-286` owns:

- startup reinjection
- unknown-word observations
- context blending
- occurrence thresholds
- reef-size adjustment
- specificity
- weight calculation
- persistence handoff

`_ingest.py` calls this pipeline but does not duplicate its mechanics.

**Assessment: Senior-level decomposition**

---

# 3. Ability to Move Between Architecture and Code

This is one of Shoal's strongest areas.

The repository describes high-level concepts and then implements their difficult details.

## Concept: two-pass vocabulary learning

At the design level, an unknown word should first be observed in context, associated with semantic reefs and then become useful during a second semantic analysis.

The implementation at `src/shoal/_ingest.py:105-166` performs exactly that sequence:

1. analyze each section
2. collect unknown-word observations
3. persist observations
4. build custom vocabulary
5. if vocabulary changed, re-analyze sections
6. track custom words in final chunks

The code also avoids unnecessary second-pass work. If no new words are learned, it reuses Pass 1 analysis rather than rescoring the entire document.

That is a concrete implementation optimization, not just architectural intent.

## Concept: learned semantic association

`src/shoal/_vocab.py:66-138` blends sentence-level and chunk-level reef context.

High-confidence sentences receive 70% sentence weight and 30% chunk weight. Lower-confidence sentences reverse those weights.

`src/shoal/_vocab.py:178-252` then aggregates those observations, adjusts reef scores for reef size, applies absolute and relative thresholds, caps association breadth and asks Lagoon to compute calibrated custom weights.

This is meaningful algorithmic implementation.

## Concept: custom terms as precise retrieval anchors

`src/shoal/_retrieve.py:116-165` creates a second candidate path for chunks that contain custom vocabulary words. It then combines literal custom-word evidence with semantic reef-overlap scoring.

The repository calls this a "lightning rod." The design exists to solve a real observed failure: broad semantic retrieval could miss or confuse rare named terms.

This is exactly the kind of architecture-to-code transition the evaluation guide asks us to find.

**Assessment: Strong Senior-level evidence**

---

# 4. Implementation Fluency

The Python code appears mechanically fluent.

Positive evidence includes:

- dataclasses for transport/domain structures
- typed signatures
- context-manager support
- appropriate use of `TYPE_CHECKING`
- focused helper functions
- comprehensions used where readable
- parameterized SQL
- SQLite row factories
- explicit resource lifecycle
- test fixtures
- sensible use of dictionaries, sets and counters
- simple algorithms expressed directly rather than wrapped in unnecessary classes

The code also includes more difficult implementation work than ConceptFor.

Examples include:

- hierarchical section trees
- cursor-aware character-offset reconstruction
- corpus-level IDF
- multiple retrieval paths
- result merging and deduplication
- learned custom vocabulary
- data-dependent semantic weighting
- runtime scorer mutation

## Mechanical fluency

**Evidence level: Strong**

There is little evidence of someone struggling to express solutions in Python.

## Engineering depth

**Evidence level: Strong**

The vocabulary path and retrieval system require reasoning about data semantics and scoring behavior beyond routine application code.

---

# 5. Error Handling and Failure Modes

Failure reasoning is mixed.

## Positive evidence

The code handles several expected conditions intentionally:

- storage access before connection produces an explicit `RuntimeError`
- empty documents and sections return clean empty results
- no-result queries are supported
- stop-word-only queries are suppressed
- low-confidence semantic queries are suppressed
- duplicate chunk text is removed during ingestion
- custom vocabulary injection tolerates words that are already present
- old custom-vocabulary database rows with zero stored weights are migrated at startup
- hash collisions or changed scorer state are handled during vocabulary insertion

The project also shows awareness that retrieval can fail semantically even when the code executes successfully. That is a major strength. Query confidence, unknown vocabulary and document-size bias are treated as failure modes.

## Concern: ingestion is not atomic

`src/shoal/_ingest.py:53-84` inserts the document, tags and sections before semantic analysis is complete.

The individual storage methods commit independently.

If Lagoon analysis, vocabulary building or chunk insertion fails later, Shoal can leave a persisted document with tags or sections but without a complete chunk set.

For a personal corpus experiment this is acceptable debt. For a durable ingestion system I would expect a document-level transaction or explicit incomplete-state marker.

## Concern: broad `ValueError` suppression

`src/shoal/_vocab.py:51-62` and `255-262` treat any `ValueError` from `add_custom_word()` as an already-known word or hash collision.

That may be the only `ValueError` Lagoon currently raises there, but the handler encodes an assumption about dependency behavior and can hide future validation errors.

**Assessment: Moderate to strong for POC scope**

---

# 6. Data Semantics and Correctness

This is a strong area.

The engineer consistently asks what stored values mean rather than simply persisting raw outputs.

Examples:

- chunk reef z-scores are normalized into a relational table
- corpus frequency is used to derive reef IDF
- section hierarchy is preserved separately from chunk boundaries
- custom vocabulary preserves both learned semantic associations and stable database identity
- exact chunk text hashes prevent duplicate content
- query metadata includes confidence, coverage and matched-word counts
- custom-word tags let runtime Lagoon word IDs map back to persistent Shoal vocabulary records

The distinction between a Lagoon runtime `word_id` and the stable `custom_words.id` is particularly important.

`src/shoal/_vocab.py:254-282` initially injects a new word with a temporary tag, persists it and then changes the scorer's runtime tag to the stable database ID.

That is evidence of careful identity semantics.

## Concern: tag and confidence constraints are violated by one retrieval path

This is the most important current correctness issue.

The public `search()` API accepts `tags` and `min_confidence` at `src/shoal/_retrieve.py:58-60`.

The standard retrieval call passes both constraints to storage at lines `172-177`.

The lightning-rod path at lines `120-128` does not.

It fetches candidate chunks solely from `get_chunks_by_custom_words()` and then calls `score_chunks_by_reef_overlap()`. Neither function accepts tags or minimum confidence.

Those results are later merged ahead of standard results at lines `180-193`.

Observed fact:

- standard candidates obey filters
- lightning candidates do not

Interpretation:

A search requesting `tags=["biology"]` or a minimum chunk confidence can return a custom-word result outside those constraints.

This is not production-polish debt. It is a semantic bug in the API contract.

**Signal interpretation:** Concern, but very fixable

---

# 7. Testing Strategy

Shoal has the strongest test footprint of the repos evaluated after Lagoon.

`pytest --collect-only` finds **208 tests**.

The tests cover:

- parsers
- section trees
- storage CRUD
- foreign-key behavior
- reef storage
- selectivity filtering
- retrieval scoring
- custom-word storage
- vocabulary learning
- ingestion
- engine integration
- query retrieval
- retrieval-quality benchmarks
- negative constraints
- result diversity
- query robustness

I was able to execute the parser, storage and vocabulary suites without the external Lagoon package by isolating the portions that do not require a real scorer.

**Result: 78 passed, 0 failed.**

The full suite requires the separate Lagoon package and its data files, which were not included in this ZIP, so I do not claim full-suite runtime verification.

## Particularly strong testing signal: known failures are encoded

`tests/test_retrieval_quality.py:202-231` contains strict `xfail` cases for known retrieval weaknesses.

That is useful because known failures are not silently omitted from the suite.

Examples include:

- crane-bird disambiguation
- crane-machine ambiguity
- apple recipe retrieval
- unknown United Nations query terms
- small lunar-crater recall
- Yamamoto crater disambiguation

This is better evidence than simply counting tests. It shows the engineer is willing to represent unsolved behavior explicitly.

## Gap: missing interaction tests for retrieval constraints

The tag filter is tested in `tests/test_retrieve.py:62-71`, but there is no test that combines:

- tag filtering
- a query that activates a custom word
- lightning-rod retrieval

That gap likely explains why the bypass bug survives despite a large suite.

Likewise, the L2 floor behavior is not tested consistently across the two retrieval paths.

**Assessment: Strong testing maturity with some cross-feature gaps**

---

# 8. Maintainability

The codebase is easy to navigate.

Strong signals include:

- private module naming for internals
- a small public API
- explicit data models
- package structure documented in README
- clear method names
- design comments focused on reasoning
- configuration constants grouped near the behavior they influence
- SQL schema located with the storage implementation
- dedicated CLI rather than mixing argument parsing into domain functions

The README is unusually detailed, though parts of it are stale.

The stale Phase 2 status is a real maintainability issue because a reader could reasonably conclude the vocabulary extension does not exist.

Given this is a personal learning repo, I would weight that lightly. The code is considerably more current than the project-status prose.

**Assessment: Strong**

---

# 9. Operational Thinking

Shoal shows moderate operational awareness.

Examples:

- WAL mode enabled for SQLite
- foreign keys explicitly enabled
- content hashes stored
- document deletion uses cascades
- engine owns startup and shutdown
- custom vocabulary is rehydrated at startup
- status command exposes corpus counts and dependency version
- explain tooling surfaces semantic confidence and weak terms
- corpus-building scripts exist

This is not a production service, so there are no health probes, metrics or structured tracing.

The most important operational weakness is ingestion atomicity. A failed ingestion can leave partial persistent state.

**Assessment: Moderate**

---

# 10. Performance and Scalability

Performance reasoning is visible throughout the design.

## Corpus selectivity

`src/shoal/_storage.py:346-360` calculates smoothed per-reef IDF:

`log(1 + N / df)`

This downweights semantic reefs that appear in many chunks.

## Storage filtering

`src/shoal/_storage.py:364-481` stores only the top K reefs per chunk based on `z_score * IDF`.

This is both a performance and retrieval-quality decision. It reduces stored relationships while prioritizing distinctive semantic features.

Unknown reefs during insertion receive a boosted default IDF because they are assumed rarer than currently observed reefs.

## Query scoring

`src/shoal/_storage.py:485-554` performs overlap scoring in SQL rather than materializing the corpus into Python.

That moves aggregation and filtering to the database and prevents a full application-side scan.

## Result diversity

`src/shoal/_retrieve.py:33-50` caps results per document so very large documents cannot dominate the result set solely through chunk count.

This behavior was motivated by observed corpus failures in `RESULTS.md`.

## Concern: inconsistent L2 floor

`src/shoal/_storage.py:19-22` defines `_L2_NORM_FLOOR = 100.0` with a clear explanation: low-norm chunks can receive disproportionately high scores.

The lightning-rod scorer uses:

`MAX(c.reef_l2_norm, _L2_NORM_FLOOR)`

The standard `search_by_reef_overlap()` path at `src/shoal/_storage.py:525-527` divides directly by `c.reef_l2_norm`.

That means the exact pathology the constant was introduced to prevent can still occur in the standard path.

This looks like a change that was propagated to one scoring path but not the other.

**Assessment: Strong performance reasoning with one consistency defect**

---

# 11. External Dependencies and Build-vs-Buy Judgment

Shoal makes good dependency choices.

Lagoon owns semantic scoring and document topic-shift analysis.

SQLite owns relational persistence and query execution.

Shoal does not introduce:

- an ORM
- a vector database
- a web framework before the REST phase exists
- a task queue
- a generalized ETL framework

The project builds only the logic that is specific to its retrieval hypothesis.

This is particularly good because the engineer is experimenting with a nonstandard retrieval architecture. The custom part is the retrieval strategy, not infrastructure reinvention.

**Assessment: Strong**

---

# 12. Security and Defensive Engineering

Security is mostly out of scope for a local POC.

Positive evidence:

- SQL values are parameterized
- user-controlled tags are passed as parameters
- dynamic SQL fragments are created from internal counts and aliases rather than raw query strings
- SQLite foreign keys are enabled

The CLI operates on local files and a local database.

No authentication, authorization or secrets model is expected for this repository.

**Assessment: Appropriate to scope**

---

# 13. Git History and Evolution

The ZIP contains no Git history.

Therefore I cannot assess commit quality, refactor sequences or authorship through Git.

However, the repository does include `RESULTS.md` and `phase2_notes.txt`, which provide useful non-Git evidence of experimental evolution.

Those notes should not be treated as proof that every described change was authored by the evaluated engineer unless authorship is independently established. They do show how the repository's development process was being reasoned about.

**Git evidence level: Insufficient**

---

# 14. Evidence of Debugging Ability

Shoal provides unusually good non-Git evidence of debugging behavior.

`RESULTS.md` records failed retrieval queries and identifies three root causes:

1. large-document bias
2. vocabulary gaps
3. low query confidence

Those root causes then map to actual implementation mechanisms:

- result diversity limits
- vocabulary extension
- quality gating
- custom-word candidate retrieval
- reef IDF

`phase2_notes.txt` goes further. It defines a specific "Yamamoto" stress test because the name appears across several unrelated domains.

The notes predict expected failure behavior before testing, then record two experimental runs and compare outcomes.

Examples from the notes:

- custom word plus lightning-rod retrieval improved to 92% success
- base-vocabulary / reef-only retrieval remained weak
- total stress-test success improved from 39% to 61%
- "Yamamoto Japanese military" improved from failure to #1
- "Ichi Kakihara yakuza" changed from zero results to #1
- chunk deduplication reduced the corpus from 4,926 to 4,033 chunks
- remaining failures were attributed separately to Lagoon-level mapping issues

The important signal is not the absolute retrieval quality. It is the reasoning loop:

**observe → isolate hypothesis → modify mechanism → rerun targeted tests → compare outcomes → retain known limitations**

That is strong evidence of real debugging and experimental engineering.

**Assessment: Strong**

---

# 15. Evidence of Technical Leadership Through Code

Shoal makes future investigation easier.

Examples:

- `Engine` gives callers a narrow API
- `explain_query()` exposes semantic diagnostics rather than hiding them
- query metadata returns confidence and coverage
- README describes the semantic model
- test suites include known failures
- result-quality experiments are documented
- module boundaries are clear
- storage retains enough structured metadata to explain why a result matched

Interpretability is a recurring theme.

Rather than returning only an opaque relevance score, the system can show shared reefs, per-word confidence and query reef activation.

That kind of observability helps another engineer debug the retrieval system.

**Assessment: Strong Senior-level technical leadership signal**

---

# 16. Signs of Over-Engineering

Shoal avoids most common over-engineering patterns.

There is no dependency-injection framework, plugin architecture, ORM or excessive class hierarchy.

The architecture is richer than ConceptFor because the problem is richer.

The most speculative element is the pre-created Phase 2 schema and extensive design prose before all Phase 2 behavior was stable. However, the implementation has now largely caught up with that design.

The custom vocabulary system itself is complicated, but the complexity is motivated by an observed problem: rare domain terms are invisible to the base vocabulary.

The "lightning rod" candidate path is also justified by measured retrieval failures.

**Assessment: Mostly appropriate complexity**

---

# 17. AI-Assisted Development

There is no direct evidence that specific code was generated by AI.

The repository does not show the typical negative indicators that would matter for this evaluation:

- duplicated competing implementations
- incoherent naming
- abandoned generic wrappers
- unexplained framework layers
- large unused utility surfaces
- contradictory domain models

The strongest evidence of authorial control is the linkage between observed retrieval behavior, documented hypotheses, algorithm changes and tests.

If AI tools contributed implementation code, the repository still appears to be under coherent technical control.

**Assessment: No material negative signal**

---

# 18. Complexity Hotspots

## Hotspot 1: Hierarchical Markdown parsing

**Location:** `src/shoal/_parsers.py:172-457`

**Problem:** Real documents have H1-H6 structures, short subsections, boilerplate and content that should be semantically analyzed at useful granularity.

**Approach:** Build a flat section list carrying parent indices, fold short H3 sections into H2 parents, always fold H4+ content and skip known boilerplate sections.

**Tradeoff:** Heuristics are corpus-specific but preserve useful structure without requiring a full Markdown AST dependency.

**Assessment:** Good practical decomposition and corpus-aware reasoning.

---

## Hotspot 2: Duplicate-safe chunk offset reconstruction

**Location:** `src/shoal/_ingest.py:390-428`

**Problem:** Lagoon returns sentence text segments, while Shoal stores absolute source character positions. Repeated sentences can make simple `str.find()` incorrect.

**Approach:** Maintain a forward cursor while finding each segment's sentences, so repeated text resolves after prior occurrences.

**Tradeoff:** Fallback offset estimation is approximate when normalized sentence text cannot be found exactly.

**Assessment:** Good attention to an implementation detail that is easy to overlook.

---

## Hotspot 3: Two-pass vocabulary extension

**Location:** `src/shoal/_ingest.py:105-182`

**Problem:** Unknown domain terms cannot affect Lagoon's first-pass semantic scoring.

**Approach:** Discover unknown terms, infer reef associations, inject vocabulary and rerun analysis only if vocabulary changed.

**Tradeoff:** Additional analysis cost and mutable runtime scorer state in exchange for improved domain coverage.

**Assessment:** Strong Senior-level implementation.

---

## Hotspot 4: Confidence-weighted context learning

**Location:** `src/shoal/_vocab.py:66-138`

**Problem:** Context for an unknown term may be more trustworthy at sentence level or chunk level depending on sentence signal quality.

**Approach:** Blend both contexts and shift the weights based on sentence confidence.

**Tradeoff:** Hand-tuned thresholds and weights rather than statistically learned calibration.

**Assessment:** Sound experimental engineering for a POC.

---

## Hotspot 5: Reef-size-adjusted vocabulary association

**Location:** `src/shoal/_vocab.py:178-252`

**Problem:** Large generic reefs may dominate learned unknown-word associations.

**Approach:** Scale mean z-scores inversely by reef word count with a capped boost for small reefs, then apply absolute and relative filtering.

**Tradeoff:** Heuristic calibration but directly addresses an observed semantic imbalance.

**Assessment:** Strong reasoning about feature informativeness.

---

## Hotspot 6: Selectivity-aware chunk storage

**Location:** `src/shoal/_storage.py:346-481`

**Problem:** Storing every activated reef increases storage and lets ubiquitous reefs dominate overlap.

**Approach:** Calculate corpus IDF and keep only the top K reefs ranked by z-score × IDF.

**Tradeoff:** The stored representation depends on corpus state at ingestion time.

**Assessment:** Strong idea with an important evolutionary consequence to probe.

---

## Hotspot 7: SQL reef-overlap retrieval

**Location:** `src/shoal/_storage.py:485-587`

**Problem:** Rank chunks using structured semantic features without vector search.

**Approach:** Join query reef values to `chunk_reefs`, compute an IDF-weighted overlap score, reward multiple shared reefs and normalize by chunk reef norm.

**Tradeoff:** Hand-designed relevance function requiring corpus-specific tuning.

**Assessment:** Strong implementation depth.

---

## Hotspot 8: Lightning-rod custom-word retrieval

**Location:** `src/shoal/_retrieve.py:96-193`

**Problem:** Rare custom terms provide high-precision lexical evidence that broad reef semantics may dilute.

**Approach:** Retrieve chunks tagged with matching custom vocabulary, score them semantically, boost based on term frequency and document concentration, then merge with standard candidates.

**Tradeoff:** Two retrieval paths create consistency risks. The current tag/min-confidence bypass is an example.

**Assessment:** Strong concept, current integration bug.

---

## Hotspot 9: Result diversity

**Location:** `src/shoal/_retrieve.py:33-50`, `167-201`

**Problem:** Large documents have more opportunities to produce high-ranked chunks.

**Approach:** Over-fetch candidates and apply a per-document result cap.

**Tradeoff:** Can suppress legitimately dense relevant documents.

**Assessment:** Appropriate response to measured corpus behavior.

---

## Hotspot 10: Retrieval quality experiments

**Location:** `tests/test_retrieval_quality.py`, `RESULTS.md`, `phase2_notes.txt`

**Problem:** Unit correctness cannot establish search quality.

**Approach:** Define ambiguous query sets, positive targets, negative constraints, known failures and explicit stress scenarios.

**Tradeoff:** The benchmark corpus is still a development set rather than an unbiased evaluation set.

**Assessment:** Strong experimental discipline for a personal project.

---

# 19. Strongest Senior+ Signals

## 1. The difficult behavior is implemented

This is not architecture around shallow wrappers.

The vocabulary-learning system, corpus-selectivity logic, SQL scorer, parser heuristics and custom-word retrieval path contain real behavior.

## 2. Retrieval failure is treated as an engineering problem

The repository identifies semantic failures, forms hypotheses and changes mechanisms to address them.

The Phase 2 stress notes are particularly compelling evidence.

## 3. Strong cross-layer reasoning

The engineer moves across:

- text parsing
- semantic scoring
- relational modeling
- SQL aggregation
- runtime vocabulary mutation
- corpus statistics
- API behavior
- test design

That breadth is characteristic of Senior-level work.

## 4. Interpretability is designed in

Search exposes shared reefs, confidence, coverage and per-word explanations.

This suggests the engineer expects the system to require diagnosis and creates tools to make that possible.

## 5. Tests include behavior, not just implementation units

There are negative constraints, known failures, ranking-quality checks and result-diversity tests.

That indicates concern for what the system actually does.

---

# 20. Strongest Concerns

## 1. Lightning-rod results bypass query filters

**Location:** `_retrieve.py:120-193`

`tags` and `min_confidence` are only passed to the standard retrieval path.

This can violate explicit caller constraints.

**Strength of concern:** Moderate

## 2. L2 normalization floor is inconsistent

**Location:** `_storage.py:19-22`, standard scorer around `525-527`, custom-word scorer around `758+`

The code documents a floor to prevent low-norm chunks from being over-rewarded, but only one retrieval path applies it.

**Strength of concern:** Moderate

## 3. Ingestion is not transactionally atomic

A failure after document insertion can leave partially ingested records.

**Strength of concern:** Low to moderate in POC context

## 4. Corpus-dependent top-K reef persistence can become stale

Chunks are filtered using IDF computed from the corpus as it existed when each chunk was inserted.

As the corpus grows, an old chunk's stored top 38 reefs may no longer be the top 38 under current corpus IDF.

This means retrieval representation is path-dependent on ingestion order.

That may be acceptable experimentally, but it is a deeper design question worth probing.

**Strength of concern:** Moderate

## 5. Documentation lags implementation

The README calls Phase 2 unimplemented although substantial Phase 2 functionality and tests exist.

**Strength of concern:** Low for leveling

---

# 21. Rust vs. Loss of Hands-On Depth

## Hypothesis A: Rusty Senior Engineer

### Strong supporting evidence

- clear decomposition with implemented behavior
- nontrivial Python and SQL
- semantic data modeling
- confidence-aware algorithms
- two-pass ingestion
- runtime vocabulary extension
- corpus-level selectivity logic
- retrieval quality experimentation
- 208 tests
- known failures represented explicitly
- documented debugging hypotheses and measured iterations

The repository shows the engineer repeatedly moving from conceptual problem to executable mechanism.

### Contradicting evidence

- there are integration bugs across retrieval paths
- the README is stale
- ingestion failure semantics are incomplete
- some scoring rules are heuristic and inconsistently propagated
- full end-to-end tests could not be independently run from this ZIP without Lagoon

Those concerns are consistent with an actively evolving personal experiment.

## Hypothesis B: Architecture/Management Strength Without Current Senior IC Depth

### Supporting evidence

The strongest argument would be that some of the most interesting semantic behavior originates in Lagoon rather than Shoal.

Shoal does rely on Lagoon for core text scoring and topic segmentation.

### Contradicting evidence

Shoal itself contains substantial implementation depth that Lagoon does not provide:

- document parsing
- section hierarchy
- persistence model
- corpus-level IDF
- reef selection
- learned vocabulary orchestration
- custom-term persistence
- lightning-rod retrieval
- result diversity
- search diagnostics
- retrieval-quality testing

The architecture is therefore not hiding the hard details.

### Conclusion

**The evidence strongly favors Hypothesis A: rusty Senior Engineer.**

---

# 22. Evidence Summary

| Dimension | Evidence Level | Key Evidence |
|---|---|---|
| Architecture | Strong | Clean parser, ingestion, vocabulary, storage, retrieval and engine boundaries |
| System decomposition | Strong | Responsibilities align to real problem boundaries |
| Implementation fluency | Strong | Substantial Python and SQL implemented coherently |
| Technical depth | Strong | Learned vocabulary, retrieval scoring and corpus statistics |
| Debugging/root-cause reasoning | Strong | RESULTS.md and Phase 2 stress-test iterations |
| Error/failure reasoning | Moderate | Semantic quality gates strong, transactional ingestion weaker |
| Data/correctness reasoning | Strong | Runtime vs persistent identity, confidence, coverage and semantic metadata |
| Testing maturity | Strong | 208 tests, 78 independently executable here, explicit xfails |
| Operational thinking | Moderate | WAL, lifecycle, diagnostics and status; no atomic ingestion |
| Performance/scalability | Strong | SQL scoring, top-K reef filtering, corpus IDF and over-fetch/diversity |
| Maintainability | Strong | Good boundaries and documentation, though status prose is stale |
| Engineering judgment | Strong | Purposeful heuristics and minimal infrastructure dependencies |
| Technical leadership | Strong | Explainability, clear API and diagnostic artifacts |
| Ability to work independently | Strong | End-to-end retrieval system around Lagoon |

No overall numeric score is assigned.

---

# 23. Final Assessment

## What level of hands-on engineering does this repository demonstrate?

Shoal demonstrates **strong current Senior Software Engineer hands-on capability**.

The repository is more than a Lagoon wrapper. It builds an independent retrieval architecture around Lagoon and implements the difficult integration behavior itself.

The code shows comfort with Python, SQL, data modeling, text structure, semantic relevance, corpus statistics and testing.

## What are the strongest Senior Engineer signals?

1. **Two-pass custom vocabulary system** with context-weighted learning and runtime injection.
2. **Custom retrieval architecture** implemented in SQL and Python rather than delegated to a vector database.
3. **Iterative debugging evidence** connecting observed quality failures to specific engineering changes.
4. **Strong behavioral test strategy**, including negative constraints and explicit known failures.
5. **Cross-layer execution**, from parsers through storage to retrieval diagnostics.

## What are the biggest concerns?

1. Custom-word retrieval can bypass tag and minimum-confidence filters.
2. Standard retrieval does not apply the L2 norm floor used by the alternate scoring path.
3. Corpus-dependent reef selection can make stored chunk representations depend on ingestion order.
4. Document ingestion is not atomic.
5. README implementation status is stale.

## Does the implementation support the "coding rust" hypothesis?

**Yes, strongly.**

There is no convincing evidence here of someone who retained architecture vocabulary while losing Senior-level implementation ability.

The repo contains too much concrete low-level work, algorithmic experimentation and debugging structure for that conclusion.

The surviving defects are primarily integration-consistency issues in an evolving experimental system. They do not look like inability to implement difficult concepts.

## What questions remain unanswered?

This repository cannot establish:

- production incident behavior
- collaboration in a multi-engineer codebase
- code review quality
- authorship without Git history
- long-term maintainability under multiple contributors
- large-scale concurrency
- distributed systems depth
- production security judgment
- whether the engineer can produce the same quality under interview time pressure

## What should a system-design or technical interviewer probe?

1. **Filter correctness:** Why can lightning-rod results bypass `tags` and `min_confidence`? Where should those constraints live so every retrieval strategy obeys them?
2. **Scoring consistency:** Why is `_L2_NORM_FLOOR` applied in `score_chunks_by_reef_overlap()` but not `search_by_reef_overlap()`? What failure behavior does the floor address?
3. **Corpus evolution:** Stored reefs are selected using corpus IDF at ingestion time. What happens after the corpus changes substantially? Would he periodically reindex?
4. **Atomic ingestion:** How would he prevent a failed Lagoon analysis from leaving a half-ingested document?
5. **Vocabulary poisoning:** How should the system stop a repeated rare word in one bad document from becoming a misleading custom semantic feature?
6. **Polysemy:** The learned custom-word representation is one reef profile per word. How would he model a term with multiple genuine meanings?
7. **Benchmark design:** How would he create a holdout evaluation set that is not repeatedly tuned against during retrieval development?
8. **Retrieval fusion:** Why use a multiplicative lightning-rod boost? What would make him adopt BM25 lexical scoring, reciprocal-rank fusion or another hybrid method?
9. **SQLite scaling:** At what corpus size or query concurrency would he move beyond SQLite and what part of the design changes first?
10. **Lagoon boundary:** Which retrieval failures belong in Shoal and which belong in Lagoon? How does he decide where a fix should live?

Questions 1, 2, 3 and 5 would be especially diagnostic. They test whether the current gaps are known consequences of experimentation or unrecognized system-level invariants.

---

# Bottom Line

Shoal is **strong leveling evidence**.

Relative to the earlier repositories, it adds something especially valuable: evidence of **debugging and iterative experimental reasoning**. Lagoon showed clean implementation strength. Windowsill showed broad systems and ML reasoning. Shoal shows an engineer building on an existing subsystem, discovering real quality failures and adding increasingly targeted mechanisms to address them.

That combination is much more consistent with a Senior engineer whose immediate coding fluency may be rusty than with a former hands-on engineer whose present value is mainly architectural or managerial.
