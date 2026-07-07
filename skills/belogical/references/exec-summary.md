# exec-summary — Summarizing a finished source

> Role: compress a finished source — a report, paper, book, article, transcript, or a pile of documents — into a summary the reader uses in place of reading it, re-aimed at the reader's question.
> Loaded on: summarize. For the bottom-up merge of part-extractions, see build-pyramid.md §3; for ordering and group checks, grouping-order.md §1 and §3.
> Invariant: the summary makes no claim the source does not make, and figures and nuance (level of confidence, emphasis, implication) survive faithfully in what remains. Unlike repair, dropping is the job — the invariant binds only what stays, and completeness is measured against the reader's question, not the source's contents.
> The pyramid logic is Minto's; the extraction contract and map-reduce procedure for oversized sources are this skill's own method.

## 1. The summary replaces the reading

The reader understands what the source claims without opening it — the summary is the deliverable, not a preview or an invitation to read. The source persists behind it, so keep every key point traceable to its part of the source (chapter, section, document); in conversation the agent holds that map, and the reader drills into any point by asking. The source needs no structure of its own — a transcript or a thread has no pyramid to extract, so build one bottom-up from what was actually said; the invariant binds all the same. One boundary: a summary section of a document you are writing belongs to the document route (the 30-second rule, page-delivery.md §1) — this module is for sources that already exist.

## 2. The defining defect — sequence-mirroring

A summary that walks the source in its own order ('the report covers X, then turns to Y') tells the reader what reading it would feel like, not what it concluded: a table of contents in prose. Select and order by the reader's logic instead. Its twin is coverage-guilt — a point earns inclusion by answering the reader's question, never by the pages the source spent on it. Identical order is not itself the defect; inherited order is. The test: would this order survive if the source's parts were shuffled?

## 3. Re-aim the apex at the reader's question

The reader's question may differ from the source's organizing question — the source asks 'why did it happen', the reader asks 'what do we do'. Fix the reader and their question first, and set the apex as the source's answer to that question. If the source does not answer it, saying so is the apex — never invent the answer. Most requests arrive with no stated question: infer it from the conversation, and failing that, default to the source's own organizing question restated for the requester — and say that is what you did. When a question is stated, re-aiming is the work.

## 4. Length is set by the question, not the source

A one-page memo may compress to a sentence or two; a book to about a page. These are observed defaults, not a scale formula — length tracks how much of the source the reader's question makes relevant. One page is the recommended ceiling, never a floor; stop the moment the reader's question closes. The procedure scales the same way (grouping-order.md §7): a short article needs no contract and no intermediate artifacts — read, re-aim, compress. The full procedure below is for sources that are large or carry stakes.

## 5. Procedure — source fits in context

1. Read the whole source; fix the reader and their question (§3).
2. Extract per part: the part's core claim as one complete sentence with subject and predicate, its strongest supports with figures verbatim, its confidence and nuance markers, and its role in the whole.
3. Select: keep the claims that answer the reader's question; drop the rest.
4. Rebuild conclusion-first: apex on top, kept claims grouped and ordered by the grouping's own logic (grouping-order.md §3), never by inherited page order.
5. Attach traceability (§1) and run the check (§8).

## 6. Procedure — oversized or multi-document sources

When the source exceeds the context window or is a pile of documents, split along the source's own structure: chapters and sections for one document, document by document for a pile (a folder, an email or chat thread). Run one subagent per part. Each subagent receives the whole's frame — the table of contents or document list plus the reader's question — together with its part, and returns the fixed extraction contract:

1. The part's core claim as one complete sentence (subject and predicate, not a topic label).
2. The strongest supports, figures verbatim.
3. Confidence and nuance markers as the source states them.
4. The part's role in the whole.

A sequential mini-summary of the part is explicitly out of contract — it reproduces the §2 defect at part level and poisons the merge. If the host cannot run subagents, process the parts sequentially yourself under the same contract: read one part, write down its contract output, discard the part's text, then read the next — only the contract outputs and the whole's frame carry forward. Then merge: deduplicate claims that in effect say the same thing, reconstruct the pyramid bottom-up (build-pyramid.md §3), and re-aim at the reader's question (§3).

## 7. The lead-in — usually none

When the requester is the reader, the question is already explicit — open with the apex and no introduction, exactly as the answer route does. Only when the summary travels standalone to readers who didn't ask for it, prepend one sentence of Situation–Complication naming the source and the question it answers (the full method: scqa-intro.md).

## 8. Check

This check replaces repair-text.md §4 for this route:

- Every claim in the summary is a claim the source makes — none added, none strengthened or weakened.
- Figures verbatim; a hedge the source tied to a claim rides in the same sentence as that claim. The summary may be written in the reader's language rather than the source's — figures, proper nouns, and key terms stay exact.
- Nothing kept out of coverage-guilt; nothing essential to the reader's question dropped.
- The order is the grouping's own logic, not the source's page order inherited.
- Each key point is traceable to its part of the source; questions the summary leaves open point into the source, not papered over.
- Then run 'Always check before you deliver' in SKILL.md.
