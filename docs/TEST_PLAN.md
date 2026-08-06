# Private MVP test plan

## Authentication

- Google-only sign-in succeeds in student, guide, and web test clients.
- Wrong/unauthorized account receives a safe denial.
- Deep-link callback returns to the correct test application.
- Logout and expired-session recovery work.

## Data and authorization

- Synthetic student submits sadhana and reads it back.
- Assigned guide and HOD can view it; another guide and another student cannot.
- Student cannot read LIT, mentor summaries, internal recommendations, or other students.
- Guide reassignment preserves audit history.

## CRM behavior

- Natural-language note produces an editable draft and asks only material missing questions.
- Only mentor-approved summary remains in durable storage.
- LIT history preserves all axes, evidence, confidence, assessor, and circumstances.
- Chanting reports use exclusive brackets and allow varying quarter totals.

## Notifications

- Timezone is Asia/Kolkata.
- Non-submitter reminders exclude completed students.
- Birthday reminders fire one day before and same day.
- Exam/festival windows modify cadence only after calendar approval.
- Duplicate jobs are idempotent and frequency limits prevent harassment.

## Corpus/RAG

- Every exact quote maps to a source locator.
- Paraphrases are labeled.
- Weak evidence yields uncertainty, not invented guidance.
- Student output excludes private assessments.

