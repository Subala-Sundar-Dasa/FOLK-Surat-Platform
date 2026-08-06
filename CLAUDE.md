# Claude Code operating instructions

Read `README.md`, `docs/CURRENT_STATUS.md`, `docs/DECISIONS.md`, `docs/ARCHITECTURE.md`, and `planning/backlog.yaml` before editing code.

## Non-negotiable boundaries

- Never merge into any `main` branch without explicit user approval.
- Never deploy publicly, message real students, connect production systems, upload the corpus externally, or use paid APIs without separate approval.
- Use only synthetic test data. Never commit secrets, OAuth credentials, service-role keys, student data, signing keys, or local `.env` files.
- Preserve the existing daily sadhana workflows in both mobile apps; improve them incrementally.
- Google is the only user sign-in method.
- Supabase is the canonical application database. Trello is an operational task projection, not the student system of record.
- FOLK guides make practical and pastoral judgments. AI summarizes evidence and recommends actions; it does not replace the guide.
- Prabhupada-grounded messages must distinguish quotation from paraphrase and include traceable corpus references.
- Student-facing guidance must never expose LIT scores, mentor assessments, confidence values, or internal prioritization.
- Keep FOLK HOD informed. Foundational goals and quarterly-target changes require HOD approval.

## Engineering workflow

Work on `codex/*` or another feature branch. Keep changes small and testable. Update `docs/CURRENT_STATUS.md`, `planning/feature-status.yaml`, and `docs/CHANGELOG.md` with every meaningful handoff. Record architectural decisions in `docs/DECISIONS.md`. Create migrations for schema changes and test RLS with student, assigned-guide, unassigned-guide, and HOD roles.

## First task

Resume the Google OAuth mobile flow and verify student entry -> Supabase persistence -> assigned-guide visibility. See `docs/NEXT_AI_START_HERE.md`.

