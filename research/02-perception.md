# How human readers perceive and detect AI-written text

Scope: psychology/HCI of authorship perception, for a "humanize" skill that writes short work messages (Slack, email, PR descriptions, status updates).

Verification legend: [FULL] = I read the full paper text (or large parts via fetch/pdftotext). [ABS] = abstract/secondary summary only. [UNVERIFIED] = could not confirm; do not cite numbers without checking.

---

## 1. Studies

### 1.1 Jakesch, Hancock, Naaman (2023) [FULL]
- Title: "Human heuristics for AI-generated language are flawed"
- Authors: Maurice Jakesch, Jeffrey T. Hancock, Mor Naaman
- Venue: PNAS 120(11), e2208839120 (2023). Preprint: https://arxiv.org/abs/2206.07271 ; PMC: https://pmc.ncbi.nlm.nih.gov/articles/PMC10089155
- Method: six Turing-style experiments (3 main, 3 validation). Participants judged whether short first-person "self-presentations" (professional/job, dating, Airbnb host profiles) were human-written (real platform text) or AI-generated (fine-tuned GPT-2/GPT-3-class models). Treatments: money incentive (dating), immediate feedback/training (professional). Post-hoc: qualitative coding of explanations, computed language features, a 1,300-person labeling task, regression of features on "seems AI" vs. "is AI".
- Sample: 4,600 participants, 7,600 self-presentations total.
- Key numbers:
  - Detection accuracy 50-52% (hospitality 52.2%; incentive 51.6%; feedback/training 51.2%). No demographic group did better. Agreement between raters above chance (Fleiss kappa 0.07) = shared but wrong heuristics.
  - Self-reported reasons: content 40% (family/life experiences = human), grammar 28% (first-person pronouns, grammatical mastery = human; grammar errors read as "bad AI" by some, "fallible human" by others), tone 24% (warm/genuine = human, impersonal/monotonous = AI).
  - Separate labelers: AI text rated nonsensical more often (13.6% vs 9.6%), more repetitive (12.7% vs 7.1%), and with FEWER grammar issues (14.8% vs 19.6%). A classifier on just "nonsensical or repetitive" would reach 58.8% accuracy vs participants' 51.7%.
  - Cue validity (odds ratios): nonsense content seen as AI +10.5% and truly +23% more likely AI (valid). Repetition seen as AI +8%, truly +47% (valid, under-used). Grammar issues seen as AI +5% but truly 15% LESS likely AI (inverted). Long words / rare bigrams read as AI, but mostly human-written (inverted). First-person pronouns and family content read as human but were NOT associated with either source (no validity). Longer text, "spontaneous" words, past-event focus read as human, also no real association.
  - Models trained on participants' judgments predicted them at 57.6% (regression) and 58.1% (LM classifier).
  - "More human than human": AI text optimized against those heuristics was judged human 65.7% of the time vs 51.6% for ordinary AI text and 51.7% for real human text (p<0.0001); up to 71% in the professional context.
- Authors propose "AI accents" as a mitigation; note heuristics could shift as models change.
- Caveat for us: stimuli were older GPT-2/3-era models writing about the self. Modern chat models have different tells (see 1.3).

### 1.2 Clark et al. (2021) [FULL via ar5iv]
- Title: "All That's 'Human' Is Not Gold: Evaluating Human Evaluation of Generated Text"
- Authors: Elizabeth Clark, Tal August, Sofia Serrano, Nikita Haduong, Suchin Gururangan, Noah A. Smith
- Venue: ACL 2021 (Outstanding Paper), pp. 7282-7296. https://aclanthology.org/2021.acl-long.565 ; arXiv 2107.00061 (note: arXiv 2107.01408 is a different paper; I hit that by mistake)
- Method: crowdworkers judged whether stories, news articles, recipes were human- or machine-written (GPT-2 XL, GPT-3 davinci). Study 2 tested three quick trainings: instructions, annotated examples, paired comparison. Coded 300 free-text comments.
- Sample: Study 1 780 evaluators, 3,900 ratings; Study 2 1,170 evaluators, 5,850 ratings; 50 texts per domain per source.
- Numbers: GPT-2 text identified at 58% overall (stories 62, news 57, recipes 55). GPT-3 at 50% (stories 48, news 51, recipes 50) = chance. Training on GPT-3: instructions 52%, examples 55% (only significant gain, not significant per domain), comparison 53%. Krippendorff alpha <=0.11.
- Cues cited: form 47% of labels vs content 25%. Spelling/grammar/punctuation most common (45 of 150 comments), then style/tone (24). Also repetition, factuality, common sense, coherence. 28.3% of untrained comments were beliefs about machine capability ("machines can't do emotion, humor, intent"). After example training: form fell to 32.5%, content rose to 50%, capability beliefs fell to 17.5%.
- Key finding: formality, grammar errors, clarity each cited as evidence for BOTH human and machine. Readers underestimate what models can do.

### 1.3 Russell, Karpinska, Iyyer (2025) [FULL for experiment results; read most of paper via fetch]
- Title: "People who frequently use ChatGPT for writing tasks are accurate and robust detectors of AI-generated text"
- Authors: Jenna Russell, Marzena Karpinska, Mohit Iyyer
- Venue: ACL 2025 (long), pp. 5342-5373. https://aclanthology.org/2025.acl-long.267 ; https://arxiv.org/abs/2501.15654
- Method: 300 English non-fiction articles; five experiments of 60 articles (30 human, 30 AI) from GPT-4o, Claude-3.5-Sonnet, o1-Pro, plus paraphrased GPT-4o and "humanized" o1-Pro. Nine annotators (4 non-expert, 5 "expert" = frequent LLM writing users) labeled and wrote paragraph explanations. Compared to commercial/open detectors.
- Numbers (as reported in the fetched text; the paper itself has minor internal inconsistency in total annotation count, 1,790 vs 1,740):
  - Non-experts (Exp 1, GPT-4o): TPR 56.7%, FPR ~52% = chance; confidence 4.03/5.
  - Experts: TPR 92.7%, FPR ~3-4%; confidence 4.39/5. Expert majority vote 100% on GPT-4o and Claude; overall 99.3% TPR, 0% FPR, 1 of 300 articles misclassified.
  - Individual expert TPR: 96.7, 88.0, 59.3, 97.3, 93.3. Annotator 3 (59.3%) was fooled by o1-Pro (0% on humanized) because she treated informality (contractions, slang) as proof of a human.
  - Detectors: Pangram 98.0% TPR / 2% FPR; GPTZero 85.3 / 0.7; Fast-DetectGPT 80.0 / 7.2; Binoculars 66.7 / 1.3; RADAR 15.3 / 2.
  - Paraphrasing and "humanizing" did NOT reduce expert accuracy; paraphrased text drew more "AI vocabulary" flags (88% of correct explanations vs 69.8% unparaphrased). Humanized text overused titles like "Dr."/"Prof.".
  - Clue categories in expert explanations: vocabulary 53.1%, sentence structure 35.9%, grammar/punctuation 24.8%, originality 23.7%, quotes 22.3%, clarity 19.5%, formatting ~15%, conclusions 13.1%, tone 9.3%, introductions 7.3%.
  - 31% of expert false-positive explanations cited vocabulary ("AI-sounding" words in human text).
- Caveat: n=5 experts, one genre (long non-fiction articles, ~hundreds of words). Short work messages give much less signal. Casal & Kessler (below) suggest short genres are hardest.

### 1.4 Köbis & Mossink (2021) [partial: read much of preprint]
- Title: "Artificial intelligence versus Maya Angelou: Experimental evidence that people cannot differentiate AI-generated from human-written poetry"
- Authors: Nils Köbis, Luca D. Mossink
- Venue: Computers in Human Behavior 114, 106553 (published online 2020/vol dated 2021; the search result said 2020; check). arXiv 2005.09980 https://arxiv.org/abs/2005.09980
- Method: incentivized Turing test (pay for correct identification). GPT-2 completed human-written poem openings. Study 1 N=~200 judges (192 after exclusion), Study 2 ~400; total 830 incl. writers. Study 2 varied whether a human picked the best AI poem (human-in-the-loop, HITL) or random (HOTL), and whether origin was disclosed.
- Numbers: Study 1 detection accuracy 50.21% (95% CI 46.4-53.9), Bayes factor 24.91 in favor of chance. Confidence mean 62.27/100 with no relation to actual performance (unincentivized estimates). Study 2: HITL at chance; HOTL above chance (mean 5.94/10 rounds correct, d=0.47). In Study 2 the incentivized confidence estimates did not exceed actual accuracy (overconfidence did not replicate). Preference for human poems persisted (slight algorithm aversion), regardless of disclosure. Study 1 human win share 56.97%.
- Takeaway: a human curating/editing AI output removes detectability. Unedited, raw AI output is more detectable.

### 1.5 Gunser et al. (2022) [ABS only]
- Title: "The Pure Poet: How Good is the Subjective Credibility and Stylistic Quality of Literary Short Texts Written with an Artificial Intelligence Tool as Compared to Texts Written by Human Authors?"
- Authors: Vivian Emily Gunser, Steffen Gottschling, Birgit Brucker, Sandra Richter, Dilan Canan Cakir, Peter Gerjets
- Venue: Proceedings of the First Workshop on Intelligent and Interactive Writing Assistants (In2Writing 2022), pp. 60-61. https://aclanthology.org/2022.in2writing-1.8 (2-page workshop abstract; also CogSci paper)
- Method/sample: two studies, N=120 and N=302, readers saw 9 AI continuations vs 9 human or original continuations of classic literary openings.
- Findings: low accuracy at telling source, overconfident; AI continuations rated lower on well-written, inspiring, fascinating, interesting, aesthetic. I did not read full text; no accuracy numbers verified.
- Note: this shows people can fail to detect source yet still rate AI text as less good on style. Detection and quality perception are separable.

### 1.6 Jakesch, Bhat, Buschek, Zalmanson, Naaman (2023) [ABS only]
- Title: "Co-Writing with Opinionated Language Models Affects Users' Views"
- Venue: CHI 2023, DOI 10.1145/3544548.3581196; https://arxiv.org/abs/2302.00560
- Method: online experiment, N=1,506 wrote a post on whether social media is good for society with an assistant biased pro or con; N=500 judges.
- Finding: assistant shifted both text written and the writers' later attitudes. Not a detection study; relevance to us is indirect (AI drafts nudge the writer's content/stance, so a human should check the claims). Treat as peripheral.

### 1.7 Jakesch, French, Ma, Hancock, Naaman (2019) [partial: read part of paper]
- Title: "AI-Mediated Communication: How the Perception that Profile Text was Written by AI Affects Trustworthiness"
- Venue: CHI 2019, DOI 10.1145/3290605.3300469; https://s.tech.cornell.edu/assets/papers/aimc.pdf
- Method: three MTurk experiments rating Airbnb host profiles for trustworthiness (Study 1 n=527, Study 2 n=286, Study 3 n=323; Study 3 pretest n=80).
- Finding: the "Replicant Effect": hosts whose profiles were labeled or suspected AI-written were trusted less, but ONLY in a mixed environment (some AI, some human). If everyone was told all profiles were AI-written (or all human), no penalty. Mixed-source environments made participants scrutinize minimal cues. In Study 2, the more a participant believed a profile was AI, the lower the trust.
- Interviewer comments (secondary): disjointed profiles assumed AI, spelling errors assumed human. [ABS]

### 1.8 Hohenstein et al. (2023) [FULL via PMC fetch]
- Title: "Artificial intelligence in communication impacts language and social relationships"
- Authors: Jess Hohenstein, Rene F. Kizilcec, Dominic DiFranzo, Zhila Aghajari, Hannah Mieczkowski, Karen Levy, Mor Naaman, Jeffrey Hancock, Malte F. Jung (author list from memory/search listing; Hohenstein first, Jung last, Hancock/Naaman included; verify full list)
- Venue: Scientific Reports 13, 5487 (2023), DOI 10.1038/s41598-023-30938-9; https://pmc.ncbi.nlm.nih.gov/articles/PMC10073210
- Method: two randomized experiments of paired chat (MTurk, custom messenger, Google smart replies; Study 2 added positive/negative smart reply sets). Study 1 219 pairs; Study 2 291 pairs. Total n=1,036 reported.
- Numbers: Smart-reply availability raised messages/minute ~10.2%. Greater partner actual use improved cooperation and affiliation ratings (b=15.66, p=.018; b=21.79, p=.007). BUT perceived partner smart-reply use, controlling for actual use, lowered cooperation (t=-9.89, p<.0001) and affiliation (t=-6.90, p<.0001) and raised perceived dominance. Perceived use correlated only r=0.22 with actual use. Positive-sentiment replies increased positive language; negative ones decreased it.
- Takeaway: suspicion of AI hurts perceived warmth/cooperation independent of whether AI was used, and suspicion is only weakly tied to reality.

### 1.9 Hohenstein & Jung (2020) [UNVERIFIED details]
- Title: "AI as a moral crumple zone: The effects of AI-mediated communication on attribution and trust"
- Authors: Jess Hohenstein, Malte Jung. Venue: Computers in Human Behavior (2020). Only a Cornell lab listing page was returned (https://interplay.infosci.cornell.edu/ai-as-a-moral-crumple-zone). I did not read abstract or results; I recall that AI absorbed blame for negative outcomes and the human partner was trusted more, but I did NOT verify. Do not cite numbers.

### 1.10 Cardon & Coman (2025) [secondary only; paper behind 403]
- Title: "Professionalism and Trustworthiness in AI-Assisted Workplace Writing: The Benefits and Drawbacks of Writing With AI"
- Authors: Peter W. Cardon, Anthony W. Coman. Venue: International Journal of Business Communication (SAGE), 2025, DOI 10.1177/23294884251350599 (DOI from a secondary article). News: https://news.ufl.edu/2025/08/writing-ai-work/ ; https://www.psypost.org/managers-who-use-ai-to-write-emails-seen-as-less-sincere-caring-and-confident/
- Method: survey experiment, US full-time professionals (computer-based work), eight randomized scenarios, congratulatory email to a team, sender = respondent or supervisor, AI involvement from light editing to mostly AI-written; some high-AI versions showed the prompt.
- Sample: PsyPost says 1,158; UF/HR press says "1,100". Unresolved. Use "about 1,100".
- Numbers (secondary): supervisor seen as author of low-AI message 93% vs 25% for high-AI without prompt; sincere ~80%+ (low AI) vs ~40% (high AI); professional 95% (low AI) fell to 69-73% under heavy AI (UF figure). High-AI messages were still rated clear, professional, sometimes more effective. Self-vs-other asymmetry: people judge their own AI use more kindly than a supervisor's. Relational/emotional messages seen as less appropriate for AI than factual updates/reminders. Only congratulatory emails were tested.

### 1.11 Kadoma, Metaxa, Naaman (2025) [FULL via pdftotext]
- Title: "Generative AI and Perceptual Harms: Who's Suspected of using LLMs?"
- Venue: arXiv 2410.00906 (v3 Mar 2025). https://arxiv.org/abs/2410.00906 (preprint; venue publication not verified)
- Method: three Prolific experiments (usable n = 334, 334, 272) rating mock freelancer press-release writing samples for AI suspicion, quality, hiring. "AI-inducing" versions: human-written text edited to add verbose language, vivid description, and thesaurus-swapped rarer synonyms (using the Jakesch heuristics).
- Findings: AI suspicion lowered quality ratings and hiring likelihood across groups (p<0.001); men freelancers suspected more (42.2% vs 35.3%, p=.037); the AI-inducing style raised suspicion, especially for men. Mixed support for demographic harm.
- Takeaway: readers punish suspected AI use even when the text is human-written; verbose, ornate synonym-swapped prose triggers suspicion.

### 1.12 Casal & Kessler (2023) [ABS / secondary]
- Title: "Can linguists distinguish between ChatGPT/AI and human writing?: A study of research ethics and academic publishing". Research Methods in Applied Linguistics 2(3). https://digitalcommons.memphis.edu/facpub2/10
- N=72 journal reviewers/editors; positive identification rate 38.9% on research abstracts; no one got all four right; their stated reasons were confident but inconsistent. Authors argue short genres are hardest to tell apart. [secondary coverage]

### 1.13 Fleckenstein et al. (2024) [ABS only]
- Title: "Do teachers spot AI? Evaluating the detectability of AI-generated texts among student essays". Computers and Education: Artificial Intelligence 6, 100209. DOI 10.1016/j.caeai.2024.100209.
- N=89 novice + 200 experienced teachers; neither group reliably identified ChatGPT essays; both overconfident. Per-group rates (45.1% pre-service, 37.8% experienced) came from a secondary blog: [UNVERIFIED].

### 1.14 Porter & Machery (2024) [FULL via PMC]
- Title: "AI-generated poetry is indistinguishable from human-written poetry and is rated more favorably". Scientific Reports 14, 26133. https://pmc.ncbi.nlm.nih.gov/articles/PMC11564748
- Study 1: 1,634 participants, 10 poets, 100 poems (ChatGPT-3.5 imitating poets). Accuracy 46.6% (below chance); AI poems judged "human" more than real human poems; Fleiss kappa 0.005; higher confidence slightly predicted being wrong. "Doesn't make sense" appeared 144 times for human poems vs 29 for AI poems. Study 2: 696 participants rated 14 qualities; AI poems rated higher on quality (d=0.67), rhythm (d=0.85) etc.; telling people a poem was AI lowered ratings (d=-0.51) regardless of true source.
- Author explanation: AI poems are simpler and more accessible; readers read the harder, more complex human poems as "AI-like incoherence". A second "more human than human" case.

### 1.15 Other relevant items
- Kobak et al. (2024/25), "Delving into LLM-assisted writing in biomedical publications through excess vocabulary", arXiv 2406.07016 [ABS]: excess-word analysis of ~14-15M PubMed abstracts; style words (e.g., "delves", "showcasing", "underscores") spiked after LLMs; lower-bound 10% of 2024 abstracts LLM-processed, up to 30% in some subcorpora. Supports vocabulary as a real tell, at population level.
- "Almost AI, Almost Human: The Challenge of Detecting AI-Polished Writing" (arXiv 2502.15666, ACL Findings 2025) [ABS]: detectors flag lightly polished text as AI. About detectors, not humans.
- AI apology literature (several 2022-2026 studies, e.g., Computers in Human Behavior vol. 140, 107592 on AI-mediated apology in multilingual work context) [ABS via search summary, sample sizes UNVERIFIED]: AI-attributed apologies seen as less sincere; self-disclosure of AI use did not improve perceived authenticity; limited use (translation/grammar fixes) mitigated the penalty.
- Not found / not verified: any rigorous "uncanny valley of text" study. The search turned up no direct test. Treat "too perfect = uncanny" as a hypothesis supported only indirectly (polish is a weak cue; experts say formal/flawless prose tends to be AI; lay readers think the opposite).

---

## 2. Cue tables

### 2a. Cues that actually correlate with AI text and readers notice or can learn to notice

| Cue | Evidence | Strength |
|---|---|---|
| "AI vocabulary": tapestry, testament, delve, landscape, realm, crucial, pivotal, robust, seamless, underscores, navigate, "it's important to note", "in conclusion", "not only...but also", "when it comes to" | Russell 2025 (experts' top cue, 53%; word list in their Table 12); Kobak 2024 population-level excess words | Strong (experts + corpus data). Note it is a cue for frequent LLM users, not general readers |
| Repetition (restating same point, repeated phrasing) | Jakesch 2023: +47% truly AI, but readers only used it a bit (+8%) | Moderate-strong, under-used by laypeople |
| Nonsense / generic content that says nothing specific | Jakesch 2023 (+23% truly AI); Russell: AI lacks specific verifiable claims (names, places, figures), is "safe", obvious answer | Moderate-strong |
| Uniform, consistent formatting: bold-header bullets with colons, same-length paragraphs, repetitive headers | Russell 2025 (experts ~15%) | Moderate (single study, n=5 experts, long articles) |
| Rhetorical templates: lists of exactly three, "not only X but also Y", neat summarizing conclusion, uniformly upbeat tone ending | Russell 2025 | Moderate |
| Complex stacked-clause sentences with little length variation; formal, flowery register | Russell 2025 | Moderate |
| Homogeneous voice (everyone quoted sounds the same, same formality) | Russell 2025 (22.3% cited quotes) | Moderate |
| Stock names (Emily, Sarah) | Russell: ~63% GPT-4o and 70% Claude articles; only one annotator noticed | Weak-moderate (specific to fiction/example names; may matter for example data in work writing) |
| Ornate verbose language / thesaurus-style synonyms | Kadoma 2025 raised suspicion (even on human text) | Moderate for triggering suspicion; validity vs real AI text: inverse in Jakesch 2023 (long/rare words were more human) so it is a "trigger" not a "tell" |
| Overall absence of grammar errors / flawless polish | Jakesch 2023: AI had fewer grammar issues (14.8% vs 19.6%); Russell: AI follows grammar strictly; Casal & Kessler | Moderate as a real statistical difference; weak as a reader-detectable cue because laypeople read perfection as human |
| Disclosure or visible prompt | Cardon & Coman: authorship credited to supervisor drops 93% to 25% when high-AI | Strong that it changes attribution (not a text cue) |

### 2b. Cues readers THINK signal AI (or human) but don't, or even invert

| Believed cue | Evidence | Strength |
|---|---|---|
| Grammar errors = AI / "bad machine" (and also = human; contradictory) | Jakesch 2023: seen as AI +5% but truly 15% LESS AI; Clark 2021: contradictory use; Jakesch 2019 interviews: spelling errors = human | Strong (multiple studies) that it is unreliable |
| Perfect grammar = human | Jakesch 2023; Clark 2021 | Strong that this is wrong for modern LLMs |
| First-person pronouns ("I", "my") = human | Jakesch 2023: no association with true source. Exploitable | Strong (large N) |
| Family/personal life topics = human | Jakesch 2023: no association; exploitable | Strong |
| Long/rare words = AI | Jakesch 2023: those texts were mostly human. Experts partly agree on vocabulary but at the level of specific words, not rarity in general | Strong for the generic form |
| Informality (contractions, slang) = human | Russell 2025: Annotator 3 fooled by o1-Pro; humanized text still caught by most experts. Jakesch: contractions heuristic reported in abstract | Moderate-strong (informality is easily imitated by the model) |
| Incoherence / "doesn't make sense" = AI | Porter & Machery 2024: human poems got 144 "doesn't make sense" vs 29 for AI; Jakesch 2023 nonsense is valid for old GPT but modern models rarely do this | Strong that it misleads for modern models and for hard human writing |
| Warm, genuine tone = human; impersonal/monotonous = AI | Jakesch 2023 self-reported cue (24% of reasons). Not shown valid. Modern LLMs default to warm/upbeat; Russell experts say AI tone is consistently positive and flat | Moderate (reader belief is real; validity unclear) |
| "Machines can't do emotion, humor, intent" | Clark 2021: 28.3% of untrained comments | Moderate-strong |
| Confidence in own ability | Jakesch, Clark, Fleckenstein, Gunser, Porter all report accuracy near chance with high confidence; Köbis Study 1 confidence uncorrelated with accuracy (not replicated in incentivized Study 2); Porter: higher confidence slightly worse | Strong |
| Simplicity/accessibility signals human | Porter & Machery 2024: simpler AI poems were judged human; complex human poems judged AI | Moderate (poetry only) |

### 2c. Consequence cues (not about style, about suspicion)
- Suspected AI use lowers perceived cooperation, affiliation, sincerity, and hiring odds (Hohenstein 2023; Jakesch 2019; Kadoma 2025; Cardon & Coman 2025).
- Perceived and actual AI use are weakly related (r=0.22 in Hohenstein), so the penalty lands on people who did not use AI too.
- Penalty is largest for relational/emotional messages (Cardon & Coman, apology studies) and smaller for transactional/informational ones.
- Disclosure does not neutralize it (apology studies; unverified details). Light-touch use (grammar/translation) is penalized less.

---

## 3. What expert detectors say they look for (Russell et al. 2025)
- Specific AI vocabulary (53% of explanations; list above). Phrases like "it's important to note", "in conclusion", "paving the way".
- Sentence-level rhythm: "not only...but also", triples, long multi-clause sentences, little variation in sentence length (humans mix simple, compound, complex).
- Perfect, uniform grammar and punctuation, a very formal register, stylistic polish that stays constant.
- Originality: AI is "safe," goes for the obvious angle, avoids controversy and mild profanity, lacks surprise or humor, "bored" the annotators. Humans produce odd analogies and creative phrasing.
- Specificity/verifiability: human non-fiction has names, places, figures, checkable claims. AI is vaguer.
- Tone: neutral to positive, reflective, upbeat especially near the end; little emotional range.
- Introductions: generic scene-setters; conclusions: tidy, repetitive summaries of the whole piece, over-optimistic. Human pieces end more abruptly.
- Formatting: consistent headings, bold-colon bullets, similar paragraph lengths.
- Quotes all in the same formal voice.
- Experts were fooled when they used informality as a proxy for human (Annotator 3). Expert false positives usually came from "AI-sounding" vocabulary in genuine human text.
- Experts' skill came from exposure, not training: they were not trained or given feedback. Clark 2021 found short trainings gave little improvement, so we cannot assume ordinary readers can learn this quickly. Yet the audience for work messages is increasingly heavy LLM users (the "experts"), so the expert cues matter more for our skill than lay heuristics.

---

## 4. Implications for how to write (for the humanize skill)

Evidence-based, ordered by strength.

1. Target the cues that are REAL, because frequent LLM users catch them and paraphrasing/"humanizer" tricks don't hide them:
   - Remove the AI-vocabulary list (delve, tapestry, landscape, realm, robust, seamless, pivotal, crucial, underscores, navigate, leverage-type words, "it's important to note", "in conclusion/summary", "additionally/moreover", "not only X but also Y", "when it comes to"). Russell shows paraphrasing leaves these in.
   - Cut restatement and summary closers. Stop when the content stops. End abruptly, not with a neat wrap-up or upbeat sign-off.
   - Avoid rule-of-three lists and parallel template structures. Vary sentence length; allow fragments and short sentences.
   - Don't format short messages like documents (no bold-colon bullet lists, no headers, no uniform paragraphs) unless the content is genuinely list-shaped.
   - Be specific: real names, ticket numbers, file names, dates, numbers, a concrete reason. Vague, safe, generic claims were the second major expert cue and the main valid layperson cue (nonsense/repetition).
   - Add a point of view or a minor non-obvious detail (originality). Avoid the "obvious" framing and uniformly positive tone. Don't hedge everything or praise everything.
   - Avoid AI-typical example names (Emily, Sarah) and the "Dr." / "Prof." overuse in generated sample content.
2. Do NOT rely on the lay heuristics, because they are invalid and the experts don't fall for them:
   - Don't sprinkle in typos or deliberate grammar errors as a "humanizing" trick. Evidence says errors don't indicate human authorship reliably, and Russell's expert who relied on informality was the one fooled; the rest weren't. Casual register is fine when natural for Slack; faking mess is not an evidence-based strategy.
   - Don't add first-person pronouns, family or personal anecdotes, or contractions merely to look human. They're exploitable for naive readers (Jakesch showed gains up to 71% "human") but carry no validity, are unreliable for experts, and in a work message invented personal detail would be fabrication.
   - Don't swap in rare/long words or thesaurus-style synonyms. That specifically raised AI suspicion (Kadoma) and is the opposite of plain writing. Plain, short, common words are both more human-reading and consistent with the "plain words" brief.
3. Beware over-optimizing for "perceived human": Jakesch's "more human than human" result means you can game naive readers, but that is a deception-flavored goal. For work messages the better goal is: sound like one specific, busy colleague, with content that is true and specific. Since the skill should not invent facts, specificity must come from the real inputs.
4. Suspicion has a real cost, mainly for relational messages. Warmth, thanks, apology, praise, feedback, and conflict messages carry the biggest sincerity penalty when readers think AI wrote them (Cardon & Coman, apology studies, Hohenstein). Status updates, PR descriptions, and routine info messages are more tolerated. Therefore: keep AI-assistance visibly light on relational messages; keep the writer's own words, concrete references, and real stakes; avoid generic gratitude/praise phrasing ("I wanted to take a moment to express my sincere appreciation").
5. Short messages are the hardest genre to attribute (Casal & Kessler; Jakesch's short profiles near chance), so the best defense is brevity: fewer sentences, fewer chances to show templated structure. But for heavy-LLM-user readers, tells like "I hope this finds you well", "Great question!", "Certainly!", "Let me know if you have any questions" are very likely to be caught. These specific greeting/closing formulas were not tested in the papers; they're inferred from the vocabulary/structure findings. [inference, not tested]
6. Consistency across the message matters. Keep register consistent with the channel and the writer's usual voice: readers (esp. the Replicant Effect in mixed environments) scrutinize minimal cues and compare against known baselines. A message that is much more polished than the sender's usual Slack voice is a mismatch (inference from Jakesch 2019 mixed-source finding; not directly tested for workplace text).
7. Don't promise that disclosure fixes anything: evidence shows disclosure doesn't reliably recover trust, and light-touch use is penalized less. The skill's job is the style, not the disclosure policy.
8. A human edit pass materially reduces detectability: Köbis & Mossink found that human curation of GPT-2 output brought detection to chance, while random AI output was detectable. So the skill should encourage the user to edit in own words, rather than ship the first draft.
9. Quality and detection are separable (Gunser; Porter & Machery): readers may not identify text as AI yet still rate it as bland. Aim for substance, not only disguise.

---

## 5. Gaps and flags
- Hohenstein & Jung 2020 (moral crumple zone): findings not verified.
- Cardon & Coman: read via press/PsyPost only; sample size conflicting (1,100 vs 1,158); exact percentages should be checked in the SAGE paper (403).
- Gunser et al.: abstract only; no numbers.
- Fleckenstein: per-group accuracy numbers unverified.
- Köbis & Mossink: venue year (2020 online vs 2021 volume) not resolved; HITL accuracy number not extracted.
- Hohenstein 2023 full author list not verified.
- Jakesch 2019: numbers beyond sample sizes not extracted.
- AI-apology studies: only search-summary level; sample sizes and exact effects not verified.
- No study found that directly tests: modern (2024-26) chat-model text in short Slack/email messages with human detection; or an "uncanny valley of text" effect. The cue lists for modern models come mainly from one study (Russell et al., n=9 annotators, long articles) plus corpus-level word-frequency evidence. Jakesch/Clark/Köbis stimuli used GPT-2/GPT-3-era models and should not be assumed to transfer to current models.
- The "stock greeting/closing phrase" cue claim and "register mismatch with sender's usual voice" are my inferences.
