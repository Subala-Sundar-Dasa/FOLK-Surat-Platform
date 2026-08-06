# Data model blueprint

Primary entities: `profiles`, `guide_assignments`, `colleges`, `academic_calendars`, `calendar_events`, `sadhana_entries`, `interaction_events`, `mentor_summaries`, `lit_assessments`, `abcde_progress`, `books`, `book_progress`, `hearing_modules`, `hearing_progress`, `services`, `service_interests`, `trips`, `trip_participants`, `trip_goals`, `trip_commitments`, `competitions`, `rdua_sessions`, `student_reflections`, `recommendations`, `approvals`, `notifications`, `tasks`, and `audit_events`.

## Important constraints

- A student may have one active primary guide and historical assignments.
- Raw verbose notes are transient by default; retain only the mentor-approved summary after posting.
- Each extracted assessment stores evidence, assessor, timestamp, and confidence.
- LIT assessments are versioned and private.
- Chanting brackets are exclusive snapshots, not cumulative counts.
- Calendar facts can be sourced from the internet or guide input, but a guide approves the calendar assigned to each student.
- HOD can observe all Surat operations; guides can access assigned students and authorized shared work.
- Students can access only their own student-facing data and never internal assessments.

## RLS test matrix

Every migration must test: student self-read/write, assigned-guide access, unassigned-guide denial, HOD visibility, anonymous denial, and service-role-only background jobs.

