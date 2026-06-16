# REPORT — corpus Runbook Automation Self-Hosted 5.20.1

- Versione verificata sul sito: **5.20.1** (link Release Notes in homepage -> version-5.20.1.html; ultima release nello storico 5_x)
- Data fetch: 2026-06-12
- Pagine convertite: **489**
- URL falliti: **2**
- Dimensione totale: 3,347,373 byte (3.2 MiB)
- Caratteri totali: 3,342,989
- Stima token (chars/4): **~835,747** — impatto sulla capacita' del Project

## File per sezione

| Sezione | File | Caratteri |
|---|---:|---:|
| about | 4 | 9,897 |
| administration | 99 | 817,533 |
| api | 4 | 302,651 |
| history | 2 | 8,422 |
| learning | 135 | 806,998 |
| manual | 222 | 1,293,517 |
| rd-cli | 10 | 47,936 |
| upgrading | 13 | 56,035 |

## Sezioni escluse (per scope self-hosted)

- `/docs/about/cloud/**` — SaaS cloud, NON self-hosted
- `/docs/history/**` — tranne release notes 5.20.x (incluse: 5.20.0, 5.20.1)
- `/docs/about/*` non in whitelist (introduction/enterprise/licensing/getting-help)
- `/docs/learning/tutorial*` e altro learning fuori da getting-started/howto/solutions
- qualsiasi URL fuori da `/docs/`

## URL falliti

- https://docs.rundeck.com/docs/api/api-index-links.html — pagina renderizzata solo client-side (widget JS), nessun contenuto statico catturabile — esclusa
- https://docs.rundeck.com/docs/api/openapi-explorer.html — pagina renderizzata solo client-side (widget JS), nessun contenuto statico catturabile — esclusa

## QA

- Errori QA: 0
- Eccezioni documentate (corpo < 200 caratteri ma pagine reali, verificate manualmente: avvisi di deprecazione, redirect, puntatori):
  - `about/licensing.md`
  - `administration/cluster/loadbalancer/aws-elb.md`
  - `administration/install/tomcat.md`
  - `api/api-spec.md`
  - `manual/command-line-tools/index.md`
  - `manual/command-line-tools/rd-acl.md`
  - `manual/command-line-tools/rd.md`
  - `manual/old-docs.md`
  - `manual/projects/scm/job-replication.md`
