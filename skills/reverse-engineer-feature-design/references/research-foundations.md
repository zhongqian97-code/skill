# Research foundations

These sources inform the workflow; they are not evidence for the target repository.

- SEI Software Architecture Reconstruction: facts → views → fusion → iterative validation: https://resources.sei.cmu.edu/asset_files/TechnicalReport/2002_005_001_14016.pdf
- Reflexion Models: compare hypothesized architecture with the source model using convergence, divergence, and absence: https://doi.org/10.1109/32.910501
- Feature location survey: combine textual, static, dynamic, and historical techniques: https://doi.org/10.1002/smr.567
- Program slicing and dynamic slicing: https://doi.org/10.1109/TSE.1984.5010248 and https://doi.org/10.1016/0020-0190(88)90054-3
- W3C PROV provenance model: https://www.w3.org/TR/prov-overview/
- CodeQL data-flow limits and semantics: https://codeql.github.com/docs/writing-codeql-queries/about-data-flow-analysis/
- Sourcegraph code navigation and SCIP: https://sourcegraph.com/docs/code-search/code-navigation and https://github.com/sourcegraph/scip
- GitHub code navigation and permanent links: https://docs.github.com/en/repositories/working-with-files/using-files/navigating-code-on-github and https://docs.github.com/en/repositories/working-with-files/using-files/getting-permanent-links-to-files
- Git history tools: https://git-scm.com/docs/git-log and https://git-scm.com/docs/git-blame
- Clang compilation database and source coverage: https://clang.llvm.org/docs/JSONCompilationDatabase.html and https://clang.llvm.org/docs/SourceBasedCodeCoverage.html
- C4 and Structurizr DSL: https://c4model.com/ and https://docs.structurizr.com/dsl
- RepoAgent and Aider repository maps: https://github.com/OpenBMB/RepoAgent and https://aider.chat/docs/repomap.html
- Characterization tests: https://martinfowler.com/bliki/CharacterizationTest.html
- Git clone/submodules and GitHub licensing: https://git-scm.com/docs/git-clone, https://git-scm.com/docs/git-submodule, and https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository
- Codex and Claude Code repository/security guidance: https://learn.chatgpt.com/docs/agent-configuration/agents-md, https://learn.chatgpt.com/docs/sandboxing, https://code.claude.com/docs/en/memory, and https://code.claude.com/docs/en/security

Borrowed design choices:

- deterministic symbol and evidence inventory before synthesis;
- feature-first slices rather than repository-wide summaries;
- observed model vs hypothesized intent vs gap;
- layered C4 plus dynamic/state/data views;
- immutable provenance and replayable evidence;
- incremental re-analysis by changed files/symbols.

Do not copy the failure modes of generated wikis and API-documentation tools: fluent unsupported intent, file-list narratives, happy-path-only coverage, mutable-branch citations, or diagrams treated as proof.