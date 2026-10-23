# Patterns with human examples

Names in brackets are framework origins. Examples are deliberately specific and uneven.

## Core structures

**Context → Request → Outcome** (close to BLUF)
> billing-svc, auth-svc and notif-svc all have their own copy of the user API contract, and they've drifted (auth's has an extra field). Can you check if we can move it to a shared repo? Would save us from patching three places every time.

**Problem → Solution → Benefit** (simplified SCQA)
> Each service keeps its own schema right now, which is how we shipped the v2 field to billing but forgot notifications last week. I'd move the schemas into one shared package so this can't happen again.

**Goal → Steps → Constraints**
> Need retry support for failed jobs. The current logic is in `worker/retry.py`, which only retries on timeouts. Extend it to cover provider 5xx errors, max 3 attempts with backoff. Don't change the public job API, since the mobile team depends on it.

**Observation → Question**
> Noticed we define the user schema in 3 repos. Was that intentional, or just how it grew? If it's the latter I can take a stab at consolidating.

**Status → Blocker → Next step**
> API's done and merged. Blocked on provider sandbox keys, waiting on Priya, she said EOD. Once I have them I'll run the integration suite, so probably tomorrow morning.

**What changed → Why → How to verify → Risk**
> Adds retry for jobs that fail on provider 5xx (fixes #412).
> We were losing ~2% of jobs to transient ElevenLabs errors.
> **Test:** set `FAIL_FIRST_ATTEMPT=1`, submit a job, check logs show attempt 2 succeeding.
> **Risk:** retries could double-charge if the provider actually processed the first call. I checked, and they're idempotent on request ID.

## Extra patterns

**BLUF**
> Short answer: yes, we can ship Friday. The one risk is the TTS provider migration, details below.

**No hello**
> Hey Arjun, quick one: is the staging Redis safe to flush, or is someone testing on it?

**Ask with a default and a deadline**
> Planning to go with Kafka over SQS for this. If no objections by Thursday, I'll start on it.

**Options → Recommendation**
> Two ways to do this: (a) cache at the gateway, which is quick but stale for up to 5 min, or (b) invalidate on write, which is more work but always fresh. I'd do (a) for now, since nobody's complained about staleness.

**Heads-up / FYI**
> FYI, no action needed: I'm rotating the Langfuse keys tonight, so you might see a few failed traces around 11pm.

**Polite nudge**
> Bumping this. Any thoughts on the schema PR? Happy to walk through it on a call if that's easier.

**Incident**
> Celery workers stopped picking up jobs 2:10–2:45pm. ~300 video jobs delayed, none lost. Cause: Redis hit maxmemory and started evicting queue keys. Fixed by raising the limit and setting the eviction policy to noeviction. Adding a Prometheus alert at 80% memory.

**Feedback (SBI: Situation → Behavior → Impact)**
> In yesterday's review the PR had no tests for the retry path, so I couldn't tell if the backoff worked without running it locally. Could you add one?

**Saying no**
> I'd like to help, but I'm heads-down on the voice agent launch till Wednesday. Could Dheeraj pick it up, or can it wait till Thursday?

**Disagree and commit**
> I still think a monorepo would be cleaner long-term, but I get the migration cost. Happy to go with the shared package. Let's revisit in Q1.

**Diplomatic pushback (be concrete, not vague)**
> I see why you split it, but could we just add a flag to the existing handler? Feels like less to maintain.

Weak version to avoid: "There might be a simpler approach." (passive, names nothing)

## Before / after

| AI-sounding | Human |
|---|---|
| "I wanted to reach out to inquire about the possibility of leveraging a shared repository to streamline our API contract management." | "Can we move the API contract into a shared repo? Three copies have drifted." |
| "I hope this helps! Let me know if you have any further questions." | (delete) |
| "There may be some potential considerations regarding the timeline." | "Might slip a day. Waiting on Priya's keys." |
| "Both approaches have their own merits." | "I'd go with the cache. Simpler." |
