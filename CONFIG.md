# CONFIG — project template

Complete the bracketed fields as the project develops. This file is the shared entry point for humans and assistants of any provider. It is documentation, not executable configuration.

## Project

- Title: [Project title]
- Research question: [Precise problem or target theorem]
- Scope and exclusions: [What belongs here; what does not]
- Intended output: [Paper, collection of results, or other deliverable]
- Contributors and ID prefixes: [Name — prefix — role]
- Human reviewer(s): [Names; unassigned until filled]

## Mathematical conventions

- Field and ambient setting: [Objects, category, base field, regularity, etc.]
- Standing assumptions: [State explicitly; mathematical version in definitions.tex]
- Notation preferences: [Conventions and conflicts to avoid]
- Proof standard: [Default: complete written proofs; gaps explicitly labelled]
- Source priorities: [Keys listed in context/context.md and references.bib]
- Citation style: [Default: precise theorem/page references using BibTeX]

## Working preferences

- Current focus: [Result ID or research direction]
- Desired initiative: [Suggest directions / develop an agreed claim / other]
- Exposition: [Default: concise, rigorous, suitable for eventual publication]
- Computation tools: [Undecided; add only when needed]
- Allowed external research/tools: [Project preference]
- Restricted files or sources: [Paths and sharing restrictions]
- Local compilation command: [Default: see README.md]

## Shared working rules

1. Begin with this file, `context/context.md`, `definitions.tex`, and the relevant dependencies. Do not claim access to unavailable files or sources.
2. Write mathematics in `.tex` files. Use `templates/result.tex` as a starting point and adapt its sections to the result. Keep hypotheses, statements, proof status, and dependencies explicit at every stage.
3. Use the four result folders as a refinement process. Preserve stable IDs and labels when moving a result; keep one canonical version. Update the context index and `main.tex` input paths after a move.
4. Record reusable definitions in `definitions.tex` and macros in `preamble.tex`. Audit dependent claims when either changes; never silently strengthen assumptions to rescue a proof.
5. Distinguish proven statements, conjectures, conditional arguments, and computational evidence. Mark gaps locally. Never invent a citation or present numerical tests as a general proof.
6. Preserve the provenance header and append substantive contributions. Record humans and each model separately; use the reported identifier or `unknown`. Model identity and confidence are not verification.
7. Human review is recorded only after that review occurs. Moving into `04-understandable` requires a complete argument, checked dependencies/citations, and explicit human review. Substantive edits reset review status.
8. End a session by updating current state, source relevance, blockers, and next steps in `context/context.md`. Keep it concise; Git history holds the full chronology.
9. Use relative paths and ordinary files. Choose providers, programming languages, and paper formats per project; do not introduce them as framework requirements.
10. Use $$...$$ instead of \[...\], and $...$ instead of \(...\) for latex.
11. Use Australian English grammar, and avoid writing in an AI-like fashion.

## Project-specific exceptions

[Record deliberate changes to these defaults and why.]
