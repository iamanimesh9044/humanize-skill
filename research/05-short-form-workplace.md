# Short-form workplace writing: what reads as human (research notes)

Verification legend: [V] = read primary page/abstract or full text this session; [S] = secondary summary only (news, blog, search snippet); [U] = unverified/from memory, do not cite without checking.
Searches were done 2026-10; many full papers were paywalled or PDF-unparseable. Where I only saw an abstract, I say so.

## 1. Sources

### A. Detectability vs length

1. **Detecting AI-Generated Text: Factors Influencing Detectability with Current Methods** (arXiv 2406.15583, 2024). Survey/review of detection factors. https://arxiv.org/pdf/2406.15583
   - PDF was unreadable by fetch [U for primary]; figures come from a search-engine summary [S]: watermarking needs ~10 words; statistical/fine-tuned detectors ~100+ words; one cited study ~120 words enough for full performance, another ~200 for strong models; a theoretical result ~500 for very close distributions. Concatenating an author's posts helps (a fine-tuned RoBERTa went ~80% to near 100% with 10 tweets) [S].
   - Takeaway: no single threshold; it depends on detector. Verify numbers against the paper before quoting.
2. **Why AI-Generated Text Detection Fails: Evidence from Explainable AI Beyond Benchmark Accuracy** (arXiv 2603.23146, 2026). https://arxiv.org/pdf/2603.23146 [S]. Misclassified texts were shorter than correct ones (false negatives avg 177 words vs 243 for true positives; modal error lengths 14 and 34 words) [S, snippet].
3. **LLM-Detector** (arXiv 2402.01158, 2024, Chinese text) https://arxiv.org/pdf/2402.01158 [S]. On 10-50 word texts, supervised and statistical detectors lost substantial accuracy; LLM-based detectors held up better.
4. **ETS note on AI detectors** https://www.ets.org/content/ets-org/cn/en/home/research/behindthebreakthroughs/using-ai-detectors-grade-student-work.html [S]. Reports ~50 words as minimum for reliable detection; judging one short sentence is "practically impossible". Single-study claim; unverified.
5. **Stylometry recognizes human and LLM-generated texts in short samples** Przystalski, Argasinski, Grabska-Gradzinska, Ochab; 2025; arXiv 2507.00838 (listed as Expert Systems with Applications) https://arxiv.org/html/2507.00838v1 [V]. Method: 2,439 Wikipedia-based terms, texts from GPT-3.5/4, LLaMA 2/3, Orca, Falcon, summarizers; StyloMetrix features, tree classifiers. Every sample is 10 sentences (>=1,100 characters). Binary accuracy 0.79-1.0 (Wikipedia vs GPT-4 ~0.98); some model pairs near chance (52-56%). No accuracy-vs-length curve; encyclopedic only. GPT-4 overused words like "significant," "notable". Note: "short" here is ~10 sentences, far longer than a Slack message.
6. **GPT detectors are biased against non-native English writers** Liang et al., 2023, Patterns; arXiv 2304.02819 https://arxiv.org/pdf/2304.02819 [S]. >half of non-native TOEFL essays misclassified as AI; low perplexity is the mechanism; GPT-4 word-enhancement cut false positive from 61.22% to 11.77%. Relevant: plain, low-variety human writing gets flagged; detectors are not ground truth. Not about short text.
7. **Human heuristics for AI-generated language are flawed** Jakesch, Hancock, Naaman; 2023; PNAS 120(11) e2208839120 https://arxiv.org/abs/2206.07271 [V abstract]. 6 experiments, 4,600 participants, professional/hospitality/dating self-presentations. People could not detect AI text; they used heuristics (first-person pronouns, contractions, family topics = "human") that AI can exploit to read as more human than humans. Suggests "AI accents". Implication: surface "human markers" like contractions are what readers look for, but they are weak, gameable signals.
8. **Unmasking the Imposters: In-Domain Detection of Human vs. Machine-Generated Tweets** arXiv 2406.17967, 2024 https://arxiv.org/html/2406.17967v1 [S]. Finding: uncensored models with in-domain fine-tuning sharply reduce detector effectiveness. Short tweets and fine-tuned models are hardest cases.

### B. Register / style studies

9. **Do LLMs write like humans? Variation in grammatical and rhetorical styles** Reinhart, Markey, Laudenbach, Pantusen, Yurko, Weinberg, Brown; 2025; PNAS 122(8), e2422455122; arXiv 2410.16107 https://arxiv.org/html/2410.16107v1 [V, full text via fetch]
   - Method: two parallel corpora (CAP: COCA 8 registers; HAP-E: academic, news, fiction, spoken, blogs, TV/movie scripts). Model gets ~500 words of human text, writes ~500 more. GPT-4o, GPT-4o mini, Llama 3 8B/70B, base and instruct. 66 Biber features; random forest/lasso.
   - Findings: instruction-tuned models overuse noun-heavy, information-dense features: present participial clauses 527% (GPT-4o) and 481% (4o mini) of human rate (text says "2 to 5 times"); nominalizations 214%/209%; "that" clauses as subject 263-331%; agentless passives ~53% for GPT-4o. Words like "camaraderie," "palpable," "tapestry," "intricate" >100x human rate. Underused: informal items like "yep," "ok," "blah," and obscenities (>100x less). Base models match humans far better, so the style comes from instruction tuning. Larger model size did not close gaps. Authorship classification of LLM vs human: only 4.2% of LLM text classed human, 9.8% of human classed LLM.
   - Limits: ~500-word continuations, not chat/Slack/email; informal text not analyzed as its own register. CMU press coverage quotes different multipliers (1.5-2x nominalizations) than the paper's table (~2.1x); use paper numbers.
10. **Biber & Conrad, Register, Genre, and Style (2009), chs. on electronic communication** [U for primary]. Only secondary: business email studies applying their framework find mixed spoken/written features (contractions, personal pronouns, abbreviations, omission of some parts of speech) (Latvian business-email study, https://journal.lu.lv/bjellc/article/download/344/327/394 [S]). I could not access rate data. No source in this set directly measures chatbot contraction rate; the "Beyond 'AI Language'" preprint (arXiv 2608.06589) looks at contractions but I did not read findings [U].
11. **Wikipedia: Signs of AI writing** https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing [V, first ~100k of 254k chars]. Editor-curated, not a controlled study. Signs: vocabulary (delve, crucial, pivotal, tapestry, showcase), avoiding "is/are" for "serves as/features", negative parallelisms ("not just X but Y"), inflated significance, trailing "-ing" analysis, vague attributions, formulaic "Despite... challenges" sections, promotional tone, markdown/bold/emoji bullets, chatbot artifacts ("Here are several..."), hedging disclaimers. Explicit caveat: no single sign is conclusive, clusters matter, humans do all of these, vocabulary shifts over model generations.

### C. Conversational features

12. **Texting insincerely: The role of the period in text messaging** Gunraj, Drumm-Hewitt, Dashow, Upadhyay, Klin; 2016; Computers in Human Behavior 55:1067-1075 https://researchconnect.suny.edu/en/publications/texting-insincerely-the-role-of-the-period-in-text-messaging/ [V abstract page + S]. Text replies ending in a period rated less sincere than without; effect absent for handwritten notes. Follow-up (Houghton et al. 2018) on one-word messages reportedly similar [S]. Small convenience samples likely [U]. Implication: terminal periods on short chat replies carry tone in chat but not on paper. Applies to one-line replies, not multi-sentence messages [inference].
13. **Investigating the Representation of Backchannels and Fillers in Fine-Tuned Language Models** arXiv 2509.20237 (ACL 2026) https://arxiv.org/abs/2509.20237 [S]. Pre-trained models know little about backchannels/fillers because they are absent from pretraining text; fine-tuning on dialogue corpora that keep them made outputs closer to humans.
14. **From "um" to "yeah": information flow in human conversation** arXiv 2403.08890 https://arxiv.org/pdf/2403.08890 [S]. Disfluencies ("um", "uh") help manage information flow; "buy time".
15. **Jennifer Nagel, Metacognition and backchannel in conversation: humans versus machines** (Oxford talk listing) [S]. Argues LLMs are compromised in backchannel signaling. A talk abstract, not evidence.
    - Gap: I found no study directly testing LLM use of ellipsis, dropped subjects, fragments, or typos in workplace chat. Claims that LLMs "lack" these are plausible from #9 and #13 but not directly measured for work chat.

### D. Plain language, Grice, writing for web

16. **Consequences of erudite vernacular utilized irrespective of necessity: Problems with using long words needlessly** Oppenheimer; 2006; Applied Cognitive Psychology 20(2):139-156. [S via secondary coverage] Needlessly complex word swaps (e.g., in grad school applications) lowered ratings of author intelligence; 71 students in one experiment per secondary report; trust/likability was a hypothesis not a result.
17. **Plain language and trust** [S]: Journal of the Association for Consumer Research 2025, five experiments: plain-language terms-of-use summaries raise perceived brand trust via subjective fluency but lower it via objective understanding (https://ideas.repec.org/a/ucp/jacres/doi10.1086-735026.html). Jargon study of >1,000 mock jurors (UF) linked jargon to lower fluency, more guilty votes, less trust in the system. Markowitz 2024 PNAS Nexus: AI plain-language science summaries improved perceived trustworthiness [S]. Mechanism: processing fluency (Schwarz). Effect is not uniform.
18. **Federal Plain Language Guidelines** https://plainlanguage.gov/guidelines/ [S]. Practitioner guidance (mid-90s origin, revised periodically); search found no controlled study isolating "most important information first". Treat as expert consensus, not experimental evidence.
19. **Nielsen Norman Group, "Concise, SCANNABLE, and Objective: How to Write for the Web" / How Users Read on the Web (1997)** [S, secondary reports only; original not opened]. Usability gains on a sample site: concise +58%, scannable +47%, objective +27% (one source says 26%), combined +124%. Small, 1997 web-page study with a single site; not workplace messages. Check original before quoting.
20. **Grice's maxims in LLM research**: IBM-authored "Language Models in Dialogue: Conversational Maxims for Human-AI Interactions" (arXiv 2403.15115, 2024) ties excess wordiness to reward-model over-optimization and adds benevolence/transparency maxims; "The Polite Liar" (arXiv 2511.07477) frames verbosity as a Quantity failure arising from user-satisfaction training; Krause & Vossen 2024 INLG survey of maxims in NLP (https://aclanthology.org/2024.inlg-main.39). All [S]; argument papers more than measurements. Grice (1975) itself is theory, not evidence.

### E. Frameworks

21. **BLUF / inverted pyramid**: no controlled email experiment found [S]. Related news-structure studies mixed: Sternadori 2008 (Univ. of Missouri dissertation; chronological slowed secondary-task reaction time, no memory difference, comprehension marginally better for inverted pyramid) [S]; a 2014 Spanish TV-news experiment (n=60) found inverted pyramid least effective for information gain [S]; "Ways With Words" (ASNE/Poynter) reportedly found inverted-pyramid stories scored low on readership/understanding [S via blog]. News readers are not workplace readers.
22. **SCQA / Minto Pyramid**: no empirical validation found; justification is practitioner experience and working-memory arguments with unsourced figures [S].
23. **SBI (Situation-Behavior-Impact)**: CCL asserts benefits (less defensiveness) without linked studies; a 2026 medical-student poster (Rowan, no control group; 98% said they could apply it; rubric mean 15.4/20 on 75 statements) [S]. Mostly vendor/practitioner claims.
24. **nohello.net**: practitioner advocacy; no controlled studies found; counterargument: "hi" signals presence. Common compromise: greeting plus the question in one message [S].
25. **Commit messages**: Tian, Zhang, Stol, Jiang, Liu; "What Makes a Good Commit Message?"; ICSE 2022; arXiv 2202.02974 https://arxiv.org/pdf/2202.02974 [S]. Found ~44% of messages could be improved; focuses on conveying why and what; classifier C-Good precision 81.6%. I did not read the taxonomy; check it before asserting "why > what" as a rule.
26. **Generative AI for Pull Request Descriptions** Xiao, Hata, Treude, Matsumoto; arXiv 2402.08967 (2024) https://arxiv.org/abs/2402.08967 [V abstract]. 18,256 PRs with Copilot-for-PRs text: less review time, more likely merged; developers often hand-edit the description. No verbosity measure.

### F. AI-mediated communication and perceived sincerity

27. **Professionalism and Trustworthiness in AI-Assisted Workplace Writing** Cardon & Coman; 2025 (online July 16); International Journal of Business Communication https://journals.sagepub.com/doi/10.1177/23294884251350599 [S, paywalled; the "2024" date in the brief appears wrong, I found 2025]. ~1,100 working professionals rated an AI-assisted congratulatory email from a supervisor at varying AI levels. Medium-to-high AI use made respondents question authorship, confidence, caring, sincerity, ability. Per press coverage: ~40% saw high-assistance supervisors as sincere vs >80% low-assistance; 95% rated low-AI messages professional vs 69-73% heavy-AI; people judge own AI use more leniently than others'. Authors advise light-editing-only for relationship messages; routine factual messages safer. Numbers from PsyPost/UF news, not the paper.
28. **Artificial intelligence in communication impacts language and social relationships** Hohenstein, Kizilcec, DiFranzo, Aghajari, Mieczkowski, Levy, Naaman, Hancock, Jung; 2023; Scientific Reports 13:5487 https://pmc.ncbi.nlm.nih.gov/articles/PMC10073210 [S]. Smart replies sped communication and raised positive language/closeness, but partners suspected of AI use were rated more negatively. Author list beyond lead is from memory [U].

### G. Prompting / few-shot style

29. **Catch Me If You Can? Not Yet: LLMs Still Struggle to Imitate the Implicit Writing Styles of Everyday Authors** Wang, Tripto, Park, Li, Zhou; EMNLP 2025 Findings; arXiv 2509.14543 https://arxiv.org/abs/2509.14543 [V abstract]. >400 real authors, >40,000 generations per model, news/email/forum/blog; in-context examples; metrics: authorship attribution/verification, style matching, AI detection. LLMs approximate structured formats (news, email) but "struggle with nuanced, informal writing in blogs and forums." Number-of-demonstrations analysis exists but I did not read results. No controlled comparison of style description vs examples found.

## 2. How human short-form differs from LLM short-form, with evidence strength

| Difference | Evidence | Strength |
|---|---|---|
| LLM text over-uses abstract, noun-heavy, participial constructions; inflated vocabulary (tapestry, palpable); humans use plainer, more varied structure | Reinhart 2025 (full text) on ~500-word continuations; Wikipedia AI-signs list | Strong for long text; extrapolation to short messages is inference |
| Style comes from instruction tuning, not pretraining | Reinhart 2025 (base vs instruct) | Strong |
| LLMs underuse informal tokens ("yep", "ok", "blah", profanity) | Reinhart 2025 word list | Moderate (corpus-level, long outputs) |
| LLMs are verbose / violate Quantity | Gricean-LLM papers; reward over-optimization claim | Moderate (argument papers) |
| LLMs lack backchannels, fillers | Fine-tuning paper (#13), Nagel talk | Weak-moderate; spoken dialogue, not chat |
| LLMs lack ellipsis, fragments, dropped subjects, typos, lowercase in work chat | No direct study found | Unverified; plausible from #9 |
| Final period reads colder in one-line chat | Gunraj 2016 (+ follow-ups) | Moderate, small-sample lab work |
| Chatbot artifacts (preamble, "I hope this helps", markdown, bold, emoji bullets, "not just X but Y") mark AI | Wikipedia editor guide | Moderate; practitioner, caveated |
| Short text is hard to classify; detectors unreliable below ~50-100 words | ETS, LLM-Detector, factors review | Moderate; thresholds vary, no consensus |
| Readers cannot reliably tell and use flawed heuristics (contractions, first person) | Jakesch 2023 (n=4,600) | Strong |
| Readers who suspect AI penalize the sender | Hohenstein 2023; Cardon & Coman 2025 | Moderate-strong (the Cardon numbers are from press) |

Key synthesis: for a 20-60 word Slack message, automated detectors are near useless, so the real audience is a human coworker. Humans guess badly, but they punish perceived AI authorship and perceived insincerity. The goal is therefore "reads like a specific person with a specific purpose wrote it", not "evade detectors".

## 3. Frameworks: for / against

| Framework | Evidence for | Evidence against / limits |
|---|---|---|
| BLUF (answer first) | Fits Federal Plain Language "most important first" and NN/g scannability (all practitioner/1997 web data); Grice Quantity/Relation logic | No controlled email study found; news-structure studies mixed; practitioners note it fails when audience needs context, in indirect cultures, or for bad news/sensitive feedback |
| SCQA / Pyramid | Widespread consulting use | No empirical test found; built for memos/decks, overweight for a 3-line Slack message |
| SBI | Used widely; small training studies show people can apply it | Evidence mostly from developer (CCL); no outcome studies; best for simple, near-term feedback; can read formulaic if used rigidly |
| nohello | Reasonable async logic | Anecdote only; "hi" as presence ping is a real counter; compromise: greet + ask |
| Plain words | Oppenheimer 2006; fluency-trust studies; jargon/jury | Trust effect not uniform (ACR 2025: understanding can lower trust); mostly lab/consumer contexts |

Net: use these as defaults, not laws. Evidence base is thin and mostly non-workplace.

## 4. Rules for a drafting LLM (Slack / email / PR)

Evidence-backed or logically near-certain:
1. Open with the point, ask, or decision. No greeting-only, no "I hope this finds you well", no "Great question". (Plain Language, Grice, AI-signs list, nohello; moderate.)
2. Size to the register: a chat reply is one to three short lines; do not add summaries, recaps, or closing offers ("let me know if you need anything else") (Quantity, verbosity evidence).
3. Plain words over inflated ones. Ban list from evidence: delve, tapestry, pivotal, crucial, underscore, showcase, palpable, camaraderie, intricate, leverage, robust, seamless. Prefer "use", "show", "fix", "check". (Reinhart; Wikipedia; Oppenheimer.)
4. Prefer verbs and clauses over nominalizations and trailing "-ing" tails ("improving X, ensuring Y"). Say who did what in active voice. (Reinhart; moderate.)
5. Be specific: names, numbers, file paths, dates, error messages, the actual thing. Replace "significant improvements" with the measured change. (Wikipedia vague-attribution; review-classifier detail finding [S].)
6. No negative parallelism ("not just X, it's Y"), no rule-of-three padding, no inflated significance, no "Despite..., ..." wrap-up.
7. No markdown in chat: no headers, bold, emoji bullets, tables; a short plain list only when the user's own messages use lists. For PR descriptions, minimal structure (what/why, how to test) is normal and expected.
8. State the uncertain thing once, plainly ("not sure if X, checking Y"); do not hedge every claim, and do not add disclaimers.
9. Keep facts you do not know out; never invent details to sound specific. Use a placeholder or ask.
10. Do not over-fake the human markers. Contractions and first person are reasonable and register-appropriate, but typos, random lowercase, or fillers inserted as decoration are unsupported and can backfire (Jakesch: such heuristics are gameable; no evidence sprinkled imperfections help). Use informal features only when mirroring the user's samples.
11. Terminal periods: for a one-line casual chat reply, drop the period if the user's own messages do (Gunraj; small effect). Not a rule for multi-sentence messages or email.
12. Commit messages: short imperative subject; body says why when it is not obvious (consistent with Tian 2022, taxonomy unread; verify).
13. Feedback or bad news: lead with context or the concrete observation and its effect, then the ask; BLUF is not mandatory here (SBI-style, practitioner support only).
14. Relationship messages (thanks, congrats, condolences, praise): keep AI to light edits; write in the user's voice with one concrete personal detail (Cardon & Coman).

Style-source rule: if the user supplies samples, mirror their length, punctuation, capitalization, greeting/sign-off habits and vocabulary more than any generic rule. Instruction-tuned defaults pull back toward the generic style (Reinhart), and few-shot imitation works better for structured genres like email than for informal ones (Wang 2025), so keep the draft short and let the user edit.

## 5. Caveats

- Almost all style evidence is on ~500-word texts (Reinhart) or essays; no study I found measures chat/Slack-length LLM text against human workplace messages. Extrapolation is inference.
- Detector thresholds (10 / 50 / 100 / 120 / 200 / 500 words) come from different detector types; most numbers here are second-hand [S].
- Cardon & Coman statistics came from press coverage; paper paywalled. The "2024" in the brief appears to be 2025.
- Oppenheimer, NN/g, Gunraj, Hohenstein, Tian, SBI, news-structure studies: read only via search summaries/abstracts. Quote numbers only after checking originals.
- Model generations change quickly; tell-tale words (delve) rise and fall. Do not hard-code a ban list as permanent; prefer structural rules.
- Surface "human-ness" tricks are gameable and humans use flawed heuristics (Jakesch); optimizing for fooling readers is a different goal from writing well and conflicts with sincerity findings. Detectors also false-flag plain human writing (Liang).
- Frameworks (BLUF, SCQA, SBI) lack workplace-message experiments; register and relationship context should override them.
- Not found / unverified: direct tests of LLM ellipsis, fragments, dropped subjects, typos, lowercase in work chat; controlled comparison of style description vs few-shot examples; any study on greeting-only messages; Biber & Conrad email feature rates; Grice-based experiments on LLM short messages.
