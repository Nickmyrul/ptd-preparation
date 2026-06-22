---
name: storm-research
description: Research any topic rigorously using the Stanford STORM method (multi-perspective scan, contradiction map, synthesis, peer review), then optionally run an autoresearch-style tournament to pick the strongest framing. Use when you need a fast, multi-angle, source-grounded research brief before writing, deciding, or building — especially when a single-prompt answer would miss the non-obvious insight. Grounds every claim in live web search.
---

# STORM Research Method

STORM = Synthesis of Topic Outlines through Retrieval and Multi-perspective Question Asking (Stanford). The point is to interrogate a topic from genuinely different vantage points instead of settling on one comfortable consensus. That is what surfaces the insight a single-prompt search misses.

Run all four prompts in order. Ground every factual claim in a real web search (use whatever web/search tool the environment provides); do not assert numbers or trends from memory. Cite sources as you go.

## Inputs
- **Topic** (required): the subject to research.
- **Audience/context** (optional): who the output is for and why. Tune the expert panel and the synthesis to this.

## Prompt 1 — Multi-Perspective Scan
Generate **five distinct expert viewpoints** on the topic and research each with web search. Default panel (swap any for a more topic-relevant expert):
1. **Practitioner** — the person doing the work daily. What actually changes on the ground?
2. **Academic / analyst** — what do the data and research say? Pull concrete numbers, studies, surveys.
3. **Skeptic** — what is overhyped, unproven, or failing in practice?
4. **Economist** — costs, incentives, second-order effects, who pays.
5. **Historian** — has this happened before? What is genuinely new vs. recycled?

For each viewpoint, capture 2-4 grounded findings with a source URL.

## Prompt 2 — Contradiction Map
Across the five viewpoints, identify:
- Where do they **conflict**? (the tension is usually where the real insight lives)
- Which claims have the **strongest evidence**, which are thin?
- What **blind spots** do all five share?

## Prompt 3 — Synthesis
Consolidate into a short executive briefing:
- **Key conclusions** (3-5 bullets, each defensible from the research)
- **Actionable insights** (what someone should actually do)
- **Frontier questions** (what is still unresolved)

## Prompt 4 — Peer Review
Self-critique before handing off:
- Rate **confidence** per key conclusion (high/medium/low).
- Flag the **weakest claim** and why.
- Check for **bias** (cheerleading a trend, recency bias, single-source reliance).
- Name any **missing perspective** that would change the picture.

## Optional — Autoresearch-style angle tournament
Borrowed from `karpathy/autoresearch`, which runs many short, cheap experiments and keeps only the winners by a single metric. When the deliverable is a piece of writing or a recommendation (not just a brief), do not hand-pick one framing — run a tournament:

After Prompt 3, generate **5-8 candidate framings/angles** from the brief, score each against a rubric, and keep only the top 1-2. A general-purpose rubric (adapt per use case):
- **Hook / attention** (0-3): would the opening make the audience keep reading?
- **Specificity** (0-3): a concrete number, named case, or first-hand detail — not generic.
- **Non-obviousness** (0-3): says something the contradiction map surfaced, not the consensus take.
- **Credibility fit** (0-2): plausibly ownable by whoever is publishing it.
- **Engagement / action pull** (0-2): invites a reply, a decision, or a next step.

Total out of 13. Discard anything under ~9. Keep a note of which framings scored well so the loop compounds over time.

## Output
Return a `## STORM Brief: <topic>` block with the four sections (and the tournament result if used), plus a **Sources** list of every URL. Keep it tight — this is research fuel, not a report.

## Notes
- The method compresses many hours of reading into minutes, but only if the searches are real. Skipping the web grounding defeats the purpose.
- For a heavier pass, run two rounds: a broad first scan, then a focused second scan on the contradictions the first round surfaced.
