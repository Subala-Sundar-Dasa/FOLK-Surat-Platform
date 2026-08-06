# Trello integration

Supabase remains canonical. Trello is a human-friendly action board for follow-ups, events, preparation, approvals, and overdue work.

## Suggested lists

Inbox, This Week, Today, Waiting for Student, Waiting for Guide, HOD Review, Event Preparation, Completed.

## Synchronization

- Supabase task ID maps one-to-one to a Trello card ID.
- Create/update/archive events pass through a small integration service with idempotency keys and an audit log.
- Cards use an opaque student code, safe action wording, cohort, due date, guide, priority, and deep link back to the protected CRM.
- Never put private revelations, LIT assessments, sadhana detail, phone numbers, birthdays, or sensitive guidance into Trello.
- Trello edits may update operational status/due date; Supabase resolves conflicts and remains authoritative.

