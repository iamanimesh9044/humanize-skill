# Evidence behind the rules

Condensed from five research passes. Full notes with sources are in `research/` at the project root. Source quality varies. Items marked (secondary) were read via summaries only. Treat numbers as approximate.

## Can people tell?

- Casual readers are near chance (about 47-52%) across studies: Jakesch et al. PNAS 2023 (n=4,600), Clark et al. 2021, Köbis 2021, Porter & Machery 2024.
- Frequent LLM users do much better. Russell, Karpinska, Iyyer, ACL 2025: expert majority vote missed 1 of 300 articles. Paraphrasing and "humanizing" did not beat them. Only 5 experts, long articles.
- So: fooling casual readers is easy and not the goal. Writing that holds up with a skilled reader needs real specifics and structure fixes.

## What experts actually key on (Russell et al. 2025)

- AI vocabulary (about 53% of explanations)
- Sentence structure (about 36%): "not only...but also", triads, uniform length
- Over-explaining, "safe" generic content, quotes where every speaker sounds alike
- Neat upbeat summary endings, uniform formatting

## Folk cues that are wrong

- Grammar errors read as AI, but were about 15% less likely to be AI.
- First-person pronouns and family topics read as human, but showed no real link.
- Informality fooled the one expert who relied on it.
- "Doesn't make sense" read as AI, but human text got more of those comments.
- Em dashes, curly quotes, "perfect grammar", formal tone, and isolated transition words are weak or model-specific.
- Text tuned to casual readers' wrong cues was judged human 65.7% vs 51.7% for real human text. That is gaming, not good writing.

## Strong structural tells

- Negative-parallelism templates: about 100-576x human rate in every model (Graphite AI Tells, 10k human vs 90k AI articles, 9 models; industry source)
- Present participial "-ing" clauses: about 2-5x human. Nominalizations: about 1.5-2.1x. (Reinhart et al. PNAS 2025, about 500-word text)
- Instruction-tuned models overuse "tapestry"-type words 95-162x and underuse informal words and profanity. Base models are close to human, so the voice comes from post-training. (Reinhart; Juzek & Ward)
- Copula avoidance ("serves as", "boasts"), significance inflation, vague attribution, assistant leftovers (Wikipedia "Signs of AI writing", WikiProject AI Cleanup)
- Lower lexical diversity and more repetition: moderate and inconsistent across models.
- Flat sentence-length distribution: widely repeated, no verified measure for current models.

## Words

- Kobak et al., Science Advances 2025: 379 excess style words in 2024 PubMed abstracts, 66% verbs. delves 28x, underscores 13.8x, showcasing 10.7x. At least 13.5% of 2024 abstracts LLM-processed.
- Liang et al.: meticulous 34.7x, intricate 11.2x, commendable 9.8x in ICLR 2024 reviews.
- Words decay. "delve" fell after it became known. 55-72% of tells are unique to one model version (Graphite). So ban structures, treat word lists as examples.

## Why it happens

- Post-training (RLHF and instruction tuning), not pretraining. Rater preference for typical text is the best mechanism (Zhang et al. 2025, preprint). Training-data frequency is ruled out (Juzek & Ward).
- RLHF lowers output diversity (Kirk et al.). Writing with feedback-tuned models homogenizes essays (Padmakumar & He).

## Human tells found in data (Graphite)

First person, specific anecdotes, casual qualifiers ("pretty", "sort of"), parenthetical asides, occasional exclamation marks. The skill must only use these if they come from the user's real input. Never fabricate.

## Trust cost of suspected AI

- Perceived AI use lowers cooperation and affiliation ratings (Hohenstein et al. 2023). Perceived use correlates weakly (r=0.22) with actual use.
- Sincerity ratings dropped from about 80% to about 40% under heavy AI use in workplace messages, worse for relational messages (Cardon & Coman 2025, secondary).
- Ornate, thesaurus-swapped prose raised suspicion even for human text (Kadoma 2025).
- Disclosure did not restore trust in apology studies (secondary).

## Detectors and evasion

- Detection doesn't generalize across generators and drops after paraphrasing or self-edit prompts. Perplexity-based detectors flagged about 61% of non-native essays as AI (Liang).
- Plain paraphrasing helps little. Detector-guided paraphrasing helps a lot but costs quality (secondary).
- No evidence that prompting makes text read better to humans.

## Short-form gap

- No study measures Slack-length or email-length text. Detection thresholds reported range from about 10 to 500 words, mostly second-hand.
- Rules for chat length are inference from long-form studies plus plain-language practice.
- BLUF, SCQA, SBI, no-hello: no controlled workplace experiments. Defaults only.
- Few-shot samples of the user's own writing likely beat style descriptions, but no controlled comparison found. LLMs imitate email and news style better than informal blog and forum style (Wang et al., EMNLP 2025).

## Known unverified items

Cardon & Coman details (paper returned 403), Hohenstein & Jung 2020, Gunser 2022 numbers, Kumarage numbers, Graphite 2026 data on newest models (single industry source), and several dates for models after 2025. Check originals before quoting numbers.
