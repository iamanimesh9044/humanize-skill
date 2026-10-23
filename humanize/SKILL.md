---
name: humanize
description: Write or rewrite text so it reads like a person wrote it, not an AI. Use whenever drafting or editing messages, Slack posts, emails, PR descriptions, status updates, incident notes, feedback, docs, or any prose meant for a human reader. Also use when the user says "make it sound human", "less AI", "humanize this", or asks for a message to send to someone. Plain, simple words; specific details; no filler.
---

# Humanize

Goal: text a skilled reader would assume a real colleague wrote. Simple words, easy to read, nothing that smells like AI.

Based on research (see [evidence.md](evidence.md)). Key lesson: readers spot AI by structure and "safe, generic" content, not by single words or by typos. So fix the structure and add real specifics. Don't fake humanity.

## Rules, in priority order

1. **Specifics from the input.** Name the repo, person, number, date, file. "billing, auth and notifications", not "multiple services". Generic, safe, unspecific content is a top tell. Only use specifics the user gave you. If one is missing, ask or leave a `[placeholder]`. Never invent names, numbers, anecdotes, or feelings.
2. **Answer first.** Point in line one, details after.
3. **Plain words, plain verbs.** "use" not "leverage". "is/has" not "serves as/boasts". Verbs over noun forms: "we decided" not "the decision was made", "fix" not "implementation of a fix". Don't try to sound smarter or more complex. Plain is not the tell.
4. **Uneven rhythm.** Mix short and long sentences. Fragments are fine in chat. Don't let every sentence be the same size.
5. **Take a stance.** "I'd go with B, because X." One opinion with a reason. Not "both have merits."
6. **Stop when done.** No summary of what you just said. No wrap-up line. No offer ("Let me know if...", "Happy to help", "Hope this helps"). Test: delete the last sentence. Usually it's better.
7. **Say it once.** Cut restating and over-explaining. Short messages stay short.
8. **Hedge once, where you're really unsure.** "Not sure if Ravi's team still uses v1, checking." Not hedges on every claim, not fake confidence either.
9. **Match the channel and the sender.** Slack is short and casual. Email is a bit fuller. PR is structured but brief. If the user gives samples of their own writing, copy that voice (length, punctuation, casing, how they greet and sign off) over any generic rule here.

## Structures to avoid (strongest evidence, ban by pattern not by word)

- Negative parallelism: "not just X, it's Y", "not only X but also Y", "rather than merely X", "It's not X, it's Y"
- Lists or runs of three ("fast, reliable, and scalable")
- Trailing "-ing" tails that add significance: ", highlighting the importance of...", ", ensuring that...", ", underscoring..."
- "serves as", "stands as", "boasts", "features" where "is" or "has" works
- Significance inflation: "plays a crucial role", "a testament to", "pivotal moment", "matters because"
- Vague attribution: "experts say", "many believe", "studies show" with no name
- Tidy upbeat closer that restates the point
- Praise or filler openers: "Great question!", "Certainly!", "Absolutely!", "I hope this finds you well"
- Offer closers on every message
- Over-explaining the obvious, repeating the same idea in new words
- Every speaker or section sounding the same
- Inline bolded mini-headers or emoji bullets in a short message
- Balanced, parallel bullet lists in chat

## Words (examples only, this list decays, the patterns above matter more)

delve, tapestry, intricate, meticulous, commendable, pivotal, crucial, testament, vibrant, realm, landscape, underscore, showcase, leverage, utilize, facilitate, streamline, robust, seamless, holistic, comprehensive, navigate (figurative), unlock, elevate, palpable, amidst, camaraderie, "it's worth noting", "it's important to note", "in today's fast-paced world".

Newer models have their own tells and they shift over time. Judge by feel: would a colleague type this word in Slack?

## Light touch

- **Em dashes:** weak signal and model-dependent. Use at most one in a message. Prefer a comma, period, or "and".
- **Contractions:** use them because people talk that way. They are not a trick. Don't force them where the user writes formally.
- **Typos, slang, lowercase:** don't add fake typos, filler, or fake anecdotes to seem human. No evidence it helps and it can read as fake. Only mirror what the user's own samples show.
- **Thanks, apology, praise, feedback:** these are the messages where readers punish suspected AI the most. Keep them short, use the user's own words and real details, skip the polish.
- **Frameworks (BLUF, SCQA, SBI, no-hello):** useful defaults, not laws. No controlled evidence behind them.

## Message patterns

Pick the one that fits. See [patterns.md](patterns.md) for examples.

- Asking for something: Context → Request (→ Outcome)
- Proposing a change: Problem → Solution → Benefit
- Giving a task: Goal → Steps → Constraints (+ file pointer, scope limit)
- Junior asking senior: Observation → Question
- Update: Status → Blocker (who, when) → Next step
- PR description: What changed → Why → How to verify → Risk
- Need a decision: ask with a default and a deadline
- Several options: Options → Recommendation (pick one, say why)
- No action needed: "FYI, no action needed: ..."
- Follow-up: short nudge, no repeated context
- Outage: What happened → Impact → Cause → Fix → Prevention
- Feedback: Situation → Behavior → Impact
- Saying no: Acknowledge → Constraint → Alternative
- Disagreeing: state it once, then commit

## Workflow

1. Identify reader and channel. Check if the user gave samples of their own writing.
2. Pick the pattern.
3. Draft with real specifics from the user's input. Ask for anything missing.
4. Run the checklist below and fix.
5. Output only the final text. No "Here's a humanized version:" intro, no explanation, unless asked.

## Output format (strict)

The text will be copy-pasted into Slack, email, or a doc. Formatting breaks on paste.

- Never use tables in the output. Not even for comparisons or lists of facts. Use short sentences or plain lines instead.
- No markdown in the message itself: no `|` pipes, no `**bold**`, no `#` headers, no `---` rules. Exception: a PR description going to GitHub may keep light markdown.
- Lists only if the channel needs them, and then plain lines starting with "-" or "1.". Never nested.
- Put the final message in a single plain-text code block so copying gives clean raw text.
- If you have 2+ versions, label each with one plain line above its own code block ("Slack:", "Email:"). Don't compare them in a table.
- Keep any note to the user outside the block, one line max.

## Final checklist

- Could a stranger tell exactly which repo, person, or date I mean?
- Did I state one opinion, with a reason?
- Can I delete the last sentence?
- Any negative parallelism, triple, "-ing" tail, or "serves as"?
- Any claim with no named source or number?
- Did I invent anything the user didn't tell me? Remove it.
- Sentences all the same length? Break one up.
- Any header, bold, table, or bullet a person wouldn't use in this channel?
- Would I type this in under a minute?

## Rewriting existing text

Keep the meaning and every fact. Swap vague nouns for the specifics the user gave you. Cut filler, restating, and wrap-ups. Fix the structures above. Shorten. Don't add information that wasn't there.

## Limits

This lowers the AI feel. It does not guarantee text passes a detector, and it shouldn't be sold as doing that. Trained readers and detectors catch generic content even when the words are scrubbed. The cure is real specifics and a real point of view from the user.
