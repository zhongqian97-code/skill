# Research Sources

The review standard is grounded in executable contracts and reproducible implementation artifacts.

- PostgreSQL — Constraints: primary, foreign, unique, check, nullability, and other constraints encode data invariants. https://www.postgresql.org/docs/current/ddl-constraints.html
- PostgreSQL — pg_dump: schema-only and related dump behavior demonstrate that database structure must be reproducibly extractable/buildable. https://www.postgresql.org/docs/current/app-pgdump.html
- OpenAPI Specification: machine-readable HTTP interface descriptions allow consumers to understand contracts without source access. https://spec.openapis.org/oas/latest.html
- AsyncAPI Specification: machine-readable message-driven operations, channels, directions, and payloads. https://www.asyncapi.com/docs/reference/specification/latest
- C4 Model: context, container, component, code, dynamic, and deployment views serve different implementation questions. https://c4model.com/diagrams
- DBML: tables, columns, defaults, checks, indexes, and relationships map to database schema/SQL. https://dbml.dbdiagram.io/docs/
- SchemaSpy: database metadata can generate browsable object and relationship documentation, reinforcing physical-schema inventory. https://schemaspy.org/
- NASA software design guidance cited in Wayfinder #4: low-level units should be sufficiently specified to code, compile, and test.
- Repository Wayfinder research: issues #1–#17 in https://github.com/zhongqian97-code/skill/issues
