# 04 - Field guides, structural tells, and evasion research

Method note: WebFetch returns a lossy, summarized view of long pages. The Wikipedia page (en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing, ~228-254k chars) was read in overlapping chunks, including via `?action=raw`. Coverage is near-complete but not verbatim; a few sections (full "Markup", "Citations", "Edit summaries" details) were seen only as summaries. The page contains dated claims up to October 2026 (GPT-5.6, GPT-6 era etc.); these are reported as the page states them and I could not independently verify the model names or dates. Quotes are short.

## 1. Wikipedia "Signs of AI writing" - full catalog

Page's own caveats: signs are not proof; patterns are "not the problem itself"; a single sign is weak, density and co-occurrence is strong; detectors and human judgment are unreliable; most underlying word studies covered scientific abstracts or fiction.

### 1.1 Content tells
| Tell | Watch phrases | Example |
|---|---|---|
| Undue emphasis on significance/legacy/trends | "stands/serves as", "is a testament/reminder", "a crucial/pivotal/vital/significant/key role/moment", "underscores its importance", "evolving landscape" | "marking a pivotal moment in the evolution of regional statistics"; "helped solidify its role as a regional hub" |
| Canned notability / media-coverage claims | "independent coverage", "trade publications", "cited/featured/profiled in", "active social media presence", "written by a leading expert" | "was featured in Vogue, Wired, Toronto Star" |
| Superficial analysis via trailing -ing phrases | "highlighting/underscoring/emphasizing...", "ensuring...", "reflecting/symbolizing...", "contributing to...", "fostering...", "encompassing...", "enhancing...", "valuable insights", "align/resonate with" | "further enhancing its significance as a dynamic hub of activity and culture" |
| Promotional/ad language | "boasts a", "vibrant", "rich", "profound", "showcasing", "exemplifies", "commitment to", "nestled", "in the heart of", "groundbreaking", "renowned", "diverse array" | "Nestled within the breathtaking region of Gonder" |
| Vague connection/association | "in connection with", "associated with", "connected with" | "associated with residential water management applications" |
| Vague attribution / overgeneralized opinion | "Industry reports", "Observers have cited", "Experts argue", "Some critics argue", "several sources" (when few cited), "such as" before exhaustive-looking lists | "widely interpreted as aimed at Islamabad" |
| Outline-like "challenges and future" conclusions | "Despite its... faces several challenges", "Despite these challenges", "Challenges and Legacy", "Future Outlook" | "Despite these challenges, Amu TV has managed to continue to provide a vital service" |
| "Awards and recognition" section | near-ubiquitous in AI-written bios | - |

### 1.2 Language and grammar
- **AI vocabulary, density matters.** Words co-occur; one is coincidence, many is strong. Era-dependent: "delve" spiked 2023-early 2024 then fell in 2025. Overuse of a word does not imply its synonyms are overused. Lists the page gives:
  - 2023-mid 2024 (GPT-4): Additionally, boasts, bolstered, crucial, delve, emphasizing, enduring, garner, intricate/intricacies, interplay, key, landscape, meticulously, pivotal, underscore, tapestry, testament, valuable, vibrant
  - mid-2024-mid-2025 (GPT-4o): align with, bolstered, crucial, emphasizing, enhance, enduring, fostering, highlighting, pivotal, showcasing, underscore, vibrant
  - mid-2025-mid-2026 (GPT-5): emphasizing, enhance, highlighting, showcasing + notability/media-coverage claims
  - mid-2026+ (GPT-6, per page): challenge, clearer, dependable, echoed, foster, leverage, matters, multifaceted, practical, prioritize, quietly, steady, universally; shorter sentences (~8-20 words), more commas/periods
  - Grok-specific: causal, empirical, correlate; still "underscore"
  - Full watch list: Additionally (sentence-initial), align with, boasts (=has), bolstered, crucial, deep dive, delve, emphasizing, enduring, enhance, fostering, garner, highlight (verb), interplay, intricate, landscape (abstract noun), meticulous, pivotal, robust, showcase, tapestry (abstract noun), testament, underscore (verb), valuable, vibrant. Example: "Somali cuisine is an intricate and diverse fusion of a multitude of culinary influences."
- **Copula avoidance.** "serves as / stands as / marks / functions as / operates as / represents", "boasts / features / maintains / offers" instead of "is/has". Cited stat: >10% drop in "is/are" in academic writing in 2023. Example edit: "is LAAA's exhibition arm" became "serves as LAAA's exhibition space". Also lead sentences "X refers to..." treating a topic as a word.
- **Negative parallelism** (page says common in humans too, esp. "myths busted" listicles, but stereotypical AI sign; "Y rather than X" is described as particularly common in recent output):
  - "Not just X, but also Y": "This remark doesn't just undermine the editor's argument; it questions their very right to participate."
  - "Not X, but Y": "not grounded in visual mastery, but in what Amelia Jones terms..."
  - "no..., no..., just..."
  - "Y rather than X": "prioritizing empirical consolidation of power... rather than ideological purity."
- **Rule of three.** Triads to look comprehensive. Stronger signal where humans would not bother (edit summaries). Example: "reshaping them through contemporary values, modern aesthetics, and digital animation technology."
- **Elegant variation / lexical diversity** (Historical): cycling synonyms to avoid repeating a noun ("the constraints of socialist realism" -> "the confines of state-imposed artistic norms" -> "the constraints imposed by the Soviet regime"). Caveat: non-native writers also avoid repetition.
- **Human-side syntax** (page's "signs of human writing"): simple "is/has", plainer verbs ("wrote" not "authored"), definitive superlatives, qualifiers ("perhaps", "tends to"), "in order to"-style wordiness.

### 1.3 Style and formatting
- Title Case section headings ("Impact of Technology and Digitalization"); no caveat.
- Overused boldface, "key takeaways" style, bolding many terms in one paragraph.
- Inline-header vertical lists: "**Header:** description" bullets.
- Heading errors: title heading atop content, skipped levels, many level-1 headings, headings containing only headings.
- Emoji as headings/bullets (rarer now): "🌍 My Mission: ..."
- Small unusual tables that could be prose.
- Curly quotes/apostrophes: ChatGPT and DeepSeek typically; Gemini and Claude typically do not. Page: "Curly quotes alone do not prove LLM use" (Word, macOS/iOS produce them).
- Em dashes: formulaic "punched up" use, often spaced, where humans use commas/colons/parentheses. Page's historical note: heavy 2022-Sept 2026; Economist July 2026 study (cited by page, unverified by me) says only Claude out-dashed professionals; newest models are hard-coded to avoid dashes, so text now leans on commas and periods, which the page itself tags as a new tell.
- Markdown syntax leaking into non-markdown contexts (`**bold**`, `##`, `[text](url)`), thematic breaks `---` between every section. Page: Markdown alone is weak (many people use it).

### 1.4 Communication aimed at the user
- Collaborative/assistant phrasing: "I hope this helps", "Certainly!", "Would you like...", "let me know", "Here's a template...". Leftover "Delete this section before submission."
- Hedging disclaimers by era: 2023-24 "it's important to note", "it is crucial to differentiate", "it's important to remember"; 2024-25 "not widely documented", "limited in the provided search results", "based on available information"; mid-2026+ "corrective framings": "rather than", "does not establish", "should be treated as... rather than as...".
- Knowledge-cutoff statements (2022-23): "as of my last knowledge update".
- Prompt refusals: "As an AI language model", "I'm sorry".
- Section summaries (historical): "In summary", "In conclusion", "Overall", restating the point at end of paragraphs.
- Placeholders: "[Describe the specific section...]", "2025-XX-XX".
- Sycophancy: no dedicated section found on the page. Closest are "I understand your concern", "I respectfully request", "Dear Wikipedia Editorial Team" (talk-page stock phrases).

### 1.5 Markup / citation / meta (low relevance for work messages)
Leaked tool markup (oaicite, contentReference, turn0search0, [cite: 1], grok-card, DeepSeek dagger brackets, attached_file, `:::writing`), utm_source=chatgpt.com, invalid DOIs/ISBNs, fabricated references, hallucinated categories/templates, canned edit summaries ("ensured", "adheres to", "streamlined", "neutral tone"), stacked policy assurances.

### 1.6 Page's "ineffective indicators" (do not trust)
Perfect grammar; mixed formal/casual register; "bland/robotic" prose; "fancy/academic" prose; transition words in isolation (Additionally/Consequently/Notably are only a weak tell). Page also notes model differences: ChatGPT/Grok broader-context and wordier, Gemini/Claude more concise.

## 2. Other sources

| Source | URL | What it adds |
|---|---|---|
| Graphite, "AI Tells" (Druck, Paredes, Smith; dated 16 Sep 2026) | https://graphite.io/five-percent/research/ai-tells | Best quantitative source. 10,000 pre-ChatGPT human Common Crawl articles vs 90,000 AI articles (9 models x 10,000, topic-matched, word-count matched +-10%). A feature is a "tell" if >=2x human rate. 12,877 unique tells. Key ratios: Claude Opus 5 "is genuinely" 1,021 uses vs 4 human; "rather than merely" 160x; "less like a _ and more like" 105x; "matters because" 132x; "without losing/sacrificing/compromising". Gemini 3.1 Pro "is not just a _ it is" 153x, "incredibly" 18x, "furthermore the" 43x. GPT-6 Astra "the _ is not simply" 576x, "matters because" 357x, "dependable" 59x. Well-known tells fell 41-86% across versions; 55-72% of tells are unique to one version (tells churn; model-specific). Human tells: exclamation marks (>100x), parenthetical asides, first person/direct address ("you can't"), casual qualifiers ("pretty", "sort of"), anecdotes ("last year", "my favorite"), "excited to". Caveat: web-article genre, synthetic AI articles from summaries, vendor blog, not peer reviewed, model names/dates unverified by me. |
| Russell, Karpinska, Iyyer, ACL 2025 | https://arxiv.org/abs/2501.15654 (html v2: https://arxiv.org/html/2501.15654v2) | 300 non-fiction articles; 5 "expert" annotators (heavy LLM-writing users) vs 4 non-experts. Experts: ~92.7% TPR, ~3-4% FPR, majority vote wrong on 1/300. Non-experts near chance (56.7% TPR / ~52% FPR). Clue shares in expert explanations: vocabulary 53.1%, sentence structure 35.9% ("not only... but also", groups of three, uniform length), grammar/punctuation 24.8% (AI is cleaner; humans make small errors), originality 23.7% ("safe", no surprise/humor), quotes 22.3% (formal, all speakers sound alike), clarity 19.5% (over-explains, tells not shows). Non-experts wrongly treat any uncommon word as AI. |
| Pangram technical report (Spero & Emi) | https://arxiv.org/abs/2402.14873 | Cited by Wikipedia page; I did not read it. Pangram claims a trained classifier on large AI corpora rather than perplexity (PCWorld summary, secondary). |
| Geng & Trotta, ACL Findings 2025 | https://aclanthology.org/2025.findings-acl.657.pdf | Cited by Wikipedia for LLM-word frequency rise in academic writing; not read directly. |
| Washington Post, Nov 2025 | https://www.washingtonpost.com/technology/interactive/2025/how-detect-chatgpt-em-dash/ | 403 on fetch; unverified. |
| Community anti-AI-writing skill files | https://alexanderweichart.de/7_Agent/skills/write-in-my-voice/references/anti-ai-writing ; https://git.secluded.site/agent-skills/blob/main/vendor/impeccable/STYLE.md?raw=1 ; https://tessl.io/registry/skills/github/flutter/agent-plugins/natural-writing ; https://skills.sh/iliaal/ai-skills/writing ; https://writewithai.substack.com/p/10-dead-giveaways-your-content-screams | Seen only as search snippets (not fetched). Consensus items: "not X, it's Y" as top tell, forced triads (use 2 or 4), "Header: description" bold bullets, throat-clearing ("Here's the thing", "The catch?"). Folk/practitioner evidence, no measurement. |
| Liang et al. 2023 (Patterns) | https://arxiv.org/pdf/2304.02819 | 7 detectors, 91 TOEFL essays, 88 US 8th-grade essays; avg 61.22% false positive on TOEFL. Low-perplexity = flagged. Relevance: plain, simple writing is also what perplexity detectors flag, so "write simply" is not evidence of being human to those detectors. |
| GPTZero/Originality.ai internals | none found | Search returned only affiliate/review blogs claiming perplexity+burstiness. No vendor research blog from GPTZero or Originality.ai was located; Pangram's own blog also not found. Treat vendor-mechanism claims as unverified. |

Not found: any source on sycophantic openers ("Great question!") beyond Wikipedia's collaborative phrases, nor Slack/email-specific tell research. Work-message-specific guidance below is inference.

## 3. Evasion research

| Study | Finding | Sample / caveats |
|---|---|---|
| DIPPER, Krishna et al. NeurIPS 2023 https://arxiv.org/abs/2303.13408 | 11B paraphraser dropped DetectGPT accuracy 70.3% -> 4.6% at 1% FPR; also beat watermarking, GPTZero, OpenAI classifier. Retrieval defense caught 80-97% of paraphrases at 1% FPR (database of 15M generations). | 2023 detectors; abstract-level read. Retrieval needs provider-side logs. |
| Adversarial Paraphrasing, Cheng et al. https://arxiv.org/abs/2506.07001 | Plain paraphrasing did NOT help much (T@1%F actually rose 8.57% on RADAR, 15.03% on Fast-DetectGPT). Detector-guided paraphrasing cut T@1%F 64.49% (RADAR), 98.96% (Fast-DetectGPT), avg 87.88%. Authors report "mostly slight" quality loss. | Needs access to a guide detector; no human readability study per abstract. |
| Russell et al. ACL 2025 (above) | Paraphrasing and a humanizer prompt built from an expert-clue guidebook (o1-Pro) crushed automated detectors: Pangram ~90% TPR, GPTZero 46.7%, Fast-DetectGPT 23.3%, Binoculars 6.7%, best GPT-4o prompted detector 3.3% on humanized text. Human experts still 100% by majority vote (individual annotator 3 fooled: 0% on humanized). Prompt reduced vocabulary clues (42.3% vs 57.1% of explanations) but experts keyed on other signals and confidence dropped. | 60 articles per condition; 5 experts, who are unusually skilled readers. Most relevant: avoiding vocabulary alone does not fool a trained human reader. |
| DAMAGE, Pangram Labs https://arxiv.org/abs/2501.03437 | 19 humanizer/paraphrase tools; many detectors fail on humanized text; authors built a robust detector. | Abstract only; vendor-authored; no numbers retrieved. |
| "Why AI Detection Fails for Academic Integrity", Karr et al., ACM AI Summit 2026 https://arxiv.org/pdf/2608.11256 | Per a search summary: after humanization, Pangram and GPTZero scores collapse toward zero while an LLM-assisted baseline still flags most. | Could not read PDF; secondary summary only. Unverified. |
| LessWrong "Pangram can be evaded" https://www.lesswrong.com/posts/hrpQxfYvF6CBGWfJX/pangram-ai-detection-software-can-be-evaded | Iterative persona/author-style prompting with GPT-5.4 got Pangram 3.2 to 20% then 100% human on a Socrates dialogue; Claude Opus 4.6 stayed 94-100% AI even after removing em dashes and rewording flagged phrases. | n of ~2 pieces; Pangram unreliable under ~200 words; Pangram 4 reportedly much better; author did not assess quality (a commenter said stories were "LLM-y in a bad way"). Anecdote. |
| "How Well Do LLMs Imitate Human Writing Style?" https://arxiv.org/pdf/2509.24930 | Few-shot gave up to 23.5x better style matching than zero-shot; completion-style prompting highest. Yet output stays more predictable (perplexity ~15.2 vs human ~29.5); fidelity and detectability separable. | Read via search snippet, not primary text. |
| "Catch me if you can? Not yet", (everyday-author imitation) | Few-shot beats zero-shot but GPTZero still labels most output AI (<55% human-like typical); adding an initial human-written snippet boosts human-likeness. | Secondary summary only; unverified. |
| Pangram / UChicago (Booth) study | Reported Pangram ~96.7% accuracy under humanizer attack while competitors fell from >90% to <50%; low FPR. | Only via news/secondary summaries (the-decoder, others); the mixed picture vs Karr et al. means unresolved. |

### Takeaways on what works
- Works against detectors: detector-guided rewriting or iteration against a detector; strong humanizer pipelines; few-shot/continuation from real human text; model choice (outputs differ a lot by model). Synonym-swap/typo-insertion tools mostly fail (practitioner ranking, https://theairankings.com/best-ai-humanizer/, unverified commercial source).
- Does not work: plain one-pass paraphrase against modern detectors (Cheng et al.); swapping flagged vocabulary alone against humans (Russell); stripping em dashes alone (LessWrong anecdote; Graphite shows em-dash use varies by model anyway).
- Against human readers: structure and specificity cues (sameness of rhythm, safe content, over-explaining, formal quotes) persist after word-level cleanup. The content-level fix (specific details, opinions, uneven rhythm) is the one that lines up with both Graphite's "human tells" and Russell's clue list.
- Do detector-evasion methods improve readability? Mostly unmeasured. Cheng et al. report slight degradation; humanizer tools that insert typos or synonyms probably hurt readability (inference). Prompt-based "write like a human with specifics/contractions/direct address" is the only family that plausibly improves it, but no study measured human reader preference.
- Tell churn: Graphite shows 55-72% of tells are unique to a model version, and Wikipedia shows lists rotating each ~year. A static word blacklist decays; structural/behavioral rules age better.

## 4. Strong evidence vs folklore

**Strong (quantified or multi-source):**
1. Dense AI vocabulary clusters (crucial/pivotal/testament/tapestry/vibrant/underscore/delve/landscape/showcase). Wikipedia + Russell (53.1% of clues) + Geng & Trotta. Caveat: decays by model generation; density not single words.
2. Negative parallelism ("not just X, it's Y", "rather than merely", "less like X and more like Y"). Wikipedia, Russell (sentence structure), Graphite ratios 100-576x per model. Present in humans too, so it is a rate issue.
3. Rule-of-three groupings and uniform sentence length (Russell, Wikipedia).
4. Copula avoidance ("serves as", "boasts", "features").
5. Trailing -ing significance clauses ("highlighting...", "ensuring...", "contributing to...").
6. Significance/legacy/"matters because" inflation, vague attribution ("experts say").
7. Over-explaining, safe/no-surprise content, uniform voices in quotes (Russell).
8. Assistant artifacts: "I hope this helps", "Certainly!", "let me know", "it's important to note", leaked markup.
9. Human tells: first person, anecdotes with specific time/place, casual qualifiers, exclamation marks, parenthetical asides (Graphite).

**Moderate / format-dependent:** Title Case headings, heavy bold, inline-bold-header bullets, emoji bullets, unusual tables, "In summary/Overall" closers, outline "challenges and future" endings (Wikipedia-observed; strong in articles, plausibly stronger in short messages where nobody formats that way; no controlled measurement). Curly quotes: ChatGPT/DeepSeek only; Claude/Gemini typically straight, so weak and model-specific.

**Weak or folklore:**
- Em dashes: widely believed, but Graphite shows GPT-6 at ~1/8 human rate, Claude near human, Gemini near zero; Wikipedia says only useful in combination; Economist figure unverified. Treat as model-specific; avoid but do not rely on it.
- "Perfect grammar", "formal/academic tone", "bland prose", isolated transition words (Wikipedia explicitly lists these as ineffective; Russell shows non-experts misuse "uncommon word" and "clean grammar" cues).
- Perplexity/burstiness as detector mechanism for modern detectors (vendor/affiliate claims; Pangram describes a trained classifier). Burstiness-style advice (vary sentence length) still matches Russell's human-expert clue, so keep it for readers, not detectors.
- Sycophantic openers, Slack/email-specific tells: no quantitative source found; common sense, flag as unverified.
- Any single-word blacklist as durable.

## 5. Implications for the skill (inference, not from sources)
- Prefer positive constraints (state the fact first, concrete numbers/names, plain "is/has", one point per sentence, uneven lengths, a stated opinion or caveat with a reason) over word blacklists.
- Ban structures by pattern not word: contrast-reframe ("not X, it's Y", "rather than", "less like... more like"), triads, trailing -ing significance clauses, summary closers, offers of further help, throat-clearing openers, "important to note", inline-bold-header bullets in short messages, Title Case, emoji bullets.
- Do not claim the skill beats detectors; evidence says only detector-in-the-loop methods do reliably, and trained humans still catch vocabulary-scrubbed text.
- Short texts (<~200 words) are weakly classified by Pangram (LessWrong note, anecdotal), which suits short work messages.
