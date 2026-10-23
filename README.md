# humanize

A Claude Code skill that makes Claude write short work messages (Slack, email, PR descriptions, status updates) the way a person would, in plain words, with real specifics, and without the habits that make text feel AI-written.

It is built on research about what actually makes text read as machine-written, not on a folklore blacklist. The evidence and its limits are in [humanize/evidence.md](humanize/evidence.md).

## Install

Claude Code reads skills from `~/.claude/skills/`.

```bash
git clone https://github.com/iamanimesh9044/humanize-skill.git
cp -r humanize-skill/humanize ~/.claude/skills/humanize
```

Start a new Claude Code session so the skill loads.

To make it apply to everything you ask Claude to write, add one line to `~/.claude/CLAUDE.md`:

```
When writing any message, email, post, or doc meant for another person, use the humanize skill.
```

## Use

Call it directly:

```
/humanize rewrite this for Slack: <paste your draft>
```

Or just ask in plain language. The skill description makes Claude pick it up for requests like:

- "Draft a message to Priya asking for the sandbox keys"
- "Write a PR description for this change"
- "Make this sound less like AI"
- "Status update for standup, I'm blocked on the API keys"

Give it real details (names, numbers, dates, file paths). The skill never invents them. If something is missing it asks or leaves a `[placeholder]`.

If you paste samples of your own writing, it copies that voice before falling back to the generic rules.

## Before and after

Input draft:

```
I wanted to reach out to inquire about the possibility of leveraging a shared repository to streamline our API contract management. This would ensure consistency across our services. Let me know if you have any questions!
```

Output with the skill, given the facts "billing, auth and notif services, auth has an extra field":

```
billing-svc, auth-svc and notif-svc each keep their own copy of the user API contract, and they've drifted (auth has an extra field). Can you check if we can move it to a shared repo?
```

## What it does

Rules, in priority order:

1. Specifics from your input, never invented
2. Answer first
3. Plain words and plain verbs
4. Uneven sentence rhythm
5. One real opinion, with a reason
6. Stop when done: no summary, no offer, no wrap-up
7. Say it once
8. Hedge once, where you're really unsure
9. Match the channel and your own voice

It also bans structures by pattern, not only words: "not just X, it's Y", runs of three, trailing "-ing" significance clauses, "serves as", vague attribution, tidy summary endings.

Output is plain text in a single code block with no tables or markdown, so it survives copy and paste into Slack or email.

Message patterns it uses (Context → Request, Status → Blocker → Next step, Options → Recommendation, SBI feedback, and more) are in [humanize/patterns.md](humanize/patterns.md).

## What it does not do

- It does not guarantee text passes an AI detector. Trained readers and detectors catch generic content even when the words are scrubbed. Real specifics from you are the fix.
- It does not add fake typos, slang or anecdotes. The research found no evidence that helps, and it can read as fake.
- It is tuned for short work messages. Almost no research measures chat-length text, so those rules are inference from long-form studies and plain-writing practice.

## Repo layout

```
humanize/
  SKILL.md       the skill (rules, patterns, output format, checklist)
  patterns.md    message patterns with examples
  evidence.md    condensed research behind the rules
research/
  01-stylometry.md              measurable features of LLM text
  02-perception.md              how human readers judge authorship
  03-vocab-rlhf.md              overused words, why they happen
  04-field-guides-evasion.md    Wikipedia's AI-writing guide, evasion studies
  05-short-form-workplace.md    short-form and workplace writing
```

## Research notes and caveats

The `research/` files were compiled with AI assistance from web sources. Some sources were read only through summaries, and several figures come from preprints or industry blogs. Each file marks what was and wasn't verified. Check the original papers before quoting any number.

Key sources include Jakesch et al. (PNAS 2023), Russell, Karpinska and Iyyer (ACL 2025), Reinhart et al. (PNAS 2025), Kobak et al. (Science Advances 2025), the Graphite "AI Tells" analysis, and Wikipedia's "Signs of AI writing" guide.

## Contributing

Issues and PRs welcome. The most useful additions are:

- Real before/after examples from short work messages
- Studies that measure chat-length or email-length text
- Tells from newer models, with a source

## License

MIT
