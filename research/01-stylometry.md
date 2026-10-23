# 01 Stylometry and detection research: measurable AI-vs-human features

Verification note: "read" = full text or HTML fetched via WebFetch (which summarizes through a small model, so numbers are as reported by that extraction, not eyeballed from the PDF). "abstract only" = not read in full. Several PDFs returned binary and were re-fetched as HTML/PMC. Anything not verified is flagged.

## 1. Papers

### 1.1 Muñoz-Ortiz, Gómez-Rodríguez, Vilares (2024), read (PMC full text)
- Title: Contrasting Linguistic Patterns in Human and LLM-Generated News Text
- Venue: Artificial Intelligence Review (Springer), DOI 10.1007/s10462-024-10903-2. arXiv 2308.09067. https://arxiv.org/abs/2308.09067 / https://pmc.ncbi.nlm.nih.gov/articles/PMC11422446/
- Method: 13,371 NYT articles (Oct 2023 to Jan 2024) vs continuations from 6 NON-instruction-tuned models (LLaMa 7/13/30/65B, Falcon 7B, Mistral 7B), prompt = headline + first 3 words of lead, max 200 tokens, temp 0.7. Stanza parsing.
- Findings (human vs LLM range):
  - Vocabulary diversity: STTR 0.491 vs 0.424-0.466; MTLD 96.5 vs 57.4-94.6. Human higher.
  - Sentence length: no summary stats; humans have more spread and more long sentences, LLMs cluster in the 10-30 token range. Differences p<0.001.
  - POS (% tokens): auxiliaries 3.81 vs 5.41-6.02; pronouns 5.32 vs 6.11-7.33; numerals 1.77 vs 1.95-2.05; symbols 0.09 vs 0.17-0.19; nouns 19.69 vs 17.44-17.85; adjectives 7.58 vs 6.69-6.86; punctuation 11.88 vs 10.77-12.14 (roughly equal).
  - Dependencies: aux 1.91 vs 2.55-2.74; cop 1.26 vs 1.86-2.28; amod 6.98 vs 5.57-5.79; appos 1.19 vs 0.85-1.07.
  - Constituents: VP 18.08 vs 20.02-20.59; NP 42.91 vs 39.96-41.42; PP 14.12 vs 12.62-12.94.
  - Emotion: humans more fear/disgust/anger.
- Caveats (authors): English news only; base models only; 200-token cap; explanations (register leveling) are hypotheses.

### 1.2 Reinhart, Markey, Laudenbach, Pantusen, Yurko, Weinberg, Brown (2025), read (arXiv HTML v2)
- Title: Do LLMs write like humans? Variation in grammatical and rhetorical styles
- Venue: PNAS, Feb 2025, DOI 10.1073/pnas.2422455122. arXiv 2410.16107. https://arxiv.org/html/2410.16107v2
- Author list beyond Reinhart is from memory, not verified from the fetched page; cite as "Reinhart et al."
- Method: HAP-E corpus, 8,290 texts / 66,320 ~500-word chunks (academic, news, fiction, spoken, blog, TV/movie); GPT-4o, GPT-4o mini, Llama 3 8B/70B base and instruct; Biber's 66 features, Wilcoxon + Bonferroni; random forest and lasso. Replication on CAP (9,615 texts, COCA) and M4 arXiv abstracts.
- Findings (GPT-4o vs human rate): present participial clauses ~5.3x (d=1.38); nominalizations ~2.1x (d=1.23); "that" clauses as subject 2.6x; phrasal coordination 1.9x; agentless passives about half; clausal coordination avoided by GPT-4o. Instruct-tuned models: participial 2-5x, nominalizations 1.5-2x.
- Words over-represented vs human: camaraderie 162x, tapestry 155x, intricate 119x, underscore 107x, amidst 100x, palpable 95x (GPT-4o). "tapestry" in 23% of GPT-4o outputs, "amidst" in 27%. Llama instruct: unease, palpable, reminder. Obscenity >100x rarer.
- Instruction tuning, not size, drives the departure; Llama base is closest to human. Seven-way classifier 66% (chance 14%); human-vs-one-LLM 93-98%. Generalization to M4: accuracy dropped substantially; classifier trained on Llama base was at chance on GPT-3.5 text.
- Caveats: 500-word chunks, English, instruct pipelines undocumented; authors say it is not a policing tool. Their texts are mostly formal genres (conversation/short messages not covered).

### 1.3 Opara (2024), read (arXiv HTML)
- Title: StyloAI: Distinguishing AI-Generated Content with Stylometric Analysis
- Author: Chidimma Opara (Teesside). AIED 2024. arXiv 2405.10129. https://arxiv.org/abs/2405.10129
- Method: 31 features (text says 31, table lists 30) + random forest. AuTexTification (55,677 texts: tweets, reviews, how-tos, news, legal; AI = BLOOM) and Education set (200 texts: 100 ChatGPT-3.5 vs 100 Wikipedia).
- Results: accuracy 0.81 (AuTexTification), 0.98 (Education). Top importances named: UniqueWordCount, StopWordCount, TTR, HapaxLegomenonRate. The rest are unranked.
- Directions are hypothesized, not measured: human higher in stop words, hapax rate, direct address, contractions (new feature), emotion.
- Caveats: reporting inconsistencies, no cross-dataset transfer test, outdated generators, "outperforms" claim not supported on the Education set.

### 1.4 Zaitsu and Jin (2023), read (PMC)
- Title: Distinguishing ChatGPT(-3.5, -4)-generated and human-written papers through Japanese stylometric analysis
- Venue: PLOS ONE 18(8):e0288453. https://doi.org/10.1371/journal.pone.0288453
- Method: 216 texts (72 human psychology-paper excerpts of ~1,000 characters, 72 GPT-3.5, 72 GPT-4); features: POS bigrams (955), particle bigrams (533), comma positions (48), function-word rates (221); random forest.
- Results: LOO accuracy POS 95.4%, particles 92.6%, comma position 93.5%, function words 98.1%, all 100%.
- Directions not reported. Japanese only, academic only, small and homogeneous. Useful only as evidence that function-word and comma-placement patterns are highly separable in formal text.

### 1.5 Herbold, Hautli-Janisz, Heuer, Kikteva, Trautsch (2023), read (ar5iv)
- Title: AI, write an essay for me: A large-scale comparison of human-written versus ChatGPT-generated essays
- Venue: Scientific Reports 13, DOI 10.1038/s41598-023-45644-9. arXiv 2304.14276. https://arxiv.org/abs/2304.14276
- Method: 90 topics x (human, ChatGPT-3, ChatGPT-4) = 270 secondary-school argumentative essays; 111 teacher raters.
- Findings (human / GPT-3 / GPT-4): MTLD 95.7 / 75.7 / 108.9; words per sentence 18.6 / 20.3 / 19.6; nominalizations 1.06 / 1.56 / 1.73 (d 0.88, 1.35); modals 10.8 / 9.0 / 6.1; epistemic markers 0.06 / 0.02 / 0.00 (d 1.01, 1.53); discourse markers 0.57 / 0.52 / 0.36 (GPT-4 d=0.98). AI essays rated higher quality (3.69 vs 4.36 vs 4.68 on 0-6).
- Note: lexical diversity is NOT consistently lower for AI: GPT-4 was higher than humans.
- Caveats: one prompt, March 2023 models, non-native writers and raters, weak feature-quality correlations (|r| 0.12-0.22), a table/text inconsistency on syntactic depth.

### 1.6 Kobak, González-Márquez, Horvát, Lause (2024), read
- Title: Delving into ChatGPT usage in academic writing through excess vocabulary
- Venue: arXiv 2406.07016 (v2, July 2024). https://arxiv.org/abs/2406.07016
- Method: 14.4M PubMed abstracts 2010-2024, excess frequency vs counterfactual from 2021-22.
- Findings: delves r=28.0, underscores 10.9, showcasing 10.2; 2024 excess words almost all "style" words (of 319, 66% verbs, 16% adjectives), unlike content-word spikes of COVID. Lower bound of >=10% abstracts LLM-processed.
- Caveat: abstracts only; rates are about 2023-24 models and the words have since been publicized (writers/models adapt).

### 1.7 Liang, Yuksekgonul, Mao, Wu, Zou (2023), read
- Title: GPT detectors are biased against non-native English writers
- Venue: arXiv 2304.02819 (ICLR 2023 RTML workshop; later journal version not verified). https://arxiv.org/abs/2304.02819
- Method: 7 detectors on 91 TOEFL essays, 88 US 8th-grade essays, etc.
- Findings: TOEFL false-positive 61.22% avg; 8th-grade 5.19%. Flagged essays had lower perplexity. Rewriting TOEFL essays with richer words cut FPR to 11.77%; asking for simpler words raised 8th-grade misclassification to 56.65%. Self-edit prompt dropped detection of ChatGPT college essays from 100% to 13%.
- Caveats: ChatGPT-3.5 only, GPT-2-era detectors, small samples.
- Meaning: perplexity (predictability) detectors flag plain, simple, common-word writing, human or not.

### 1.8 Freeburg (2026), read; independent researcher, preprint, not peer reviewed
- Title: The Last Fingerprint: How Markdown Training Shapes LLM Prose
- arXiv 2603.27006 (March 2026). https://arxiv.org/html/2603.27006v1
- Method: 12 instruction-tuned models, 10 essay prompts, ~10k words/model/condition, with and without "prose only" instruction; human baseline 8 essays, 57,232 words.
- Em dashes per 1,000 words (unconstrained): GPT-4.1 10.62, Claude Opus 4.6 9.09, Claude Sonnet 4 8.29, Claude Haiku 3.5 7.51, DeepSeek V3 6.95, GPT-4o 4.12, Gemini 2.5 Pro 3.53, GPT-5.4 1.43, Llama 3.x 0.00. Human baseline mean 3.23 (median 3.83, range 0.33-17.12).
- Suppression: "no markdown" instruction cut Claude Opus 4.6 em dashes by 98% but GPT-4.1 only 14%, DeepSeek 22%. Explicit "no em dashes" brought GPT-4.1 from 11.51 to 3.86 (not zero).
- Caveats: essay genre, tiny human baseline, author's causal story is hypothesis. Does not report colons or semicolons.

### 1.9 Russell, Karpinska, Iyyer (2025), abstract + partial HTML read
- Title: People who frequently use ChatGPT for writing tasks are accurate and robust detectors of AI-generated text
- Venue: ACL 2025 (arXiv 2501.15654). https://arxiv.org/abs/2501.15654
- Method: 300 English nonfiction articles (<1K words), GPT-4o / Claude / o1; annotators gave explanations.
- Results: 5-expert majority misclassified 1/300; non-experts ~56.7% TPR with 51.7% FPR (chance). Pangram 98.0%, GPTZero 85.3%, Fast-DetectGPT 80.0%, Binoculars 66.7%.
- Cues cited in explanations (share of explanations): vocabulary 53.1%, sentence structure 35.9% ("not only... but also", lists of three), grammar/punctuation 24.8% (too clean), originality 23.7% ("safe"), quotes 22.3%, clarity 19.5% (over-explains). Formulaic conclusions. Names "Emily"/"Sarah" in 63-70% of articles. Humans say "says"; AI "notes/explains". Word list table was truncated; examples: vibrant, crucial, testament, delve.
- Caveats: American nonfiction, 5 experts, authors built the humanizer. Remaining ~60K characters not read.
- Meaning: heavy ChatGPT users spot it by content habits (vocabulary, structure, safeness) not by statistics.

### 1.10 Dawkins, Fraser, Kiritchenko (2025), read (first 100K chars)
- Title: When Detection Fails: The Power of Fine-Tuned Models to Generate Human-Like Social Media Text
- arXiv 2506.09975 (NRC Canada). https://arxiv.org/abs/2506.09975
- Method: 11,000 human tweets on 11 topics; 505,159 AI tweets from GPT-4o/mini, Llama-3-8B/3.2-1B, prompt vs fine-tuned (800 or 2,000 tweets); 250 MTurk raters.
- Findings: base GPT-4o tweets: more emojis (rank-biserial 0.92), longer (0.60), more contractions (0.39), fewer @mentions, lower TTR, more hashtags. Fine-tuned: these gaps nearly vanish. Humans 61.2% on base, 53.9% on fine-tuned. GPTZero ~chance on fine-tuned; best off-the-shelf ~61%. Humans relied on formal tone and emojis, which misled them on fine-tuned text.
- Caveats: X only, English, mentions/links stripped.

### 1.11 Xu and Zubiaga (2025), read (HTML), preprint
- Title: Understanding the Effects of RLHF on the Quality and Detectability of LLM-Generated Texts. arXiv 2503.17965. https://arxiv.org/abs/2503.17965
- Findings: Llama-7B base to SFT to RLHF: distinct n-gram diversity 0.42, 0.24, 0.18; detection AUROC (Fast-DetectGPT) 0.68, 0.80, 0.91 on instruction following; trained detector more sensitive to short outputs. 100 samples per class. Not uniform (QA AUROC fell 0.89 to 0.84).
- Meaning: alignment training is what makes text more repetitive and detectable.

### 1.12 Rodrigues, Sturm, Pinheiro (2026), read (first 100K chars)
- Title: A linguistic comparison between human- and AI-generated content. iScience 29(3):114976. https://pmc.ncbi.nlm.nih.gov/articles/PMC12969083/
- Method: ~200 Portuguese news articles (human true/false vs GPT-4o, Mistral Large, Llama 3.3 70B), LIWC.
- Findings (LLM vs human): informal language -54% to -72%; netspeak -32% to -84%; positive emotion +70% to +133%; certainty +111% to +152% (factual news); achievement +65% to +132%; anger -15% to -51%. Detector accuracy 93% on human, 75% on LLM. LLM text more uniform in length.
- Caveats: Portuguese, news, ~200 articles.

### 1.13 Sadasivan et al. (2023-2025), abstract only
- Title: Can AI-Generated Text be Reliably Detected? Sadasivan, Kumar, Balasubramanian, Wang, Feizi. TMLR (arXiv 2303.11156). https://arxiv.org/abs/2303.11156
- Recursive paraphrasing (~300-token passages) significantly lowers detection across watermark, neural, zero-shot, retrieval detectors. Theoretical bound: detection AUROC limited by total variation distance between human and AI distributions.

### 1.14 Kumarage et al. (2023), abstract only
- Title: Stylometric Detection of AI-Generated Text in Twitter Timelines. Kumarage, Garland, Bhattacharjee, Trapeznikov, Ruston, Liu. arXiv 2303.03697. https://arxiv.org/abs/2303.03697
- Claim: tweets are short so pretrained-LM detectors struggle; stylometric features augment them. No numbers verified (PDF unreadable).

### 1.15 Weaker or secondary sources (only snippets seen)
- Almulla (2025), Open J. Modern Linguistics 15(5), DOI 10.4236/ojml.2025.155044, read: ~40K words, ChatGPT-4o vs human essays. Hedging tokens 405.5 (AI) vs 250 (human); engagement markers 220 vs 267.5. Neither difference significant (Wilcoxon p>0.05). A "humanizing prompt" did not change hedging (404 vs 408). Author says hedging is NOT a distinctive feature.
- Tang/"CT2" (Counter Turing Test, Chakraborty et al., EMNLP 2023): snippet only; says GPTZero introduced burstiness, and newer LLM text is statistically near human. Not read in full.
- Preprints with "lower perplexity and burstiness, more consistent sentence lengths" and a Tarım and Onan diffusion-LM paper: snippets only, unverified.
- arXiv 2608.06589 ("Beyond 'AI Language': the case for the idiolectal nature of LLM output", contractions case study): PDF unreadable, findings NOT verified.

## 2. Ranked AI-tell features

Strength reflects: replicated across papers, effect size, relevance to modern instruct models. Direction is LLM relative to human.

| Rank | Feature | Direction | Evidence | Strength |
|---|---|---|---|---|
| 1 | "AI vocabulary" (delve, tapestry, intricate, underscore, showcasing, palpable, camaraderie, amidst, vibrant, crucial, testament, pivotal-type words) | LLM much more | Reinhart (95-162x), Kobak (r 10-28), Russell (53% of expert cues) | Strong, but model/era-specific and decaying as words get known |
| 2 | Noun-heavy, nominalized, information-dense prose; present participial clauses ("..., highlighting X") | LLM more (nominalization 1.5-2.1x; participials 2-5x) | Reinhart, Herbold (d 0.9-1.35) | Strong for instruct models in formal genres; untested on short chat messages |
| 3 | Safe, formulaic structure: lists of three, "not only...but also", neat concluding line, over-explaining | LLM more | Russell (35.9% structure, 19.5% clarity, formulaic conclusions) | Moderate-strong (human annotator evidence, small n) |
| 4 | Register too formal: fewer informal words, netspeak; fewer contractions (base prompting), fewer swear words | LLM more formal | Rodrigues (informal -54 to -72%), Reinhart (obscenity >100x rarer), Dawkins (mixed: base GPT-4o had MORE contractions in tweets) | Moderate; contraction direction inconsistent across registers |
| 5 | Lower vocabulary diversity / more repetition | LLM lower in most base-model and RLHF studies | Muñoz-Ortiz (MTLD 57-95 vs 96.5), Xu (distinct-ngram 0.42 to 0.18), Dawkins (lower TTR); BUT Herbold GPT-4 MTLD higher than humans | Moderate, inconsistent |
| 6 | Flat sentence-length distribution (fewer very short and very long sentences; cluster at 10-30 tokens) | LLM less variable | Muñoz-Ortiz (figure, no numbers), unverified preprints; Herbold means similar (19.6 vs 18.6) | Moderate-weak: variance claim not well quantified in verified sources |
| 7 | Em dashes | Many models more; human rate itself varies ~50x | Freeburg (GPT-4.1 10.6, Claude 7.5-9.1 vs human 3.2 per 1,000 words); Llama 0; prompts only partially suppress | Moderate for GPT-4.1/Claude, weak overall (single preprint, essay genre) |
| 8 | More auxiliaries/copulas, pronouns, numerals; fewer adjectives, appositives | LLM more aux (5.4-6.0 vs 3.8%), pronouns | Muñoz-Ortiz | Moderate (base models, news) |
| 9 | Fewer modals, epistemic and discourse markers (human "I think", "maybe", "well", "like") | LLM fewer (modals 6.1 vs 10.8; epistemic ~0 vs 0.06) | Herbold (d up to 1.5) | Moderate for 2023 models; hedging total conflicts (Almulla: AI MORE hedges, n.s.) |
| 10 | Unusually clean grammar, no typos, even punctuation | LLM cleaner | Russell (24.8% of cues) | Weak-moderate |
| 11 | Excess emotion positivity, certainty, achievement words; less anger/fear | LLM more positive and certain | Rodrigues (+70-133% positive), Muñoz-Ortiz | Moderate (news only) |
| 12 | Function-word and comma-placement fingerprints | Highly separable, direction not given | Zaitsu (92-98% accuracy), Opara (StopWordCount top-2 feature) | Strong for detection, no actionable direction |
| 13 | Colons, semicolons | No verified data | Not reported in any paper I read (Freeburg explicitly does not report) | None verified |
| 14 | Generic names ("Emily", "Sarah") and generic examples | LLM more | Russell (63-70%) | Weak-moderate, specific to news |

## 3. What this means for a writer of short work messages (inferences, not findings)

- Cut the stock vocabulary and participial "-ing" tail clauses ("..., ensuring X"). Highest-confidence tells.
- Prefer verbs over nominalizations ("we decided" not "the decision was made").
- Vary sentence length on purpose; allow a 3-word sentence and a long one. Do not end with a tidy summary or a list of three.
- Use the register of the channel: contractions, plain words, an occasional fragment. Informality was the clearest register gap in Rodrigues and in the human-rater cues, but note Dawkins found base GPT-4o tweets over-casual (emojis), so avoid performative informality too.
- Em dashes: avoid as a default; they are a model-specific tell, but humans use them too.
- Keep concrete specifics (names, numbers, ticket IDs). Generic "safe" content is a rater cue.
- Do not add hedges or "I think" for their own sake; evidence on hedging direction is mixed.

## 4. Caveats

- Almost none of this evidence is on short (<200 words) informal workplace messages. Formal genres dominate: news, essays, academic abstracts. Reinhart's own conclusion is that LLMs fail to adapt style to register, so short-message tells are probably real but unmeasured by these studies.
- Model drift: tests use GPT-3.5/4, Llama 3, BLOOM, and a few 2026 models. Word lists and em-dash rates change per model version (GPT-5.4 had 1.43 vs GPT-4.1 10.62).
- Base vs instruct: Muñoz-Ortiz used base models only, so its numbers (lower diversity, more aux) do not isolate what instruction tuning does. Reinhart shows instruction tuning drives the biggest gaps; Xu shows RLHF lowers diversity and raises detectability.
- Detection does not generalize: Reinhart's classifier fell sharply on a new generator and domain; Dawkins shows fine-tuning on ~800 tweets pushes off-the-shelf detectors to ~chance and humans to ~54%; Sadasivan shows paraphrasing breaks detectors and a theoretical limit; Liang shows 61% false positives on non-native essays and that "simple, predictable" writing is flagged. Perplexity-based detection penalizes plain writing, so "be more complex" is not the answer.
- Burstiness: widely repeated, but I found no verified paper with a measured burstiness gap for current models. Only sentence-length spread (Muñoz-Ortiz, no numbers in text; Herbold means) supports it. Treat as moderate-weak.
- Short texts: one unreviewed page claimed sentence-level variation carries almost no signal under 50 words; not verified, do not cite. Trained detectors are more sensitive to short outputs (Xu), and Kumarage says short tweets hamper PLM detectors, supporting "detection is least reliable on short text", which also means readers rely on content/voice cues, per Russell.
- Mutually inconsistent results: lexical diversity (Herbold GPT-4 higher vs Muñoz-Ortiz lower), hedging (Almulla AI higher vs Herbold epistemic markers lower), contractions (Dawkins base GPT-4o higher). A skill built on these should treat them as weak.
- Not verified: Reinhart author list beyond the first; Zaitsu feature directions; Kumarage numbers; contraction paper 2608.06589; CT2 and burstiness preprints; Russell's full AI-word table.
- Skill-design implication: rules should target content habits human readers notice (vocabulary, structure, safeness, over-explaining, register mismatch), because that is what remains detectable when statistics are gamed.
