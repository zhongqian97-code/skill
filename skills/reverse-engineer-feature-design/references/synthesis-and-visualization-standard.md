# Synthesis and Visualization Standard

## Editorial integrity

The formal deliverable is one Markdown document with one H1, one status block, one vocabulary, and one continuous hierarchy. Multiple agents may collect evidence but cannot author final independent chapters. The integrator rewrites all accepted FeaturePackets.

Hard-splice indicators include multiple H1s, repeated introductions/conclusions, numbering restarting, duplicated API/table definitions, contradictory names, or embedded standalone review reports.

## Visual closure

- one early system summary diagram;
- one primary Mermaid behavior diagram per F-ID;
- triggered sequence/state/flow/ER/deployment views;
- every diagram has purpose, text alternative, guided reading, stable D-ID, and traceability;
- every key node/edge resolves to a contract, module, state, DB object, or evidence coordinate;
- diagrams and normative tables must agree.

## Dual-reader usability

The first 20% must establish scope, vocabulary, system shape, core lifecycle, and the feature map. Detail follows progressive disclosure.

A learner can follow a guided flow without source knowledge. An implementer can jump from any F-ID to API/event, backend, DB, failure, test, and source evidence within two navigational jumps.

## Multi-agent synthesis

Freeze scope, F/BEH IDs, glossary, outline, evidence format, and diagram conventions before delegation. Delegate vertical feature slices plus cross-cutting audits. Accept only structured packets. Resolve conflicts centrally. Rewrite once, then run terminology, duplicate-fact, cross-reference, Mermaid, evidence, and dual-reader checks.

## Research foundations

- C4 diagrams and abstraction: https://c4model.com/diagrams
- arc42 building block/runtime/glossary: https://docs.arc42.org/section-5/ , https://docs.arc42.org/section-6/ , https://docs.arc42.org/section-12/
- Google large documents, audiences, editing, illustrations: https://developers.google.com/tech-writing/two/large-docs , https://developers.google.com/tech-writing/one/audience , https://developers.google.com/tech-writing/two/editing , https://developers.google.com/tech-writing/two/illustrations
- Diátaxis: https://diataxis.fr/
- Mermaid sequence/state/ER and accessibility: https://mermaid.js.org/syntax/sequenceDiagram.html , https://mermaid.js.org/syntax/stateDiagram.html , https://mermaid.js.org/syntax/entityRelationshipDiagram.html , https://mermaid.js.org/config/accessibility.html
- Docs as Code: https://www.writethedocs.org/guide/docs-as-code/