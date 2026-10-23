# 03 - Vocabulary, RLHF, mode collapse, homogenization

Research date: 2026-10-23. Papers marked FULL were downloaded and read as full text. Others were read via abstract page or secondary summary and are marked as such. Anything I could not verify is tagged [UNVERIFIED].

Important framing for the skill: nearly all hard quantitative word data is from scientific abstracts (PubMed, arXiv) and creative writing. There is no peer-reviewed word-frequency study of Slack/email/PR text. Word lists are therefore transferable as "what the model reaches for", not as measured frequencies in work messages.

---

## 1. Sources

### 1.1 Kobak et al. - excess vocabulary (FULL)
- Title: "Delving into LLM-assisted writing in biomedical publications through excess vocabulary" (arXiv v1 title was "Delving into ChatGPT usage in academic writing through excess vocabulary").
- Authors: Dmitry Kobak, Rita Gonzalez-Marquez, Emoke-Agnes Horvat, Jan Lause. 2024 preprint (v5 Jul 2025). Published in Science Advances 11(27), 2 Jul 2025, doi 10.1126/sciadv.adt3813.
- URL: https://arxiv.org/abs/2406.07016
- Method: 15.1M English PubMed abstracts 2010-2024. For each word, observed 2024 frequency p vs counterfactual q extrapolated linearly from 2021-2022 frequencies. Excess ratio r = p/q, gap delta = p - q. Excess word = delta > 0.01 or r above a frequency-dependent threshold. Manually labelled content vs style words.
- Key numbers:
  - delves r = 28.0; underscores r = 13.8; showcasing r = 10.7 (plus inflections).
  - Common words by gap: potential delta = 0.052; findings 0.041; crucial 0.037.
  - 379 excess style words in 2024. 66% verbs, 14% adjectives. Pre-2024 excess words were mostly content nouns (79.2% nouns). Covid-era excess was content words (coronavirus etc.).
  - 454 excess words in 2024 (counting inflections), 343 unique lemmas, vs peak 190 words / 180 lemmas in 2021 (Covid). Before 2020, no word had delta > 0.01.
  - At least 13.5% of 2024 PubMed abstracts processed with LLMs (lower bound); up to 40% in some subcorpora (e.g. computer science, China/Korea style countries, some journals).
  - Example LLM-flavored abstract fragments they quote: "meticulously delving into the intricate web", "comprehensive grasp of the intricate interplay ... is pivotal", "we delve into the intricacies ... accentuating its indispensability".
- Full list of 291 rarer excess style words (Fig S6) includes: accentuates, adept, advancements, akin, align, alongside, amidst, avenue(s), bolster, burgeoning, capabilities, commendable, compelling, comprehending, comprehensive(ly), consequently, conversely, crafting, culminating, delineates, delve, demonstrating, discern, distinctive, elevate, elucidate, embracing, emphasizes, encapsulates, encompasses, endeavors, enduring, enhances, ensuring, exceptional, exhibits, expedite, explores, facilitates, fostering, foundational, garnered, grappling, groundbreaking, harness, heighten, hinges, illuminates, imperative, intricate/intricacies, interplay, invaluable, leverages, meticulous(ly), multifaceted, nuanced, notable, noteworthy, optimizing, orchestrating, pinpoint, pioneering, pivotal, poised, pressing, realm, remarkable, revolutionize, scrutinize, seamless(ly), showcased, signifying, streamline, surpass, swift, thorough, transformative, ultimately, uncharted, underscore, unparalleled, unraveling, unveil, uphold, versatility, warranting.
- Authors' own caution: cannot identify individual abstracts; their discussion cites Padmakumar & He for homogenization.

### 1.2 Liang et al. - Mapping (FULL) and Monitoring (FULL)
- "Mapping the Increasing Use of LLMs in Scientific Papers." Weixin Liang, Yaohui Zhang, Zhengxuan Wu, ... Christopher Potts, Christopher Manning, James Zou. arXiv 2404.01268, Apr 2024 (COLM 2024). https://arxiv.org/abs/2404.01268
  - Method: distributional LLM-quantification (mixture model of human vs AI reference word distributions) on 950,965 papers Jan 2020-Feb 2024 (arXiv, bioRxiv, 15 Nature portfolio journals).
  - Results: LLM-modified share up to 17.5% (abstracts) / 15.3% (introductions) in arXiv CS by Feb 2024; Mathematics 4.9% abstracts, Nature portfolio 6.3%. Higher in papers with frequent preprinting first authors, crowded fields, shorter papers.
  - Top four words by log-odds LLM vs human in arXiv CS abstracts: realm, intricate, showcasing, pivotal. Flat 2010-2022, surge from 2023.
- "Monitoring AI-Modified Content at Scale: A Case Study on the Impact of ChatGPT on AI Conference Peer Reviews." Liang, Izzo, Zhang, ... Zou. arXiv 2403.07183 (ICML 2024). https://arxiv.org/abs/2403.07183
  - 6.5%-16.9% of peer-review text at ICLR 2024 / NeurIPS 2023 / CoRL 2023 / EMNLP 2023 substantially LLM-modified (ICLR 10.6%, EMNLP 16.9%, NeurIPS 9.1%, CoRL 6.5%; none in Nature portfolio).
  - ICLR 2024 reviews: probability-in-a-sentence increases of 9.8x commendable, 34.7x meticulous, 11.2x intricate. Also lists innovative, versatile as AI-skewed adjectives.
  - Higher LLM share in reviews with lower reviewer confidence, near deadline, from reviewers less likely to reply to rebuttals.
- "The Widespread Adoption of LLM-Assisted Writing Across Society." Liang, Zhang, Codreanu, Wang, Cao, Zou. arXiv 2502.09747, 2025 (abstract page only, secondary read). Estimated LLM-assisted share Jan 2022-Sep 2024: about 18% of financial consumer complaints (687,241), up to 24% of corporate press releases (537,413), just under 10% of job postings in small firms (304.3M), nearly 14% of UN press releases (15,919). Adoption rose sharply post-ChatGPT then leveled off by 2024. Closest thing to "work writing" data.

### 1.3 Juzek & Ward - "Why Does ChatGPT 'Delve' So Much?" (FULL)
- Title: "Why Does ChatGPT 'Delve' So Much? Exploring the Sources of Lexical Overrepresentation in Large Language Models." Tom S. Juzek, Zina B. Ward (Florida State). arXiv 2412.11385, Dec 2024. COLING 2025 (Proc. 31st Int. Conf. on Computational Linguistics; Wikipedia cites ACL Anthology 2025.coling-main.426). https://arxiv.org/abs/2412.11385
- Method: 3-step procedure; PubMed abstracts; ChatGPT-3.5 summarized/regenerated abstracts to test; 21 focal words. Tests of training data (arXiv, Leipzig news corpus, Wikipedia, International Corpus of English varieties), architecture/algorithms, and RLHF (Llama 2-Base vs Llama 2-Chat per-word entropy; Llama 3/3.1 similar); online study comparing abstracts with/without focal words.
- 21 focal words (increase in occurrences per million, 2020 to 2024; mapping of figures to words inferred from table column order, treat the per-word pairing as likely but check the PDF): delves +6697%, delved +2240%, delving +1817%, showcasing +1396%, delve +1375%, boasts +918%, underscores +904%, comprehending +899%, intricacies +773%, surpassing +667%, intricate +611%, underscoring +537%, garnered +437%, showcases +422%, emphasizing +397%, underscore +391%, realm +381%, surpasses +368%, groundbreaking +330%, advancements +278%, aligns +267%.
- Findings: no evidence for training data (focal words far rarer in arXiv/news/Wikipedia than in ChatGPT output), no evidence for Nigerian-English hypothesis in ICE corpus (Hern, Guardian, 2024 hypothesis not supported by their initial check), none for architecture/algorithm. RLHF "consistent with" playing a role: Llama Chat less "surprised" by AI abstracts with focal words than Base. Online study inconclusive: people did not simply prefer focal-word abstracts; for "delve"-initial items they preferred the version without, likely because they already know "delve" is a tell.
- Authors speculate rushed, underpaid raters may treat particular words as a proxy for quality.

### 1.4 Juzek & Ward 2025 follow-up (full text via HTML read)
- "Word Overuse and Alignment in Large Language Models: The Influence of Learning from Human Feedback." arXiv 2508.01930, Aug 2025, BIAS 2025 workshop at ECML PKDD. https://arxiv.org/abs/2508.01930
- Method: Llama 3.2-3B Base vs Instruct (DPO, not RLHF proper). Flags words used far more by Instruct.
- Numbers: nuanced +8342%, nuance (verb) +6301%, firstly +4794%, reliance +3193%, generalizability +3124%. 813 of 814 words used more by Instruct than Base were also used more than in human PubMed text. 28 of 32 literature-cited overused words appear in the Instruct-vs-Base list.
- Experiment: 400 Prolific participants (about 90% from Africa, 10% SE Asia), 4,039 ratings. High-score variants preferred 52.4% vs 47.6% (small effect, p<0.01). "Nuanced" pairs went the other way (46.6%).
- Claim: overuse is misalignment between feedback-worker lexical expectations and ordinary users' expectations. Authors say causal link is preliminary.
- A 2026 LREC follow-up (Lexical Alignment Score, Triangulated Preference Shift) was only seen in search-result summary [UNVERIFIED details].

### 1.5 Yakura et al. - spoken language (FULL). This is the "delve in YouTube talks / spoken language" paper.
- "Empirical Evidence of Large Language Model's Influence on Human Spoken Communication." Hiromu Yakura, Ezequiel Lopez-Lopez, Levin Brinkmann, ... Iyad Rahwan (Max Planck Institute for Human Development). arXiv 2409.01754 (v4 dated Jul 2026, preprint). https://arxiv.org/abs/2409.01754
- Method: synthetic-control analysis of 737,083 hours / 824,634 spontaneous podcast episodes (from 1.4M, spontaneity classifier ~90% accuracy); a "GPT score" per word from log-odds of human vs GPT-edited abstracts; a preregistered experiment (N=496) where a brief chatbot interaction made people adopt the bot's words (persisting after a distractor task).
- Numbers: delve in Science and Technology podcasts rose to about 44% above counterfactual over months 13-18 after release (95% CI +22% to +63%, placebo p=0.010); Education +32% (p=0.06); Business +31% (p=0.04); all-category sample +9%; Sports -7%. Top 1% of GPT-score words (n=36): 28 of 36 increased, 13 credibly; median peak about 50% above baseline.
- Crucial for the skill: delve reverted. Gap peaked around mid-2024, then fell below baseline (Science and Tech -15%, Education -11%, Business -30%, all-sample -35%). Coincides with GPT-4o free release and public awareness. Words such as boast, meticulous, showcase kept rising. GPT score for delve is "markedly attenuated" for GPT-5 vs GPT-3.5/4.
- Earlier YouTube academic talks result (360,445 talks) is only mentioned in an appendix (concurrent work). Task brief named "Geng et al." for this; I found no Geng paper on YouTube talks. Geng papers are on arXiv abstracts (see 1.6). [Attribution to Geng UNVERIFIED]
- Related: Florida State "Model Misalignment and Language Change: Traces of AI-Associated Language in Unscripted Spoken English," arXiv 2508.00238 (podcast data 22.1M words). Search summary says "delve" did not show a significant increase there and causal direction is open. I downloaded it but did not read it in detail [only abstract-level, treat as UNVERIFIED].

### 1.6 Geng & Trotta
- "Is ChatGPT Transforming Academics' Writing Style?" Mingmeng Geng, Roberto Trotta (SISSA). arXiv 2404.08627 (v2 Nov 2024). One million arXiv abstracts May 2018-Jan 2024; adaptive word set incl. decreasing words; estimated about 35% of CS abstracts LLM-style (baseline: GPT-3.5 "revise the following sentences"). Found "is"/"are" frequency fell more than 10% in 2023 (as cited by Wikipedia; also GPT-3.5 revisions used "is/are" less). (FULL abstract; the 10% figure via Wikipedia citing it.)
- "Human-LLM Coevolution: Evidence from Academic Writing." Geng & Trotta. arXiv 2502.09606; ACL Findings 2025 (aclanthology 2025.findings-acl.657). (FULL abstract/intro.) Frequency of "delve" and "intricate" in arXiv abstracts dropped sharply after being publicized in spring 2024, while "significant" and "additionally" kept rising; "is"/"are" still falling. Interpretation: authors adapted (selecting or editing outputs). Also: words LLMs disfavor (decreasing) are a signal too.

### 1.7 Reinhart et al. - style, not just words
- "Do LLMs write like humans? Variation in grammatical and rhetorical styles." Alex Reinhart et al. PNAS 122(8), Feb 2025, arXiv 2410.16107. Biber features; GPT-4o, GPT-4o mini, Llama 3 8B/70B base and instruct. (Read via arXiv HTML.)
- Present participial clauses 2-5x human rate (GPT-4o 5.3x); nominalizations about 1.5-2x (GPT-4o 2.1x); "that" clauses as subjects up to 2.6x; phrasal coordination about 1.9x; agentless passives about half human rate for GPT-4o.
- Words used at over 100x human rate by GPT-4o: camaraderie, tapestry, palpable, intricate. "Tapestry" in 23% of GPT-4o outputs; "amidst" in 27%.
- Instruction tuning produces the biggest departure from human style; base Llama closest to human. Larger model did not help. Classifier accuracy for 7-way source ID 66% (chance about 14%).

### 1.8 Russell, Karpinska, Iyyer
- "People who frequently use ChatGPT for writing tasks are accurate and robust detectors of AI-generated text." ACL 2025, arXiv 2501.15654. 300 non-fiction articles; 5 frequent-LLM-user annotators, majority vote misclassified 1 of 300 (about 99.7%); beat commercial detectors even on paraphrased/"humanized" text. They rely on "AI vocabulary" plus judgments of formality, originality, clarity. (abstract page read.) Implication: swapping synonyms is insufficient; humans detect holistic voice.

### 1.9 Wikipedia "Signs of AI writing" (community field guide, fetched raw wikitext, content current to Oct 2026)
- URL: https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing . Not a peer-reviewed source, but each vocabulary word requires a non-pop-science external citation. Strongest synthesis I found, and the only one with an era breakdown. Its era claims for 2025-2026 rest partly on blogs [flagged below].
- It cites Reinhart for GPT-4o producing "more variation from human writing than other contemporaneous models."

### 1.10 Washington Post analysis (Nov 2025) - via secondary summaries (Yahoo mirror); original 403-blocked
- Merrill, Chen, Kumer, "What are the clues that ChatGPT wrote something?" 13 Nov 2025. 328,744 public ChatGPT messages (mostly GPT-4o) May 2024-Jul 2025; English, 10+ words.
- Reported: em dash in under 1 in 10 responses a year earlier vs over half by summer 2025; emoji in 70% of messages by July 2025; "not just X, but Y" in 6% of chats in July; "delve" in 1 in 1,000 chats in July 2025; "core" up 5x, "modern" up; sharp rise in contractions. [From secondary summary; verify before quoting.]

### 1.11 Em dash studies
- Freeburg, "The Last Fingerprint: How Markdown Training Shapes LLM Prose," arXiv 2603.27006, Mar 2026 (single independent author, preprint; read via HTML). 12 instruction-tuned models, 10 topics, about 10,000 words each per condition. Em dashes per 1,000 words, unconstrained: GPT-4.1 10.62; Claude Opus 4.6 9.09; Claude Sonnet 4 8.29; Claude Haiku 3.5 7.51; DeepSeek V3 6.95; GPT-4o mini 4.16; GPT-4o 4.12; Gemini 2.5 Pro 3.53; GPT-5.4 1.43; Gemini 2.5 Flash 1.28; Llama 3.1 8B / 3.3 70B Instruct 0.00. Human baseline 3.23 per 1,000 (8 published essays, 57,232 words; range 0.33-17.12; small sample). With a "no markdown" instruction Claude Opus 4.6 fell to 0.19 and Gemini 2.5 Pro to 0.00 but GPT-4.1 stayed 9.10 and DeepSeek V3 5.41. Explicit em-dash ban left GPT-4.1 at 3.86, DeepSeek 1.57 (so "don't use em dashes" is not fully obeyed by every model). Llama 3.1 8B base 0.49 vs instruct 0.00. Author's hypothesis: markdown-heavy training data leaks into prose via the em dash; post-training modulates strength. Hypothesis, not proven.
- Czuma, "Em-ergence of the em-dash," arXiv 2606.29540 (2026; FULL abstract). 69,632 medRxiv preprints; share of Discussion sections with at least one em dash 4.23% before ChatGPT release vs 11.58% after (+7.35 pp, OR 2.96); about 4% through 2023, 8.0% in 2024, 20.3% in 2025, 20.9% in first four months of 2026. Preregistered. Shows em dash rise is real but slow and delayed, and that human adoption (not only model output) is driving it.
- The Economist analysis (Jul 2026; 55,940 sentences, 1.2M words; models ChatGPT, Claude, Gemini, Grok vs NYT/WaPo/novels), via Dataconomy and Fast Company summaries only (original not read): em dash no longer a reliable marker; only Claude used em dashes more than humans; ChatGPT now less than humans; clearest signs are verbosity and LESS punctuation (fewer commas, semicolons, parentheses), overuse of "and" in long sentences, polysyllabic/rarer/scientific words, nominalizations, "it's not X, it's Y", rule of three, uniform sentence length. [Secondary summary only; details UNVERIFIED]
- Altman said OpenAI adjusted em-dash behavior in response to users; GPT-5.1 added an opt-out instruction (Nov 2025) per Wikipedia and the Freeburg paper.

### 1.12 Graphite, "AI Tells" (16 Sep 2026; industry research, read in full via fetch)
- Druck, Paredes, Smith. https://graphite.io/five-percent/research/ai-tells
- Method: 10,000 pre-ChatGPT Common Crawl articles; 9 models x 10,000 articles each (GPT-4.1, GPT-5, GPT-5.6 Sol, GPT-6 Astra, Claude Opus 4, Opus 4.6, Opus 5, Gemini 2.5 Pro, Gemini 3.1 Pro) generated from GPT-4.1 summaries, length-matched. Tells = words/2-3-grams/"frames" at >= 2x human rate. About 12,877 unique tells; 65% unique to one model family.
- Cross-model patterns: more than 100x fewer exclamation marks than humans; fewer parenthetical asides; less sentence-length variance; longer words (5.2-5.7 chars vs 4.9); across versions, hype words and "well-known tells" decline but total tell count does not fall (GPT total tells +48% earliest to latest).
- Per model highlights are in section 4 below. I could not independently verify the model names beyond the page. Treat as the single source for 2026 per-model data.

### 1.13 Mode collapse and diversity
- Kirk et al. "Understanding the Effects of RLHF on LLM Generalisation and Diversity." Robert Kirk, Ishita Mediratta, Christoforos Nalmpantis, Jelena Luketina, Eric Hambro, Edward Grefenstette, Roberta Raileanu. ICLR 2024, arXiv 2310.06452. (FULL abstract/intro.) LLaMA 7B and OPT 125M, summarisation and instruction following. RLHF generalizes better OOD than SFT but significantly reduces per-input output diversity (measured by distinct n-grams, SBERT cosine similarity, NLI diversity) and across-input diversity. Tradeoff generalisation vs diversity.
- Padmakumar & He, "Does Writing with Language Models Reduce Content Diversity?" ICLR 2024, arXiv 2309.05196. (FULL.) Controlled experiment with argumentative essays: no model, base GPT-3, feedback-tuned InstructGPT. InstructGPT (not GPT-3) increased similarity between different authors and reduced lexical and key-point diversity; effect attributable to the model's contributions being less diverse, while user-written parts were unaffected. Users accepted about 70% of suggestions; model supplied about 35% of characters. Key-point Rouge-L homogenization 0.1536 (solo) / 0.1578 (GPT-3) / 0.1660 (InstructGPT), InstructGPT significantly higher (p<0.05).
- West & Potts, "Base Models Beat Aligned Models at Randomness and Creativity," COLM 2025, arXiv 2505.00047. (FULL abstract.) Aligned models: favorite random number "7", predictable game strategies, "pleasant writing over creative originality". Better benchmark scores correlate with worse unpredictability tasks.
- Zhang, Yu, Chong, ... Manning, Shi, "Verbalized Sampling: How to Mitigate Mode Collapse and Unlock LLM Diversity," arXiv 2510.01171 (v4 Jul 2026; FULL). Claims mode collapse is driven by typicality bias in preference data: annotators favor familiar text. On HelpSteer, higher base-model log-probability responses preferred at 51.6-60.8% (above chance); fitted typicality coefficient alpha = 0.57 +/- 0.07 and 0.65 +/- 0.07 on 6,874 correctness-matched pairs (p<1e-14). Prompting for a verbalized distribution of responses with probabilities raised creative-writing diversity 1.6-2.1x and recovered 66.8% of base-model diversity. The best direct evidence for a specific mechanism, but preprint; moderate-high strength.
- Jiang et al., "Artificial Hivemind: The Open-Ended Homogeneity of Language Models (and Beyond)," arXiv 2510.22954 (v2 Oct 2026; FULL abstract+Fig 4). Infinity-Chat: 26K real open-ended queries; 70+ models. Within-model: with top-p 0.9, temperature 1.0, 50 samples per query, in 79% of cases mean pairwise similarity exceeds 0.8. Across models: different models produce strikingly similar outputs. Reward models and LLM judges poorly calibrated on items where human annotators disagree.
- Anderson, Shah, Kreminski, "Homogenization Effects of Large Language Models on Human Creative Ideation," C&C 2024, arXiv 2402.01536. 36 participants; ChatGPT users produced individually varied but group-level more homogeneous ideas than users of a non-LLM tool (Oblique Strategies); felt less responsible for ideas. This is the "Anderson" homogenization paper.
- Sourati, Ziabari, Dehghani, "The Homogenizing Effect of Large Language Models on Human Expression and Thought," Trends in Cognitive Sciences (online 11 Mar 2026, doi 10.1016/j.tics.2026.01.003, per search results); arXiv 2508.01491. (FULL abstract.) Opinion/synthesis, no new experiment; argues LLMs mirror dominant styles from training data and amplify convergence as everyone uses the same models. Qualitative. Note: the task brief paired "Sourati/Anderson"; these are two separate papers.
- Qiu, He, Chugh, Kleiman-Weiner, "The Lock-in Hypothesis: Stagnation by Algorithm," arXiv 2506.06166 (ICML 2025). Agent-based simulations plus real GPT usage data: sudden sustained drops in diversity after new GPT releases, consistent with a human-AI feedback loop. (abstract read.)

### 1.14 "Slop" research
- Paech, Roush, Goldfeder, Shwartz-Ziv, "Antislop: A Comprehensive Framework for Identifying and Eliminating Repetitive Patterns in Language Models," arXiv 2510.15061 (Oct 2025; FULL abstract + Section 3). Slop = repeated phrasing that makes text recognizable. Frequency ratio vs human baseline (wordfreq plus Reddit/Gutenberg corpora), 2,000 creative-writing outputs from gemma-3-12b: "Elara" 85,513x; "unsettlingly" 3,833x; "shimmered" 2,882x; "stammered" 2,043x; trigram "heart hammered ribs" 1,192x; "voice trembling slightly" 731x; "felt profound sense" 550x. "It's not X, it's Y" about 6.3x more common than in human text in some models. Slop fingerprints cluster within model families and differ across families. Antislop sampler/FTPO fine-tuning: 90% slop reduction in their evals. CAUTION: creative writing, small open models; not representative of work messages. Useful points: it's model-specific, and token banning has collateral damage (which maps to "don't just ban words" in a prompt).
- EQ-Bench slop scores (Sam Paech): I did not retrieve the EQ-Bench page. [UNVERIFIED. Antislop's author is the EQ-Bench creator but I did not confirm method/numbers.]

### 1.15 Perception studies relevant to work messages (secondary only)
- Coman & Cardon, International Journal of Business Communication 2025 (via UF news, PsyPost summaries; paper not read). Professionals rated AI-assisted messages as efficient; but when supervisors used heavy AI assistance, sincerity, caring and perceived leadership ability dropped. About 95% judged low-AI supervisor messages professional vs 69-73% for high-AI use. [Secondary only.]

---

## 2. Verified word and phrase list (by type)

Source key: K = Kobak 2025 (PubMed, excess words 2024); J = Juzek & Ward 2024/25; L = Liang et al. 2024; R = Reinhart 2025; W = Wikipedia Signs of AI writing (cites external studies); G = Graphite Sep 2026; GT = Geng & Trotta; Y = Yakura; WP = WaPo via secondary; A = Antislop.
Tier A = quantified in a peer-reviewed or archival paper. Tier B = appears in Wikipedia list with external corroboration or in one industry study. Tier C = anecdotal / single secondary source.

### Verbs (strongest category; 66% of Kobak's 379 style words are verbs)
| Word | Evidence |
|---|---|
| delve / delves / delving | K r=28.0 (delves); J +1375% to +6697%; Y delve peaked 2024 then reverted; WP 1 in 1,000 chats Jul 2025 |
| underscore(s) | K r=13.8; J +391 to +904%; W; Wikipedia says Grok still overuses it in 2026 |
| showcase / showcasing | K r=10.7; J +422 to +1396%; L top-4 (showcasing); W; Y sustained uptake |
| boast(s) (meaning "has") | J +918%; Y sustained; W |
| highlight (verb), highlighting | W; K; GT |
| emphasize / emphasizing | J +397%; K; W |
| foster / fostering | K; W; also in W's 2026 list |
| enhance | K; W |
| garner / garnered | J +437%; K; W |
| bolster(ed) | K; W |
| align with | J +267% (aligns); K; W |
| leverage(s) / harness | K (leverages, harness); W 2026 list (leverage) |
| surpass / surpassing | J +667%/+368% |
| comprehend / comprehending | J +899% |
| elevate, facilitate, streamline, unveil, unlock, navigate(?) | elevate/facilitate/streamline/unveil/unlocking are in K's list. "Navigate" not in K list; do not claim it. |
| serves as / stands as / features / offers (instead of "is" / "has") | W (copula avoidance); GT "is/are" down more than 10% in 2023 abstracts |
| ensuring, encompassing, contributing to (trailing -ing clauses) | K (ensuring, encompassing); W superficial analyses; R present participial clauses 2-5x |

### Adjectives
| Word | Evidence |
|---|---|
| intricate / intricacies | J +611% / +773%; L 11.2x ICLR reviews, top-4 arXiv; K; R >100x GPT-4o |
| pivotal | K; L top-4; W |
| crucial | K delta=0.037; W |
| meticulous(ly) | L 34.7x ICLR reviews; K; Y sustained |
| commendable | L 9.8x ICLR reviews; K |
| comprehensive | K |
| nuanced | J2025 +8342% (Llama 3.2 Instruct vs Base); K; W 2026 "multifaceted" |
| robust | W list |
| vibrant, valuable, key, enduring, tapestry, testament, landscape (abstract noun), interplay | W words-to-watch; tapestry R >100x and in 23% of GPT-4o outputs; interplay/enduring K |
| seamless(ly), invaluable, unparalleled, groundbreaking, transformative, multifaceted, innovative, versatile | K and/or L lists. groundbreaking J +330%. |
| notable, noteworthy, remarkable, exceptional | K list |

### Nouns
realm (J +381%, L top-4, K), landscape (as abstract noun; W), tapestry (R, W, A), testament (W), interplay (K, W), avenues/avenue (K), advancements (J +278%), camaraderie / palpable (R, creative/narrative writing), deep dive (W, citing Economist Jul 2026), "potential", "findings" (K, high-frequency inflation rather than rare-word).

### Transitions and sentence openers
| Item | Evidence |
|---|---|
| Additionally (sentence-initial) | W; GT: "additionally" keeps rising in arXiv abstracts through 2024-25. Graphite: Gemini 3.1 Pro "additionally the" 8.6x human rate, and "furthermore the" 43x |
| Moreover / Furthermore / Consequently / Notably / Ultimately | K lists consequently, conversely, ultimately; Graphite: "ultimately this" 78x (Gemini 3.1 Pro). Wikipedia cautions transition words alone are weak evidence (humans use them too) |
| "In summary," / "In conclusion," / "Overall," as section-ending recap | W (rated historical: older LLMs) |
| "However, it's important to note that..." / "It is crucial to differentiate..." | W (2023-24 didactic disclaimers; Pangram report cited) |
| "Another dimension" 117x, "together these" 95x | Graphite GPT-6 Astra (2026) |
| "What comes next", "looking ahead" | Graphite Claude Opus 5 |

### Openers and closers (conversation-facing; mostly chat leakage)
| Item | Evidence |
|---|---|
| "Certainly!", "Of course!", "Absolutely!", "Great question" | W (collaborative communication): "Certainly!", "Of course!", "You're absolutely right!" |
| "I hope this helps", "Let me know if...", "Would you like...", "Is there anything else", "Here is a..." | W collaborative-communication list |
| "As an AI language model", "as of my last knowledge update" | W (historical 2022-23) |
| Closing summary paragraph restating the point; "Overall," | W (older output) |
| Offering follow-up options at the end | W ("more detailed breakdown", "would you like") |
| "Despite its X, Y faces challenges... Future outlook" | W, encyclopedic outline-style conclusions |

### Structures and constructions (highest value for short work messages)
| Construction | Evidence |
|---|---|
| "Not just X, but (also) Y" / "It's not X, it's Y" / "no X, no Y, just Z" | W; A (6.3x human in some models, creative writing); Economist summary (secondary); WaPo summary: "not just X, but Y" in 6% of chats Jul 2025 (secondary); Graphite: "is not just" 18x, "not simply" 157x, "rather than merely" 160x (2026) |
| "Y rather than X" / "X should be treated as Y rather than Z" | W, flagged as growing in 2026; Graphite "rather than relying" 187x (GPT-6 Astra) |
| Rule of three (adjective, adjective, adjective; "A, B, and C") | W; Economist summary (secondary) |
| Trailing present-participle clause adding fake analysis ("..., highlighting its importance") | R: 2-5x human (GPT-4o 5.3x); W |
| Nominalization-heavy, long, information-dense sentences | R 1.5-2.1x; Economist summary |
| "Serves as / stands as / marks / represents" in place of "is" | W; GT |
| Vague attribution ("experts argue", "industry reports") | W |
| Vague connection ("associated with", "in connection with") | W (flagged as among the most common 2026 signs) |
| Hedge/disclaimer about missing info ("not widely documented", "based on available information") | W (2024-25; extends to "corrective framing" mid-2026) |
| Inline-bold-header bullet lists ("**Header**: text") | W |
| Title Case headings, heavy bold, emoji bullets, tables | W; WaPo summary: 70% of messages had emoji Jul 2025 [secondary] |
| "without sacrificing / without losing / without compromising" (avoiding tradeoffs) | Graphite: 4-8x across models, "without requiring" 70x (GPT-6 Astra) |
| "X matters because..." | Graphite: "matters because" 357x (GPT-6 Astra), 132x (Claude Opus 5) |
| Em dash, formulaic and sales-like | See 1.11. Strongly model-dependent. |
| Uniform sentence length, few commas/semicolons/parentheticals, almost no exclamation marks | G; Economist summary; GT; Wikipedia 2026 note on 8-20 word sentences (blog-sourced) |
| Fewer repeated words ("elegant variation") in older models | W (older models, repetition penalty) |
| Hype adverbs: incredibly 18x, remarkably 19x, profound 25x, immense 22x, absolutely essential 32x | Graphite Gemini 3.1 Pro |

---

## 3. Why models do this (causal explanations and evidence strength)

| # | Explanation | Evidence | Strength |
|---|---|---|---|
| 1 | Post-training (SFT/RLHF/DPO), not pretraining, creates the tells. Base models write closer to humans; instruct versions overuse. | Reinhart (Llama base vs instruct; instruct largest style deviation); Juzek & Ward 2024 (Llama 2 Base vs Chat entropy) and 2025 (813 of 814 Instruct-favored words also exceed human PubMed rates); Freeburg (Llama 3.1 8B base 0.49 vs instruct 0.00 em dashes; single comparison) | Moderate-strong for the general claim. Weak for any specific word, because the studies use few model pairs. |
| 2 | Not training-data frequency. | Juzek & Ward: focal words are far rarer in arXiv, Wikipedia, news corpora than in ChatGPT output | Moderate. They could not inspect actual training data. |
| 3 | Rater typicality / familiarity bias: annotators prefer text the base model finds likely. This pushes toward the mode, i.e. mode collapse and cliche. | Zhang et al. (alpha 0.57-0.65, 51.6-60.8% preference for higher-likelihood response, 6,874 pairs); Padmakumar & He (feedback-tuned but not base lowers diversity); Kirk (RLHF reduces per-input diversity); West & Potts | Moderate-strong for diversity loss; Zhang is a single preprint for the mechanism. Not direct evidence for specific words. |
| 4 | Rater lexical preferences or "proxy for quality": raters (often low-paid, rushed) reward polished-sounding words. Possibly different English variety than end users. | Juzek & Ward 2025: small preference (52.4 vs 47.6%) for high-score variants among Prolific raters; speculation about rushed raters. Hern/Guardian Nigeria hypothesis: Juzek & Ward 2024's ICE check found no support; Wikipedia/others only report it as a hypothesis; Nigerian users objected | Weak-moderate. Treat "Nigerian English" as unsupported. Mechanism is plausible but effect size small. |
| 5 | Length and verbosity bias in reward models: longer, more elaborate answers win, producing padding, summaries, qualifiers. | Singhal et al., "A Long Way to Go: Investigating Length Correlations in RLHF," COLM 2024, arXiv 2310.03716 (abstract via search summary): reward gains are largely length gains; length-only reward reproduces most RLHF improvements. Economist summary: verbosity is the clearest tell. | Moderate (second-hand read). |
| 6 | Sycophancy / agreeableness from human preference for agreement. Explains "Great question!", "You're absolutely right", softened critique. | Sharma et al. (Anthropic), arXiv 2310.13548 (abstract read): five assistants show sycophancy; agreeing responses more likely preferred in human data; PMs sometimes prefer convincing sycophantic answers over correct ones. | Moderate-strong for sycophancy; link to specific phrases is inference. |
| 7 | Information-dense "formal register" default. | Reinhart: nominalizations, participial clauses, "academic" style even for fiction prompts | Moderate. |
| 8 | Markdown leakage (em dash, bold, lists). | Freeburg 2026 (12 models; single author; hypothesis) plus Wikipedia's markdown observations | Weak-moderate. |
| 9 | Regression to the mean: generic, positive, significance-asserting statements replace specific facts. | Wikipedia editorial claim; consistent with Zhang typicality and Hivemind. | Weak as stated (no direct test). |
| 10 | Feedback loop. Humans adopt LLM words, then humans write that way, so detection by "human vs AI words" blurs. | Yakura (spoken, preregistered N=496 experiment; podcasts), Czuma (em dash rising in human preprints through 2026), Geng & Trotta (authors dropping flagged words) | Strong for adoption; causal link in the wild is moderate. |
| 11 | Publicity-driven reversal: once a tell is known, humans edit it out and vendors tune it away. | Yakura (delve drop after mid-2024), Geng & Trotta (delve/intricate drop), WaPo (delve 1 in 1,000), Wikipedia (delve drop-off 2025), OpenAI GPT-5.1 em-dash control | Strong for delve; the tell inventory shifts to new words instead of shrinking (Graphite: total tells up 48% for GPT lineage). |

Bottom line on causality: the best-supported statement is "post-training on human preferences produces homogeneous, typical, high-register, verbose, agreeable output with a model-family-specific word fingerprint." The exact word-level mechanism is not settled.

---

## 4. How tells shift by model and over time

### Time (ChatGPT lineage)
- 2023 to mid-2024 (GPT-3.5/4): delve, intricate, meticulous, pivotal, commendable, tapestry, testament, underscore, realm, showcasing, "Additionally," didactic "it's important to note" disclaimers, knowledge-cutoff statements, "In conclusion" closers. (K, L, J, W.)
- Mid-2024 to mid-2025 (GPT-4o): delve declines sharply; Wikipedia lists align with, bolstered, crucial, emphasizing, enhance, fostering, highlighting, pivotal, showcasing, underscore, vibrant. WaPo (secondary): em dashes, emoji, "not just X but Y", contractions up; "core", "modern" up. Reinhart: GPT-4o deviates from human style more than other contemporaries (via W).
- Mid-2025 to mid-2026 (GPT-5): per Wikipedia, emphasizing, enhance, highlighting, showcasing persist; more "canned emphasis on notability/media coverage", vague connection phrases, hedging about sources. Freeburg: GPT-5.4 only 1.43 em dashes per 1,000 (below human 3.23).
- Mid-2026 on: Wikipedia lists challenge, clearer, dependable, echoed, foster, leverage, matters, multifaceted, practical, prioritize, quietly, steady, universally, plus shorter, plainer sentences (8-20 words) and heavy period/comma use. The Wikipedia source for this is a blog review of a model [weak; UNVERIFIED]. Graphite (Sep 2026) independently shows GPT-6 Astra: dependable 59x, practical 26x, meaningful 13x, "matters because" 357x, "not simply" 157x, "without requiring" 70x, em dashes about 1/8 human rate. So "dependable / practical / matters because / rather than relying" is corroborated by two sources, though both are non-peer-reviewed.
- Wikipedia (Sep 2026+): newest models increasingly hard-coded to avoid em dashes; commas and periods now more frequent than human. Wikipedia text carries a {{cn}} (citation needed) on the last claim, so treat as unverified.

### Model family
- Claude: Freeburg - highest em-dash rates among non-GPT-4.1 models in 2025-26 era (Opus 4.6 9.09/1,000 unconstrained) but collapses to about 0.2 when told "no markdown/prose-only"; Economist summary: only Claude exceeded humans on em dashes in Jul 2026 [secondary]; Graphite: Claude Opus 5 em-dash rate about human, tells include deliberate (26x), steady (6x), measured (4.2x), "rather than merely" 160x, "less like a X and more like" 105x, "every single" 112x, "enormously" 45x, "matters more than" 93x, "what comes next", "looking ahead". Anecdotal (single blogs): Claude is agreeable; "You're absolutely right" appears in Wikipedia's collaborative list but not attributed to Claude by a study. [Claude-specific word tics other than Graphite's are UNVERIFIED]
- GPT: em dash heavy in 4.1/4o, much lower in GPT-5.x/6 per Freeburg and Graphite; word tells shifted from delve-type to "dependable/practical/matters because/rather than relying". Graphite: GPT lineage total tells +48% earliest to latest version.
- Gemini: Graphite: hype register: incredibly (18x; 1,835x relative to GPT-6 Astra), profound 25x, immense 22x, remarkably 19x, absolutely, "furthermore" and "additionally" heavy, "this comprehensive guide", "is not just a X, it is" 153x, em dashes nearly eliminated. Freeburg: Gemini 2.5 Pro 3.53, Flash 1.28.
- Grok: overuses "scientific" words (causal, empirical, correlate), still underscores in 2026 (Wikipedia, uncited here).
- DeepSeek V3: 6.95 em dashes per 1,000 (Freeburg); explicit ban less effective.
- Llama / Mistral / Gemma: open models have different fingerprints (Antislop: fingerprints cluster by family; creative-writing slop: Elara, shimmered, voice barely above a whisper). Llama 3.x Instruct: nuanced, firstly, reliance (J2025).
- 65% of Graphite's tells are unique to one model family. A single global "AI word list" will therefore have declining recall, and wrong-model word lists can even be fine.

Open question the skill should not paper over: recency. The most recent hard data (Graphite Sep 2026, Economist Jul 2026, Wikipedia Oct 2026) is industry or community, not peer-reviewed. Peer-reviewed word data stops at GPT-3.5/4/4o era.

---

## 5. Practical implications for the humanize skill

1. Do not rely on a banned-word list alone. Evidence: tells migrate (delve to dependable/practical/matters because), 65% of tells are model-specific, total tell count does not fall across versions (Graphite), and expert human detectors key on holistic formality/originality/clarity, not just vocabulary (Russell 99.7% majority-vote accuracy, even on "humanized" text). Ban structures and registers, not only words.
2. Highest-value structural bans for short work messages: (a) "not just X, but Y" / "it's not X, it's Y" / "rather than X" corrective framing; (b) rule-of-three lists; (c) trailing "-ing" analysis clauses ("..., ensuring alignment"); (d) significance/legacy statements ("underscores the importance of"); (e) "serves as / stands as" for "is"; (f) closing recap or offer ("Let me know if...", "Hope this helps", "Overall,"); (g) opener praise ("Great question", "Certainly!"); (h) vague attribution and vague connection ("associated with"); (i) hedging disclaimers about missing information; (j) inline-bold-header bullets, emoji bullets, Title Case.
3. Core word blacklist (high confidence, multiple independent sources): delve, underscore, showcase, boast (meaning "has"), intricate/intricacies, pivotal, crucial, meticulous, commendable, nuanced, tapestry, testament, realm, landscape (abstract), interplay, vibrant, foster, enhance, bolster, garner, highlight (verb), emphasize, align with, leverage, comprehensive, robust, seamless, multifaceted, "Additionally,". Add the 2026 candidates with the caveat that they are single-source: dependable, practical, "matters because", "without sacrificing/losing", "rather than relying/merely/simply", deliberate, steady, "the distinction matters".
4. Replace, don't just delete: fill with plain verbs (is, has, use, show, fix, ship, need) and specific facts. Wikipedia notes synonyms of a flagged word are not necessarily flagged ("a word being overused does not imply its synonyms are overused") but also that swapping words does not fix the regression-to-the-mean specificity problem. The real fix is concrete detail: names, numbers, file/PR identifiers, dates, what changed, what is blocked, what is needed from whom.
5. Counter mode collapse with specificity and variation, not with randomness: model output converges (Hivemind: mean similarity > 0.8 in 79% of queries; typicality bias). Instruct the model to commit to a specific stance and details, vary sentence length, allow fragments, let the first sentence carry the content. Optional trick for generation pipelines: Verbalized Sampling (ask for several candidates with probabilities, pick a low-probability/atypical one); +1.6-2.1x diversity in creative writing, untested on work messages.
6. Punctuation and rhythm: do not claim "avoid em dashes" is the whole fix. It is model-dependent: Claude (and earlier GPT-4.x) over-use, GPT-5.x/Gemini now under-use. Newest tell is the opposite pattern: very uniform sentences, few commas/semicolons/parentheticals, almost no exclamation points, longer words. Humans in short messages use fragments, contractions, parentheses, lowercase openers, a stray exclamation, and uneven length. Explicit em-dash ban is not fully obeyed by every model (GPT-4.1 3.86/1,000 even when banned; Freeburg), so post-check by regex.
7. Length: verbosity is the strongest tell in the Economist summary and is consistent with RLHF length bias (Singhal). For Slack/email/status updates, hard-cap length, drop setup and recap, no summary line that repeats the body.
8. Sycophancy/warmth markers: strip praise openers and "You're absolutely right"-style validations, performative empathy, "I hope this finds you well" filler, and the "Let me know if you have questions" closer unless a real next action exists.
9. Calibrate with the audience cost: heavy AI assistance in manager-to-team messages lowered perceived sincerity and leadership (Coman & Cardon, secondary), so the stakes are highest for praise, congratulations, apologies, and feedback. Write those with personal specifics.
10. Keep the list versioned and dated. Add a "last verified" date and a maintenance process: re-run Kobak-style excess-word analysis or sample current model outputs per target model, because (a) delve fell sharply within about 18 months of publicity, and (b) the newest models (per Graphite) prefer different words.
11. Test method: have the skill generate against a representative prompt set per model and count hits against structure and word patterns, rather than trusting any static list.

---

## 6. Claims I could not verify, or that conflict

- Nigerian-English/outsourced-rater origin of "delve" (Hern, Guardian 2024): hypothesis only; Juzek & Ward's ICE check found no support; Nigerian readers contested the premise. Do not use as a fact.
- Wikipedia's "GPT-6 / mid-2026" word list and 8-20 word-sentence claim cite a single blog review; Graphite independently supports some words (dependable, practical, matters) but not all. Wikipedia's text also references "GPT-5.6" and "GPT-6 Astra"; I could not independently confirm these releases beyond the Graphite and Wikipedia pages.
- Wikipedia's claim that newest models are hard-coded to avoid em dashes and over-use commas has a citation-needed tag.
- WaPo and Economist figures are from secondary summaries (both originals blocked or paywalled).
- Geng-on-YouTube: no source found; the spoken-language "delve" evidence is Yakura et al. (YouTube talks only in appendix).
- The pairing of focal-word percentages in Juzek & Ward 2024 to individual words is by table column order from pdftotext.
- EQ-Bench slop scores: not retrieved.
- Florida State spoken paper (2508.00238): I only saw search summaries; its null/weak finding for "delve" conflicts with Yakura's +44% and was not reconciled.
- Singhal (length bias) and Sharma (sycophancy) were read at abstract/secondary level only.
- Kirk et al. numeric effect sizes were not extracted.
- Freeburg's human baseline is only eight essays; treat its 3.23/1,000 human rate as rough. Study is a single-author preprint.
- Claude "genuinely/honestly/You're absolutely right" as measured tells: no study found.

## 7. Source URLs
- https://arxiv.org/abs/2406.07016 (Kobak)
- https://arxiv.org/abs/2404.01268, https://arxiv.org/abs/2403.07183, https://arxiv.org/abs/2502.09747 (Liang)
- https://arxiv.org/abs/2412.11385, https://arxiv.org/abs/2508.01930 (Juzek and Ward)
- https://arxiv.org/abs/2409.01754 (Yakura), https://arxiv.org/abs/2508.00238 (FSU spoken)
- https://arxiv.org/abs/2404.08627, https://arxiv.org/abs/2502.09606 (Geng and Trotta)
- https://arxiv.org/abs/2410.16107 (Reinhart PNAS), https://arxiv.org/abs/2501.15654 (Russell)
- https://arxiv.org/abs/2310.06452 (Kirk), https://arxiv.org/abs/2309.05196 (Padmakumar and He), https://arxiv.org/abs/2505.00047 (West and Potts), https://arxiv.org/abs/2510.01171 (Verbalized Sampling), https://arxiv.org/abs/2510.22954 (Hivemind), https://arxiv.org/abs/2402.01536 (Anderson), https://arxiv.org/abs/2508.01491 (Sourati), https://arxiv.org/abs/2506.06166 (Lock-in)
- https://arxiv.org/abs/2510.15061 (Antislop)
- https://arxiv.org/abs/2310.03716 (Singhal), https://arxiv.org/abs/2310.13548 (Sharma)
- https://arxiv.org/abs/2603.27006 (Freeburg), https://arxiv.org/abs/2606.29540 (Czuma)
- https://graphite.io/five-percent/research/ai-tells
- https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing
- https://www.washingtonpost.com/technology/interactive/2025/how-detect-chatgpt-em-dash/ (paywalled; secondary: Yahoo mirror)
- https://dataconomy.com/2026/08/04/how-to-spot-ai-writing/ (Economist summary)
