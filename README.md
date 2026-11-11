# 😵‍💫 Low-Fry Assistant: a system prompt that reduces AI brain fry

This system prompt makes an AI assistant cheaper to supervise. In the one survey behind the term "AI brain fry," the strain tracks how much AI output people have to monitor and correct, how much information they have to take in, and whether AI has increased their workload. How much they use AI matters less. So the prompt doesn't make the assistant do less. It cuts how much attention you spend to get a correct result.

No study has yet tested an assistant's behavior against brain fry. Each rule here is an extrapolation from related research on overreliance, verification, interruptions and sycophancy, plus vendor guidance on how current models follow prompts. Treat it as a well-grounded starting point, not a proven fix.

## What it does

- **Hands over checked work.** It checks with tools when it can (runs the code, opens the file, fetches the source), reports only checks it actually ran, and says what is incomplete or unchecked.
- **Makes checking cheap.** It leads with the answer and a short rationale instead of a full reasoning trace. It flags only the few uncertain claims that would change what you do, in the first person and with how to confirm them. It cites only sources it has actually seen.
- **Cuts decisions.** You get one recommendation and stated defaults for routine calls. It asks questions together, up front, and only when the answer would change the work. It offers options only when the choice turns on your own values or risk tolerance.
- **Keeps long tasks quiet.** It reports at natural breakpoints and asks before irreversible, costly or out-of-scope steps. It flags deviations from a plan you approved, and ends with a short review summary: what changed, what was risky, and exactly what to check.
- **Produces what was asked.** It adds no unrequested variations or sections, and it names unfinished work instead of ending with open-ended offers.
- **Stays honest.** It judges your claims as it would a third party's, changes its position for new evidence but not for insistence, and corrects its own earlier mistakes.

Brevity never wins over substance. Correcting a mistaken premise, a caveat that changes what you should do, or a needed warning always earns its space.

## The prompt

The full prompt is in [prompt.md](prompt.md). Copy it into your assistant's system prompt or custom instructions.

## Why it's written this way

- **Exceptions live inside each rule.** Current models follow instructions literally, so absolute rules such as "never ask mid-task" or "no recap" get over-applied. Each rule carries its own scope instead.
- **Each rule gives its reason.** Vendor guidance reports that models generalize from the reason, not just the command.
- **One "Check" note replaces several disclosure lists.** Flags on every answer turn into boilerplate people stop reading, and stacking several reliance safeguards can backfire.
- **There's no "re-read your work" instruction.** Re-reading without new information rarely fixes errors. Checks that bring in new information, such as tests, tools and sources, do.
- **There's no "pause before deciding" advice and no wellbeing nudges.** The evidence for passive pauses is weak, and every nudge is itself an interruption.

## Before you deploy it

- **Tune the confirmation triggers.** "Irreversible, costly or outside what was agreed" is generic on purpose. Naming specific actions sharpens it, but test each one, because overly broad approval rules make models hold back routine work.
- **Trim the self-check sentence on models that already verify their own work.** Keep the sentence about reporting only checks actually run.
- **Test for silent failures.** Run it on a few representative conversations. Check that the model still corrects false premises, still asks when stakes are high, and still names unfinished work. A prompt that has gone too far looks calm while costing you more to supervise.

## Sources

### AI brain fry and workslop

- Bedard, J., Kropp, M., Hsu, M., Karaman, O. T., Hawes, J., & Kellerman, G. R. (2026, March 5). [When using AI leads to "brain fry."](https://hbr.org/2026/03/when-using-ai-leads-to-brain-fry) *Harvard Business Review*.
  - **Survey:** BCG and UC Riverside, 1,488 full-time US workers at large companies.
  - **Prevalence:** 14% said they had ever experienced brain fry, ranging from 6% in legal to 26% in marketing.
  - **Oversight:** workers whose AI use required high oversight reported 14% more mental effort, 12% more mental fatigue and 19% more information overload.
  - **With vs. without brain fry:** affected workers reported 33% more decision fatigue and 39% more major errors (both self-reported).
  - **Correlates:** brain fry correlated strongly with information overload, and less clearly with task switching.
- Niederhoffer, K., Kellerman, G. R., Lee, A., Liebscher, A., Rapuano, K., & Hancock, J. T. (2025, September 22). [AI-generated "workslop" is destroying productivity.](https://hbr.org/2025/09/ai-generated-workslop-is-destroying-productivity) *Harvard Business Review*. BetterUp Labs and Stanford Social Media Lab surveyed 1,150 US full-time employees. 40% had received workslop in the past month, and recipients estimated spending about 1 hour 56 minutes dealing with each instance.
- Lee, H.-P., et al. (2025). [The impact of generative AI on critical thinking: Self-reported reductions in cognitive effort and confidence effects from a survey of knowledge workers.](https://www.microsoft.com/en-us/research/publication/the-impact-of-generative-ai-on-critical-thinking-self-reported-reductions-in-cognitive-effort-and-confidence-effects-from-a-survey-of-knowledge-workers/) *CHI 2025*. With AI, workers' effort shifts from producing work toward verifying and integrating it.

### Making output cheap to check

- Passi, S., Dhanorkar, S., & Vorvoreanu, M. (2024). [Appropriate reliance on GenAI: Research synthesis.](https://microsoft.com/en-us/research/uploads/prodnew/2024/03/GenAI_AppropriateReliance_Published2024-3-21.pdf) Microsoft. Users treat fluency, length and speed as signs of accuracy. Verification-focused explanations, first-person uncertainty and AI self-critiques help, but applying every mitigation at once can backfire.
- Kim, S. S. Y., Liao, Q. V., Vorvoreanu, M., Ballard, S., & Wortman Vaughan, J. (2024). ["I'm not sure, but...": Examining the impact of large language models' uncertainty expression on user reliance and trust.](https://arxiv.org/abs/2405.00623) *FAccT*. First-person uncertainty raised user accuracy from 63.9% to 72.8%.
- Steyvers, M., et al. (2025). [What large language models know and what people think they know.](https://arxiv.org/abs/2401.13835) *Nature Machine Intelligence*. Longer explanations raised users' confidence without helping them tell right answers from wrong ones.
- Vasconcelos, H., Jörke, M., Grunde-McLaughlin, M., Gerstenberg, T., Bernstein, M. S., & Krishna, R. (2023). [Explanations can reduce overreliance on AI systems during decision-making.](https://arxiv.org/abs/2212.06823) *CSCW*. Explanations help only when they make checking cheaper than trusting.
- Fernandes, Buschek, Tankelevitch, Kosch, & Welsch (2026). [Explaining too much? Understanding how large language model reasoning traces influence performance and metacognition.](https://arxiv.org/abs/2605.25856) Preprint. Full reasoning traces lowered accuracy and inflated self-assessment compared with shorter formats. That condition also used a different model.
- Kim, S. S. Y., Wortman Vaughan, J., Liao, Q. V., Lombrozo, T., & Russakovsky, O. (2025). [Fostering appropriate reliance on large language models: The role of explanations, sources, and inconsistencies.](https://arxiv.org/abs/2502.08554) *CHI*. Showing sources reduced agreement with wrong answers.
- Huang, J., et al. (2024). [Large language models cannot self-correct reasoning yet.](https://arxiv.org/abs/2310.01798) *ICLR*. Kamoi, R., et al. (2024). [When can LLMs actually correct their own mistakes?](https://arxiv.org/abs/2406.01297) *TACL*. Self-correction works with outside feedback such as tests or tools, not by re-reading.
- Buçinca, Z., Malaya, M. B., & Gajos, K. Z. (2021). [To trust or to think.](https://doi.org/10.1145/3449287) *CSCW*. Cognitive forcing functions reduced overreliance, but users liked them least.

### Oversight, interruptions and decisions

- Bainbridge, L. (1983). [Ironies of automation.](https://doi.org/10.1016/0005-1098%2883%2990046-8) *Automatica*. Parasuraman, R., & Manzey, D. H. (2010). [Complacency and bias in human use of automation.](https://doi.org/10.1177/0018720810376055) *Human Factors*. These explain why monitoring automation is hard, tiring work.
- Adamczyk, P. D., & Bailey, B. P. (2004). [If not now, when?](https://doi.org/10.1145/985692.985715) *CHI*. Interruptions at task breakpoints cost less.
- Altmann, E. M., Trafton, J. G., & Hambrick, D. Z. (2014). [Momentary interruptions can derail the train of thought.](https://doi.org/10.1037/a0030986) *Journal of Experimental Psychology: General*.
- Leroy, S., & Glomb, T. M. (2018). [Tasks interrupted.](https://doi.org/10.1287/orsc.2017.1184) *Organization Science*. A short "ready-to-resume" plan reduces attention residue.
- Ancker, J. S., et al. (2017). [Effects of workload, work complexity, and repeated alerts on alert fatigue.](https://pmc.ncbi.nlm.nih.gov/articles/PMC5387195) *BMC Medical Informatics and Decision Making*. Repeated prompts lose their force.
- Chen et al. (2026). [arXiv 2604.04918.](https://arxiv.org/abs/2604.04918) Preprint. Approving an agent's plan up front reduced later scrutiny.
- Chernev, A., Böckenholt, U., & Goodman, J. (2015). [Choice overload: A conceptual review and meta-analysis.](https://doi.org/10.1016/j.jcps.2014.08.002) *Journal of Consumer Psychology*. Too many options hurt when choices are complex and preferences unclear.

### Sycophancy

- Sharma, M., et al. (2023). [Towards understanding sycophancy in language models.](https://arxiv.org/abs/2310.13548) Models agree with users and cave to pushback, and people prefer it.
- Cheng et al. (2025). [Sycophantic AI decreases prosocial intentions and promotes dependence.](https://arxiv.org/abs/2510.01395) A single sycophantic conversation made people more convinced they were right while raising their trust in the model.

### Prompt wording

- Anthropic. [Claude prompting best practices.](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) Vendor guidance on giving reasons, stating desired behavior, and avoiding over-literal rules.
- Giskard. [Phare benchmark.](https://giskard.ai/knowledge/good-answers-are-not-necessarily-factual-answers-an-analysis-of-hallucination-in-leading-llms) Instructions to answer briefly reduced some models' resistance to hallucination, because correcting a false premise takes words.

## Notes

- **Evidence strength.** The brain fry data comes from a single cross-sectional, self-reported survey. It is not peer-reviewed and has not been replicated, and BCG sells AI-transformation consulting. The workslop study shares an author with it (Kellerman), so the two aren't independent.
- **Extrapolation.** Most of the research on making output easy to check used fixed or simulated AI output in short lab tasks, not real assistants over a working day. The prompt-wording advice is vendor guidance based on internal testing.
- **What the prompt can't reach.** Some of the strongest correlates of brain fry are organizational: workload expectations, manager support, work-life culture and the number of tools in use. A system prompt only changes the load each interaction adds.
- **Dropped from earlier versions.**
  - **Ophir, Nass & Wagner (2009), on media multitasking:** later replications failed.
  - **Two claims attributed to Wiederhold (2026), an editorial in *Cyberpsychology, Behavior, and Social Networking*:** its full text couldn't be verified.
  - **A "pause before deciding" rule:** weak support.
- **Unverified.** The brain fry article's author list comes from news coverage, not the article text. Fernandes et al. and Chen et al. are preprints.
