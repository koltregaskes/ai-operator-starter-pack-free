# Harness Reference Card

A single printable page. Front: the three-layer diagram. Back: five concrete failure modes and how to notice them.

Designed for desk-side reference. Print at A5 (148 × 210 mm) or US Letter half-fold. The layout below is the source text — a designer / typesetter renders it into the final print PDF.

---

## FRONT — The Three-Layer Diagram

**Title:** What you actually use, when you "use AI"

**Subtitle:** Three layers, all changing on different schedules.

```
┌─────────────────────────────────────────────────────────────┐
│  LAYER 3 — THE SURFACE                                      │
│  The chat box, the IDE plugin, the in-app assistant.        │
│  What changes here: UI, settings, defaults, rate limits.    │
│  How fast it changes: weekly to daily.                      │
├─────────────────────────────────────────────────────────────┤
│  LAYER 2 — THE HARNESS                                      │
│  System prompts, tool calls, routing, memory, verification, │
│  sandboxing, context plumbing.                              │
│  What changes here: silently and often. Vendors usually do  │
│  not announce harness changes.                              │
│  How fast it changes: weekly. Sometimes hourly.             │
├─────────────────────────────────────────────────────────────┤
│  LAYER 1 — THE MODEL                                        │
│  The neural network weights themselves.                     │
│  What changes here: only when a new model version ships.    │
│  How fast it changes: monthly to quarterly. Always announced.│
└─────────────────────────────────────────────────────────────┘
```

**Footer (front):**
> When something "feels worse today", it is almost never the model. The model is the most stable layer. The harness is the noisy one.

---

## BACK — Five Harness Failure Modes

**Title:** How to notice the harness is misbehaving

A short reference. Each failure mode includes the symptom you feel, the layer that is moving, and one diagnostic question.

---

### 1. The Silent Reroute

**Symptom you feel:** "The model is dumber today."
**What is happening:** The harness is routing your request to a faster, cheaper, or smaller model variant — usually to manage capacity.
**Diagnostic question:** Has the response time also changed? A noticeably faster response with worse quality is a routing change.
**What to do:** Check whether the tool exposes a model selector. If it does, lock the larger model. If it does not, log the suspicion in your regression diary and look for a pattern.

---

### 2. The Drifting System Prompt

**Symptom you feel:** "The model started apologising more / refusing more / hedging more this week."
**What is happening:** The vendor updated the system prompt that wraps every request — usually to add a safety instruction or a behaviour tweak.
**Diagnostic question:** Are the changes consistent across multiple unrelated tasks? If the same shift appears across different prompts, it is the system prompt, not your prompt.
**What to do:** Test with a deliberately neutral prompt (e.g. "summarise this paragraph in three sentences"). If even that response shape changed, the wrapping prompt moved.

---

### 3. The Quiet Tool Failure

**Symptom you feel:** "The answer looks right but is subtly wrong."
**What is happening:** A tool the model called returned bad data, and the model trusted the result without flagging the trust.
**Diagnostic question:** Does the answer contain any specific number, name, or fact that the model could not have known without a tool? If yes, that is the failure surface.
**What to do:** Re-ask the question, this time explicitly: "List every external lookup you would need to answer this. Then answer." Many silent tool failures show up only when you make the lookup explicit.

---

### 4. The Lost-Context Loop

**Symptom you feel:** "The model forgot what we just discussed."
**What is happening:** The harness is dropping older parts of the conversation — usually because the context window filled up, or because the harness condensed earlier turns into a summary.
**Diagnostic question:** Did this start happening after a specific message? If yes, that message likely pushed the conversation past a context threshold.
**What to do:** Re-paste the critical context once at the top. If that fixes it, the problem was context truncation. If not, the problem is verification — the model never had a hold on it in the first place.

---

### 5. The Verification Gap

**Symptom you feel:** "The model produced a confident answer that turned out to be wrong, and nothing flagged it."
**What is happening:** The harness has no automated check on the kind of output you got — it returned the model's first draft to you without grading it.
**Diagnostic question:** Was there a moment in the response where you would have wanted a second opinion? That is the verification gap.
**What to do:** Add your own verification turn — re-ask the model to grade its own confidence on each claim (see *The Verifier* in the prompt kit). It is a workaround, not a fix, but it closes 80% of the gap.

---

**Footer (back):**
> The model is the smallest cause of "the model feels different".
> Look at the harness first. Look at the surface second. Look at the model last.
> — AI Resource Hub

---

## Designer notes

- A5 portrait or US Letter half-fold portrait, double-sided
- Body type: 10/14 pt, generous line-height
- Diagram on front fills 65% of the page; the footer line sits in the bottom 15%
- Back page: five sections, each a clear small block with a heading and four lines of body
- Use the AI Resource Hub palette (charcoal background, off-white text, single accent colour)
- Keep all diagrams in vector (SVG) so the print holds at any size
