# Runbook Automation Self-Hosted 5.20.1 — Docs Corpus

Corpus Markdown pulito e version-pinned della documentazione di **PagerDuty Runbook
Automation SELF-HOSTED v5.20.1**, estratto da [docs.rundeck.com](https://docs.rundeck.com)
il 2026-06-12. Destinato alla knowledge base di un Claude Project (PoC interno,
nessuna redistribuzione).

- **489 pagine** (~3,2 MiB, stima ~836k token), albero che rispecchia il sito.
- Ogni file ha front-matter YAML: `title`, `source_url` canonica, `product`,
  `version: 5.20.1`, `fetched`.
- Link interni riscritti come URL assolute `https://docs.rundeck.com/...`.
- Scope: solo self-hosted (`manual/`, `administration/`, `api/`, `rd-cli/`,
  `upgrading/`, `about/` selezionato, `learning/`, release notes 5.20.x).
  Escluso il SaaS cloud (`about/cloud/`) e lo storico versioni precedenti.

File chiave:

- [`_SOURCE_OF_TRUTH.md`](./_SOURCE_OF_TRUTH.md) — regola di astensione anti-allucinazione
  (da copiare anche nelle *Project instructions* di Claude).
- [`INDEX.md`](./INDEX.md) — tabella file → sezione → titolo → source_url.
- [`REPORT.md`](./REPORT.md) — audit: conteggi, dimensioni, esclusioni, QA.
