---
name: belogical
description: 'Structures answers and documents as logic pyramids that fit how humans comprehend. Use for standalone documents (reports, proposals, plans, READMEs, announcements), drawing conclusions from unsorted material and ideas, checking and repairing the logic of existing text, and logically structured answers. Explicit `/belogical` invocation only — pass a route as the argument (e.g. `/belogical document`, `/belogical organize`, `/belogical repair`).'
disable-model-invocation: true
---

# belogical — the logic pyramid skill

Readers understand most easily when they read the conclusion first and take in each detail knowing what it supports. This skill applies the governing principles below to every answer, classifies each request and routes it to the methodology module that fits, and judges every deliverable against the same gate.

<!-- BELOGICAL:PRINCIPLES:BEGIN -->
## Governing principles for deliverables and answers

AI output is too long, too dense, and too complex for people. To help people understand, an AI must always put what it means to say in order before sending it out.

### Every answer must form a logic pyramid

A logic pyramid puts the core idea — the answer to the reader's question — at the top, held up by the supporting ideas beneath it. Supporting ideas are grouped horizontally by kind, and each group is stacked vertically so that the statement above is a summary of the items below. Reading this structure, the reader takes in the conclusion first and then follows each detail knowing what it supports. So the AI must always answer in the order a reader can follow, never in the mechanical order the information arrived in. The pyramid grows downward only while the reader still has questions — if the single sentence at the top closes the reader's question, stop there.

### Order your thinking before you write

1. Set the core answer you mean to deliver as one sentence at the top of the pyramid (the apex). If the answer honestly splits on the reader's situation, put the single variable that splits it into that sentence and give a decision for each branch ('if A, then P; if B, then Q').
2. Group the points you will make by kind — each group must be nameable by one plural noun (reasons, steps, problems). When dividing a whole, make the parts neither overlap nor leave gaps (MECE). Completeness is measured against what the question requires, not against everything on the topic.
3. Give every group one substantive summary sentence. An empty assertion that states only kind and count ('there are three issues') is not a summary. A summary must synthesize the core idea the items below actually share.
4. Order each group by logic: processes in time order, structures in the order the eye sees them, everything else in order of degree — the most important or strongest first.
5. Discard clutter that does not serve the core answer.

### Write as a dialogue with the reader

6. Lead with the point — in the answer as a whole and in every paragraph; a paragraph's first sentence is its conclusion. A condition or qualifier that changes the point's meaning goes in the same sentence as the point, never deferred.
7. A new idea raises questions in the reader's mind ('Why? How? Meaning what?'). Sequence the text so each question is answered right where it arises. Don't answer questions the reader hasn't asked yet, and don't raise questions you aren't ready to answer.
8. Move from what the reader already knows to what they don't. State definitions and premises before using them. Open each new sentence with what the previous one just established. In conversation, 'what the reader already knows' is the information in the context window plus the dialogue so far.
9. Put messages in headings and bullets too. Don't use category labels ('Background', 'Conclusion') as headings — except navigational headings that convention has fixed in reference documents (Installation, Usage). Use bullets only for true parallels (specs, procedures, checklists).
10. Reduce the load. Write plainly; don't dress ideas in jargon. If one sentence compresses several claims, split it sensibly. Delete anything whose removal loses no information: wrap-up remarks, formulaic transitions, ornament (emoji, heavy bolding, overselling).

### Always check before you deliver

Before delivering, ask whether the person reading this explanation will understand it easily. All of the following must pass:

- Does the whole point come across in the first 30 seconds?
- Is the reader left with no logical questions — counting only questions the answer itself raised? Questions you can't answer now, or that fall outside the answer's scope, get surfaced, not papered over.
- Can the reader stop at any depth without the takeaway flipping — reading only the apex, or down to each group summary, or the full text — with more depth adding only detail?
- Is every higher-level message a substantive summary of what sits below it — with no empty assertions ('there are three...') left?
- Do headings carry messages rather than category labels ('Background', 'Conclusion') — navigational headings in reference documents excepted?

If any check fails, reorder and only then deliver. When touching existing text, never change meaning, figures, or nuance (level of confidence, emphasis, implication).
<!-- BELOGICAL:PRINCIPLES:END -->

> **To apply the principles ambiently**: copy only the principles section between the `BELOGICAL:PRINCIPLES` markers above into your global (`~/.claude/CLAUDE.md`) or project CLAUDE.md. The principles then apply to every conversation without invoking `/belogical`. Do not paste the frontmatter or the routing and procedures below.

## These principles come first

The 'Governing principles' above take precedence over every module below. The numeric thresholds in the principles and the modules (the principles' '30 seconds', the modules' '4–5 per group') are recommended defaults for reducing cognitive load, not absolute rules. Depart from them when you judge the departure serves the reader's understanding — but have a reason when you do.

## Routing

If the user names a route as the argument (`/belogical repair`, etc.), go straight there without classifying. Otherwise take the first match from the top.

| Test (top to bottom) | Route | Modules to load |
|---|---|---|
| Gives existing text and asks to fix or check it | **repair** | references/repair-text.md (diagnostic criteria: grouping-order.md) |
| Asks for a deliverable that will be read standalone, outside this conversation | **document** | references/build-pyramid.md → scqa-intro.md → grouping-order.md → page-delivery.md |
| Hands over a pile of material or ideas and asks to draw a conclusion or organize it | **organize** | references/build-pyramid.md (bottom-up) + thinking-tools.md (check criteria: grouping-order.md) |
| Everything else — answering a question in conversation | **answer** | No extra modules — the principles above suffice |

Mixed cases:

- If a document is required but no conclusion stands yet, run the organize route first to obtain the apex sentence, then return to the document route.
- If repair needs rewriting beyond rearrangement, escalate to the document route — keeping the invariant that meaning, figures, and nuance do not change.

## Procedures per route

Whatever the route, run 'Always check before you deliver' above before delivering. If any check fails, return to the relevant module, reorder, then deliver.

### Answer — immediately, no modules

Apply the principles above and answer. In conversation the reader's question is already explicit — the user just asked it — so do not build an introduction (SCQA). If the answer grows into multiple sections, also apply the document route's heading rule (no category labels).

### Document — four modules in order

The reader of a standalone document doesn't hold a question yet. The writer must design the question and plant it.

1. **Set the apex** (build-pyramid.md): fix the reader's question and set the one-sentence answer at the top.
2. **Design the introduction** (scqa-intro.md): carry the reader to the apex through Situation–Complication–Question.
3. **Build the body** (grouping-order.md): descend the layers, form the groups, and check them against the three rules.
4. **Lay out the page** (page-delivery.md): arrange headings, hierarchy, and transitions so the whole registers within 30 seconds. For presentation decks, apply that module's presentation section.

### Organize — derive the conclusion bottom-up

1. Write down all the points, work out their relationships, and derive the conclusion (the bottom-up procedure in build-pyramid.md).
2. If the points are entangled, make the relationships visible with the problem-definition frame or a logic tree (thinking-tools.md).
3. Check the resulting groups against the three rules in grouping-order.md.
4. If the deliverable is a document, take the derived conclusion as the apex and hand off to the document route.

### Repair — diagnose, then rearrange

Follow the procedure in repair-text.md: extract → diagnose → rearrange → check. For the group and summary criteria used in diagnosis, see grouping-order.md. What makes text easier to understand is arrangement, not sentence style — preserve sentences as far as possible, and never change meaning, figures, or nuance (level of confidence, emphasis, implication).
