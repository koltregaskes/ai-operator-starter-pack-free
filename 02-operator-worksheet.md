# The Operator Worksheet

A working document. Print it, write on it, scan it back, share it with your team. It is deliberately small — four exercises that should take a focused person two to three hours total, spread across a week.

The worksheet assumes you have read the three lessons in `01-three-lessons.pdf`. If you have not, go and do that first. The exercises only work if the vocabulary is shared.

---

## Exercise 1 — The Harness Audit (one tool you use daily)

**Time required:** 30–45 minutes
**Output:** one filled audit table for one tool

Pick a single AI tool you use almost every day. Not the one you find most interesting — the one you actually use. Write its name in the title.

**Tool name:** ____________________________________________

For each layer of the harness, write what you know, what you suspect, and what is invisible to you. The point is not to be exhaustive — it is to map your own ignorance.

| Harness layer | What I know | What I suspect | What is invisible to me |
|---------------|-------------|----------------|--------------------------|
| **Prompt system** (the system prompt the tool sends with every request) | | | |
| **Tools / functions** (what the model is allowed to call) | | | |
| **Routing** (which model handles my request, and when it changes) | | | |
| **Memory / context** (what the tool remembers between turns or sessions) | | | |
| **Verification** (what the tool checks before returning output) | | | |
| **Sandbox** (what the model is and is not allowed to touch) | | | |

When you finish, look at the **invisible** column. That column is your real risk surface. Anything in it can change without warning, and you will feel it as "the model feels worse today" or "my prompt stopped working".

**Two follow-up questions to write a short answer to:**

1. If a vendor silently changed three things in the **invisible** column tomorrow, which one would I notice fastest? Which one might I never notice?
2. What would I have to do to move one item from **invisible** to **suspect**? (Talking to other operators, reading change-logs, instrumenting my own usage — be concrete.)

---

## Exercise 2 — The Regression Diary

**Time required:** 5 minutes per entry, sustained over four weeks
**Output:** a running log

The hardest thing about AI tools is that "it feels worse today" is real, but rarely caused by what you think. The regression diary is a discipline tool. It is not a complaint log. It is a way to convert vague frustration into evidence.

Use this template. Print copies, or keep it as a spreadsheet.

| Date | Tool | What I tried | What I expected | What happened | Likely harness layer | Confidence (low/med/high) | Reproduced? |
|------|------|--------------|-----------------|---------------|----------------------|---------------------------|-------------|
| | | | | | | | |
| | | | | | | | |
| | | | | | | | |

**Discipline rules:**

- Only fill it in when something *did* feel worse. Do not pre-fill.
- "Likely harness layer" must be a specific layer from Exercise 1 (prompt system, tools, routing, memory, verification, sandbox), not "the model".
- "Reproduced?" is critical. If you cannot reproduce it the next day, the change may have been transient or your prompt may have been the variable.
- After ten entries, look for patterns. The same layer keeps coming up? That is your highest-leverage place to instrument.

After four weeks, you will know more about your tools than the people selling them.

---

## Exercise 3 — The Prompt Failure Taxonomy

**Time required:** ongoing — three classifications per week minimum
**Output:** a running classification table

When a prompt fails, the failure is rarely "the model is dumb". This exercise trains you to classify failure precisely so you intervene at the right layer.

**The five failure classes:**

1. **Prompt failure** — the prompt was ambiguous, contradictory, or under-specified. The model behaved correctly given the input.
2. **Model failure** — the prompt was clear and complete, the harness was healthy, the model still produced wrong output. Genuinely the model.
3. **Tool failure** — the model called a tool, the tool returned bad data or errored. The model trusted the tool result.
4. **Routing failure** — the harness sent the request to a different model than expected (e.g. a faster, cheaper variant for a hard task), and the chosen model could not handle it.
5. **Verification failure** — the model produced output, no layer checked it before returning, and the failure passed through to me.

**Template:**

| Date | Prompt summary | Output summary | Failure class | Why I picked that class | Fix to try next time |
|------|----------------|----------------|---------------|--------------------------|----------------------|
| | | | | | |
| | | | | | |
| | | | | | |

**The goal:** after twenty entries, look at the distribution. If 80% of your "model is dumb" frustrations turn out to be prompt failures, that is enormously useful. If 80% turn out to be tool failures, you have a different problem and a different fix.

Most operators discover their distribution is wildly skewed and the skew points to a specific intervention.

---

## Exercise 4 — The "Before You Ship" Operator Checklist

**Time required:** 20 minutes to draft the first time, 1 minute to use thereafter
**Output:** a one-page personal checklist

Your job is to draft a ten-item checklist you will run before shipping any AI-assisted output that matters. The list is yours, not mine. The exercise is to force the muscle of asking "what could be wrong with this?" before pushing publish.

**Suggested categories — pick at least two checks from each:**

- **Prompt clarity** — is the request unambiguous? Did I specify the audience and format?
- **Context completeness** — did I supply enough source material, or did I assume the model knew?
- **Tool result trust** — if a tool was called, did I sanity-check the result?
- **Verification** — did I read the output critically, or skim it?
- **Stakes calibration** — does the output go to someone who will trust it more than they should?

**Write your ten items here.** They must be specific, checkable, and short. "Read it carefully" is not a check. "Read every numbered claim and search for one that I cannot defend" is.

```
1.
2.
3.
4.
5.
6.
7.
8.
9.
10.
```

Print the finished checklist. Stick it next to your monitor. Use it for one month before editing.

---

## What this worksheet is and is not

It is a discipline tool. Discipline tools are boring on purpose. They work because you use them, not because they are clever.

It is not a course. There is no certificate at the end. The reward is that you stop being surprised by your tools.

If you finish all four exercises and feel they were useful, the next step is to read the rest of the AI Resource Hub Academy material — the deeper lessons assume you have done this kind of work first.

If they were not useful, write me one sentence about why. The pack will improve faster from one honest "this exercise did not land" than from ten polite thank-you notes.

— AI Resource Hub
