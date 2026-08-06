# Prabhupada-grounded RAG

The curated corpus in `knowledge-base/prabhupada-corpus/` contains Markdown books, correspondence, audio transcripts, indexes, metadata guides, vocabulary/glossary material, source maps, citation guidance, and QA notes.

## Retrieval contract

1. Retrieve by semantic similarity plus metadata filters.
2. Preserve source ID, title, date, content type, section/chapter, and stable chunk locator.
3. Prefer direct primary-source context over generated summaries.
4. Mark exact quotations explicitly and never reconstruct missing words.
5. Label paraphrases as paraphrases and provide traceable references.
6. If evidence is weak or conflicting, say so and route practical judgment to the guide.
7. Never expose internal LIT or mentor notes in a student response.

## Two outputs

- Guide-facing: recommendation, rationale, evidence, confidence, suggested conversation, and “why this guidance.”
- Student-facing: warm principle-level encouragement, optional reflective question, safe invitation to share more, and guide escalation when practical/private guidance is needed.

## Corpus handling

The Git copy is a working derivative. Do not rewrite the originals in the D-drive archive. Do not upload the corpus to external AI/vector services without separate approval. A future manifest must record checksums, source collection, category, and processing status.

