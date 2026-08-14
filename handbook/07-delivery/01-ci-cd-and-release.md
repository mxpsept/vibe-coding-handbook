# Stage 07 — CI/CD & Release

Pipeline: `PR → static checks → tests → architecture/security checks → build immutable artifact → staging → smoke/E2E → approval policy → production → health verification`.

Build once and promote the same artifact. Version/review migrations. Externalize secrets. Keep rollback/roll-forward strategy and release evidence. AI may generate pipeline/config changes, but privileged deployment, secret changes and destructive migrations require explicit controls and review.

Release notes record behavior, migrations, configuration, known issues and rollback notes.