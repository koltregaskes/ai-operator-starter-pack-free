# The Operator Prompt Kit

Ten deliberate prompts. Each one solves an operator-grade problem — the kind of work you do when you treat AI as part of a system, not as a magic box.

For each prompt:

- **The prompt itself** — copy and paste, edit the bracketed parts.
- **The operator reasoning** — why this prompt is shaped the way it is. The reasoning is the actual lesson; the prompt is just the artefact.
- **Where it works best** — Claude, ChatGPT, or Gemini. Most work in any. A few use specific affordances.

---

## 1. The Hostile Reviewer

**Use when:** you are about to ship something and want one more pass that is not lazy praise.

**Prompt:**
> You are a hostile but fair reviewer. Read the document below and find the three weakest claims. For each, explain why it is weak and what would have to be true for it to hold. Do not soften your language. Do not list strengths. Do not number more than three — pick the three most important.
>
> [DOCUMENT]

**Operator reasoning:**
Models default to being agreeable. "Find issues" returns a generous list of mild concerns. "Find the three weakest claims and do not soften" forces a real opinion and bounds the response so you can actually use it.

**Best on:** any. Claude is currently the most willing to be specifically critical when asked.

---

## 2. The Verifier

**Use when:** the model has produced a confident answer and you want to check whether it actually checked anything.

**Prompt:**
> You produced this answer:
>
> [PASTE THE ANSWER]
>
> Now do three things, in this order:
>
> 1. List every factual claim in the answer as a numbered list. Do not summarise — list each claim atomically.
> 2. For each claim, mark it as: VERIFIED-FROM-SOURCE / VERIFIED-FROM-MEMORY / UNVERIFIED.
> 3. For every UNVERIFIED claim, propose the smallest possible action that would verify or falsify it.

**Operator reasoning:**
This separates "the model said it confidently" from "the model knows it". Most "hallucinations" are actually unverified claims dressed in confident language. Asking the model to grade its own confidence after the fact is more reliable than asking for caveats inside the original answer.

**Best on:** Claude or Gemini. ChatGPT tends to over-mark things as VERIFIED-FROM-MEMORY.

---

## 3. The Reverse-Brief

**Use when:** you are about to send a brief to a contractor, agency, or another AI, and you want to know whether it is actually unambiguous.

**Prompt:**
> You are reading the brief below for the first time. You are not allowed to ask questions. Tell me:
>
> 1. The single sentence I would write to summarise what you have been asked to do.
> 2. Five specific things you would have to assume because the brief did not specify them.
> 3. The two assumptions most likely to make you produce work I would reject.
>
> [BRIEF]

**Operator reasoning:**
Briefs feel complete when you write them and feel ambiguous when someone else reads them. The model is the cheapest fresh reader you have. The "no questions" constraint forces it to surface assumptions instead of asking for clarification — that is the failure mode you are trying to spot.

**Best on:** any.

---

## 4. The Pre-Mortem

**Use when:** about to launch, ship, publish, or commit to a decision.

**Prompt:**
> Imagine it is six months from now and the [DECISION / LAUNCH] has clearly failed. Write a short post-mortem from that future perspective. Cover:
>
> - What were the three earliest signals that something was wrong?
> - Which assumption, if questioned upfront, would have changed the decision?
> - What did we miss that, in hindsight, was obvious?
>
> Write it as if the failure already happened.

**Operator reasoning:**
Asking "what could go wrong" returns a polite hedged list. Asking the model to write from a future where the failure already happened removes the hedge and produces specific, useful failure modes. This is a documented technique called pre-mortem; it works as well with models as with humans.

**Best on:** any.

---

## 5. The Five-Whys, Properly Run

**Use when:** something broke and you want to find the systemic cause, not the proximate one.

**Prompt:**
> The following thing happened:
>
> [DESCRIPTION OF WHAT WENT WRONG]
>
> Run a five-whys analysis. After every "why", do not move on until you have written one sentence about whether the answer is a person-issue, a process-issue, or a system-issue. The fifth "why" should resolve to a system-issue if at all possible — if it resolves to a person, treat that as a sign you stopped one why too early.

**Operator reasoning:**
Five-whys done badly resolves to "X person did not check". Done properly it resolves to "the system did not require checking". The constraint that the fifth why must lean toward a system answer is what saves the technique from becoming a blame exercise.

**Best on:** Claude. It is the best at sustaining the chain.

---

## 6. The Voice-Match Critic

**Use when:** writing something in your voice and the model has produced a draft that is technically fine but does not sound like you.

**Prompt:**
> Read the two passages below.
>
> SAMPLE OF MY WRITING:
> [PASTE 200–400 WORDS YOU WROTE]
>
> DRAFT THE MODEL JUST PRODUCED:
> [PASTE THE DRAFT]
>
> List the five biggest stylistic differences between the two passages. Then rewrite the draft to match the sample's voice. Do not change the meaning. Do not "improve" it.

**Operator reasoning:**
Voice transfer is hard because the model's defaults are loud. Showing it the gap between your sample and its draft, then asking for a rewrite that respects meaning, gets much closer than "write in my voice" ever will.

**Best on:** Claude or Gemini.

---

## 7. The Constraint-Stripper

**Use when:** the model has produced something that feels generic, and you suspect it is hedging.

**Prompt:**
> Look at the answer you just gave. List every place where you hedged, qualified, or added "however" / "but it depends" / "in some cases". For each one, tell me:
>
> 1. What you would say if you were not allowed to hedge.
> 2. The single condition under which the hedge would be the correct answer.

**Operator reasoning:**
Hedges are how models manage uncertainty. They are also how models smuggle in laziness — "it depends" without specifying what it depends on is a dodge. This prompt makes the dodge visible and forces a stronger answer.

**Best on:** any.

---

## 8. The Steel-Man

**Use when:** you have a strong opinion and you want to interrogate it.

**Prompt:**
> I believe [POSITION]. Build the strongest possible argument against my position. The argument should be made by someone who is intelligent, well-informed, and not strawmanning me. After the argument, list the two pieces of evidence I would need to produce to defeat it.

**Operator reasoning:**
Asking for "counter-arguments" returns a list of mild objections. Asking for a steel-manned opposing case forces the model to do real work. The "two pieces of evidence" closer keeps the exercise actionable instead of philosophical.

**Best on:** Claude.

---

## 9. The Diff-Reviewer

**Use when:** you have edited something and want to understand what changed and whether it improved.

**Prompt:**
> Compare these two versions of the same document.
>
> ORIGINAL:
> [V1]
>
> EDITED:
> [V2]
>
> Tell me:
>
> 1. The three most significant differences.
> 2. For each, whether the edit made the document stronger, weaker, or neutral, and why.
> 3. One specific change that, if you were the editor, you would have made instead.

**Operator reasoning:**
Self-reviewing your own edits is hard because you are still in the writing flow. Off-loading the comparison forces a fresh read. The "what would you do instead" closer prevents the model from defaulting to flattery.

**Best on:** any.

---

## 10. The "Why Is This Hard?" Prompt

**Use when:** stuck on something and not sure why you are stuck.

**Prompt:**
> I am trying to do this:
>
> [DESCRIPTION OF WHAT YOU ARE TRYING TO DO]
>
> I have been stuck for [TIME]. Without trying to solve the problem, tell me:
>
> 1. Why this kind of problem is usually hard for people who try it.
> 2. The three most common ways people get stuck on this specific kind of problem.
> 3. Which of those three is most likely to be what is happening to me, based on what I have told you.
>
> Do not give me a solution. Diagnose the stuckness.

**Operator reasoning:**
"Help me solve this" returns a generic plan. "Diagnose why I am stuck" forces a different mode and often surfaces the real issue, which is usually an unspoken assumption or a missing piece of context. The "no solution" constraint is what makes it work — solutions are cheap, diagnoses are valuable.

**Best on:** Claude.

---

## How to use the kit

These prompts are not magic. They are leverage. They work best when:

- You treat the response as a draft, not a verdict.
- You combine them — run the Hostile Reviewer on output the Verifier already passed.
- You modify them. The reasoning is the lesson; the prompt is just the entry point.

The pack is deliberately small because ten prompts you actually use beat a hundred you have bookmarked.

— AI Resource Hub
