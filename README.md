# Smithers

A minimal, safe, and genuinely collaborative mathematical research assistant. Smithers will help you be the best Mr. Burns version of your mathematical self...

## Start here

1. Copy this folder for a new project, or publish it on GitHub and mark it as a template repository.
2. Fill in `CONFIG.md`, then record the research question and priority sources in `context/context.md`.
3. Add shared definitions to `definitions.tex`. Copy `templates/result.tex` into the appropriate results folder and replace its placeholders.
4. Keep the repository as the durable record. At the end of a chat, save mathematical changes and update `context/context.md`.

```text
CONFIG.md                         Project choices and collaboration instructions
definitions.tex                   Shared mathematical definitions and notation
main.tex                          Assemble selected results into a draft
preamble.tex                      Shared LaTeX packages, environments, and macros
context/
  context.md                      Current state, source relevance, next steps
  references.bib                  Bibliography with stable citation keys
  sources/                       Sources suitable for version control
  private/                       Local sources and notes, ignored by Git
results/
  01-ideas/                      Formal directions and proposed statements
  02-conjectures/                 Precise claims and proof strategies
  03-lemmas-and-proofs/           Proof development and review
  04-understandable/             Reviewed exposition ready for a paper
code/                            Computations; choose tools as the project grows
templates/result.tex             Reusable LaTeX fragment and provenance record
scratch/                         Local experiments, ignored by Git
```

Git does not preserve empty directories: create `context/private/` and `scratch/` locally when needed. Their ignore rules are already present.

## The research filtration

| Stage | Required mathematical content | Ready to advance when |
| --- | --- | --- |
| Ideas | Objects, tentative hypotheses, proposed statement, and a concrete direction or proof sketch | The claim can be stated precisely and its open assumptions identified |
| Conjectures | Quantifiers, exact hypotheses, dependencies, examples or counterexample searches, and a proof strategy | A candidate proof can be developed and checked step by step |
| Lemmas & proofs | Explicit statements, detailed arguments, citations, and named remaining gaps | The proof and all dependencies have been checked by a named human reviewer |
| Understandable | Clear, formal, paper-ready exposition with complete proofs and consistent definitions | Suitable for inclusion in a manuscript; substantive edits require renewed review |

These are stages of refinement, not measures of confidence. A polished argument may still be wrong. Here, “formal” means precise mathematical writing; machine verification is optional and must be recorded separately if used. An explicitly identified open conjecture may appear in a paper, but must never be presented as proved.

Use one canonical file per result, for example `R-alice-001-compactness.tex`. Keep its ID and LaTeX labels stable when moving it between folders with `git mv`. Git retains earlier versions; avoid four diverging copies. New branches of an idea get new IDs and list their origin in `derived-from`. Rejected or refuted claims remain at their current stage with their status and counterexample recorded. A result can move backwards when a gap is found.

Use globally unique labels, such as `res:alice-001` and `def:compactness`. List result IDs, definition labels, and bibliography keys in each file's comment header. In the mathematical text, cite precise source locations, for example `\cite[Theorem 2.3]{source-key}`. Do not leave citations or hypotheses implicit.

When a definition changes, search for its label and notation, recheck dependent results, and reset affected review records. Keep the result index in `context/context.md` current. If a source definition differs from ours, record the translation there.

## LaTeX and paper assembly

Each result is a `.tex` fragment without `\documentclass` or `\begin{document}`. Use standard theorem environments and ordinary LaTeX so sections can move into a journal template. Metadata stays in `%` comments and does not appear in the paper.

`definitions.tex` contains mathematical content; `preamble.tex` contains macros and environment declarations. `main.tex` includes both, and is the only compilation entry point. Add explicit `\input{results/.../file.tex}` lines in dependency order. Include each result once. For a research draft, select any stage and keep visible gap/status notices. For a paper, select reviewed material from `04-understandable` and include any necessary reviewed prerequisites.

Compile **from the repository root**:

```sh
pdflatex -interaction=nonstopmode -halt-on-error main.tex
pdflatex -interaction=nonstopmode -halt-on-error main.tex
```

Once you add citations, enable the two bibliography lines in `main.tex` and run `pdflatex main.tex`, `bibtex main`, then `pdflatex main.tex` twice. The starter uses the standard `amsmath`, `amssymb`, `amsthm`, and `hyperref` packages. A successful build checks typesetting, not mathematical correctness.

## Work with any chat or assistant

Start with the chat subscription you already use. This repository makes no API calls and does not require an API subscription. Product access and usage limits still depend on your account; no particular plan is assumed.

**Recommended workflow:** keep a local Git checkout and open that folder in an app that supports reading and editing local project files. If your app only accepts uploads or repository context, give it `CONFIG.md`, `context/context.md`, `definitions.tex`, `preamble.tex`, and the relevant result/source files. Request changes by file path, then save and review them locally. Uploads are snapshots; refresh them after edits. A repository connection should not be assumed to provide write-back.

Paste this at the beginning of a chat or into project instructions:

> Read CONFIG.md, context/context.md, definitions.tex, and the relevant result files before working. Follow the project conventions and use the repository as the durable record. Say which files you can actually access and identify missing dependencies. Write mathematical results as LaTeX fragments with stable IDs, explicit hypotheses, and honest proof status. Preserve contributor/model history and record the model identifier only when known; otherwise use unknown. Never infer human review. At the end, update the affected files and context/context.md; if you cannot edit files, return complete replacements or a patch with exact relative paths.

`CONFIG.md` is an explicit entry point, not a universally auto-loaded filename. No `CLAUDE.md` is required. An app-specific instruction file can later point to `CONFIG.md` without duplicating its content.

Integration references, checked 2026-09-27:

- [ChatGPT local projects](https://learn.chatgpt.com/docs/projects) can provide access to attached folders; a ChatGPT project by itself does not give access to a local checkout.
- [ChatGPT desktop quickstart](https://learn.chatgpt.com/docs/quickstart) explains account sign-in and opening folders. Available capabilities vary by account and environment.
- [Claude GitHub integration](https://support.claude.com/en/articles/10167454-use-the-github-integration) supports selecting repository files for chat/project context and manually refreshing them. Refresh before a session; its synced context does not include commit history.

Keep attribution inside result files, so it travels even when a chat cannot see Git history. Record each substantive contribution with date, human contributor or operator, service/app, model as reported, role, and affected portion. Use `none` for human-only work and `unknown` when model identity is unavailable. Attribution is a record of assistance, not proof review or a claim of authorship.

## Git, collaboration, and portability

Use relative paths, UTF-8 text, and small files. There are no symlinks, submodules, or external framework folders. Create language environments only when needed and document reproduction commands in `code/README.md`.

For a new copy without Git history:

```sh
git init -b main
git add .
git diff --cached
git commit -m "Start mathematical project"
```

Create an empty GitHub repository, then substitute its URL:

```sh
git remote add origin https://github.com/YOUR-ACCOUNT/YOUR-PROJECT.git
git push -u origin main
```

For ongoing work, start from a clean working tree and run `git pull --ff-only`. Commit or stash local edits before pulling. Collaborators can use `git switch -c research/short-topic`, commit related changes together, and push the branch for review. Coordinate result IDs using contributor prefixes. Resolve competing changes to definitions explicitly and record the decision in `context/context.md`. Do not have multiple assistants edit the same checkout concurrently without coordination.

The `.gitignore` excludes private sources, scratch files, local environments, generated computational outputs, and LaTeX build files. Shared source PDFs are allowed in `context/sources/`; the generated root `main.pdf` is ignored. Add project-specific exclusions as needed. Ignoring a previously tracked file does not untrack it. Gitignore also does not prevent a local assistant from reading a file: configure access separately.

Cloning or pulling transfers tracked files only. Transfer needed private sources separately, and leave a source identifier and acquisition note in the shared context when appropriate. A fresh project should choose its own sharing license; no third-party source licenses are changed by this template.

## Credit

Inspired by **Yan He (GitHub: dazhima)** and [math-ai-framework](https://github.com/dazhima/math-ai-framework), especially its emphasis on modular mathematical work, explicit dependencies, and human–AI collaboration. This is a newly written, independent template tailored to a four-stage research filtration; it does not bundle the original framework's files. Please retain this acknowledgement when reusing the template.
