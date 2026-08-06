# Edge Cases and Vocabulary Revision Decisions

## Corpus checkpoint

- Original RTF masters: **26**
- Faithful Unicode Pass-1 Markdown files: **26**
- Natural recording events detected: **3,222**
- Planned NotebookLM transcript sources: **240**
- Words scanned: approximately **10.86 million**
- Median natural event: **2,990 words**
- Largest natural event: **37,085 words**
- Unique normalized scriptural references detected: **1,190**
- Exact duplicate source files: **0**
- Exact duplicate event-text groups: **0**

## Edge cases discovered

### 1. Legacy Balaram font encoding

The RTF files do not contain modern Unicode diacritics. A generic RTF extractor
produces corrupt forms such as `Prabhupõda` and `KÕ±Ùa`. Pass 1 therefore uses
the original Balaram character map before Unicode NFC normalization.

**Decision:** Preserve the original RTFs unchanged. All working and final
Markdown uses Unicode IAST. Conversion QA must report zero residual legacy
encoding corruption.

### 2. Aggregated sources conceal thousands of natural events

The 26 RTFs contain 3,222 conversations, walks, interviews, lectures,
ceremonies, and philosophical discussions. One file per recording would exceed
NotebookLM's 300-source limit by more than ten times.

**Decision:** Bundle complete events into exactly 240 transcript sources. Never
split an event merely to obtain equal file sizes. Small categories remain
intact; unusually long individual events remain intact.

### 3. File-level tags become too broad

At approximately 45,000 words per bundle, many broad concepts occur in nearly
every source. Presence alone would assign tags such as `Bhagavad-gita`,
`maya`, `preaching`, or `science` almost everywhere and would reduce search
precision.

**Revision proposed for Vocabulary 1.0:**

- Use **8–15 dominant file-level tags**, selected by density and distinctiveness,
  not mere occurrence.
- Add **3–8 event-level semantic tags** beneath each recording heading.
- Treat terms appearing across more than 80 percent of bundles as corpus
  stop-tags unless their density is unusually high in the particular file.
- Use a family quota so one dimension cannot fill all available tag positions.

### 4. Event type must come from the event header

Words such as “initiation,” “wedding,” “festival,” and “morning walk” may be
mentioned inside unrelated conversations.

**Decision:** Determine event type from the event title and code, not from body
keyword frequency.

### 5. Duplicate event code without duplicate content

`710729iv.gai` occurs twice in the 1971 conversations. The two items have
different titles, word counts, and text hashes.

**Decision:** Do not delete either event. Retain both and distinguish them by
event sequence and title. A repeated code is a review flag, not proof of a
duplicate.

### 6. Missing date or place metadata

There are **103** events without a recoverable date/place string. Most are
philosophical discussions identified by codes such as `KANT.SYA` or
`SOCRATES.HAY`.

**Decision:** Use `date_place_status: not supplied in source`. Do not infer a
date or place from neighbouring material unless the source explicitly connects
them.

### 7. Very short fragments and excerpts

There are **148** events under 500 words, including **11** under 100 words.
Some are genuine excerpts, short comments, blessings, or ceremony fragments.

**Decision:** Keep them when they have a distinct source code. Bundle them with
adjacent events from the same source category. Apply
`transcript-status:fragment` or `transcript-status:excerpt`; do not pad them
with inferred content.

### 8. Very long individual recordings

There are **49** events over 10,000 words and **11** over 20,000 words. The
largest is the 5 August 1976 New Mayapur room conversation at approximately
37,085 words.

**Decision:** Keep each recording whole. NotebookLM's per-source limit is far
above these sizes, and citation coherence is more valuable than artificial
uniformity.

### 9. Unclear audio and editorial notation

The corpus contains approximately:

- 5,538 `(indistinct)` or equivalent markers
- 9,824 `[break]` markers
- 4,117 uncertainty markers such as `(?)`
- 3,202 explicit end markers

**Decision:** Preserve these as source-critical evidence. Normalize their
format but never silently invent missing words. Add transcript certainty
metadata at event level when the density is material.

### 10. Multiple languages

There are approximately 4,548 explicit language markers, including Sanskrit,
Hindi, Bengali, Gujarati, German, French, Marathi, and Tamil.

**Decision:** Preserve supplied language labels and the transcribed material.
Do not treat a quoted untranslated passage as an English semantic assertion.
Use language metadata separately from topic tags.

### 11. Speaker labels are inconsistent

Participants may be named, numbered (`Guest (1)`), generic (`Devotee`,
`Indian man`), unidentified, or represented inconsistently across events.

**Decision:** Maintain an authority table containing the original label,
normalized label where certain, and certainty status. Never merge generic
participants solely because their labels match.

### 12. Quoted positions versus Śrīla Prabhupāda's teaching

Interviews and philosophical discussions frequently quote scientists,
philosophers, journalists, disciples, or opposing doctrines before Śrīla
Prabhupāda responds.

**Decision:** Distinguish `position:explained`, `position:quoted`,
`position:critiqued`, and `position:affirmed`. A body keyword does not by itself
show endorsement.

### 13. Scriptural abbreviations and citation form

The corpus uses abbreviated references, variant capitalization, ranges, and
occasionally malformed or incomplete references.

**Decision:** Preserve the source text but add canonical metadata anchors:

- `Bg. 2.13` → `Bhagavad Gita As It Is 2.13`
- `SB 1.2.4` → `Śrīmad-Bhāgavatam 1.2.4`
- `Cc. Ādi 1.3` → `Chaitanya Charitamrita Ādi 1.3`

Unresolvable references receive a review flag rather than a guessed number.

### 14. Lecture anchor versus incidental citation

A Bhagavad-gītā lecture may cite Śrīmad-Bhāgavatam and many other works. If all
citations become equal tags, the principal anchor is lost.

**Decision:** Separate `primary-scriptural-anchor` from
`referenced-scriptures`. Determine the primary anchor from the recording title
and header.

### 15. Advanced devotional and rasa terminology

Names such as Rādhārāṇī, the gopīs, Vṛndāvana, or rasa may occur in introductory
or incidental contexts.

**Decision:** Apply advanced devotional tags only when an event substantively
explains the relationship, mood, līlā, or siddhānta. A name occurrence alone
does not qualify.

### 16. Historical instruction versus universal principle

Conversations often combine enduring siddhānta with temporary management
directions, local circumstances, travel arrangements, financial decisions, or
instructions to a particular disciple.

**Decision:** Distinguish:

- `instruction-scope:universal-principle`
- `instruction-scope:mission-policy`
- `instruction-scope:local-direction`
- `instruction-scope:personal-guidance`

### 17. Sensitive historical language

Some statements concern race, nationality, gender, religion, politics, social
class, bodily identity, or contemporary controversies. Removing context could
misrepresent the discussion.

**Decision:** Preserve speaker, date, place, interlocutor, and neighbouring
argument. Use descriptive contextual tags rather than modern evaluative labels.
Do not rewrite Śrīla Prabhupāda's words.

### 18. Source front matter and repeated headings

The aggregated RTFs include contents material and repeated title/date blocks.

**Decision:** Preserve source front matter once in Pass 1. In segmented
NotebookLM files, represent each event with one Markdown heading and one
metadata block, while keeping the spoken transcript unchanged.

## Vocabulary 1.0 structural revision

The final semantic layer should have two levels.

### File-level metadata and dominant tags

- source family
- source RTF and checksum
- part number and event-code range
- dominant event forms
- 8–15 density-ranked semantic tags
- principal scriptures
- principal people and places
- corpus and transcript status

### Event-level semantic block

- event code
- title
- date and place
- event type
- primary scriptural anchor
- normalized explicit references
- principal speakers
- 3–8 event-specific semantic tags
- instruction scope
- position or speech function
- language and transcript-certainty flags

This two-level method gives NotebookLM precise search terms near the relevant
passage without consuming additional source slots or covering the spoken text
with tags.
