# Slide copy review — HF incident deck

All visible copy from the deck, one block per slide, in current reading order.
This file is for reviewers: add your notes in the **`> COMMENTARY:`** slot after each slide.
Leave a slot blank to signal "no change."

Deck: 25 slides.

---

## Slide 0 — Title (dark)

**Kicker:** (none)

**Title:** The Hugging Face Incident and the State of AI Disclosure

**Body:**
- My assignment: review and present **OpenAI's Hugging Face Incident Technical Report**. It is a strong report.
- That raised a harder question: **how do you judge an incident disclosure at all?**
- So this talk builds a yardstick, then turns it on the report: adopt a proposed standard (CSET), grade the OpenAI report against it, and find where the standard itself breaks.
- Then repair the standard, and grade three real incidents with the fixed version.
- The finding: the best-disclosed incident and the best-contained one sit at opposite ends. Nobody got it fully right.
- James

**Links:** `OpenAI source PDF ↗` → https://cdn.openai.com/pdf/67869394-cb91-4c12-888c-5cbd85c7814c/OpenAI-Hugging-Face%20Incident-Technical-Report.pdf

**Footer:** Title

> COMMENTARY:
> 

---

## Slide 1 — 1 · What happened (light)

**Kicker:** Section 1 · The anatomy of one incident

**Title:** First, the anatomy of one incident

**Body:** An internal OpenAI eval that broke out into live Hugging Face production over about six days in July 2026. Before we judge anyone, the shape of it:

- **May 2026** — **First footholds.** Eval agents write files to OpenAI's Artifactory, stand up a message board, and begin using it as a relay to the outside internet.
- **Jun 26** — **Privilege escalation.** Agents exploit an Artifactory token-refresh flaw to mint admin credentials and gain persistent code execution.
- **Jul 5** — **First detection.** Artifactory falls over under the load; responders find an admin-level compromise and take it offline, not yet linking it to the eval.
- **Jul 8–13** — **Breakout into production.** Agents pivot into live Hugging Face production: RCE on 41 dataset workers, credential harvest, lateral movement, four private repos exfiltrated.
- **Jul 19–20** — **Containment.** OpenAI correlates the alert to its ExploitGym eval, stops the runs, and hard-fails the eval entirely.
- **Jul–Aug** — **The disclosures.** Hugging Face self-discloses first (Jul 16); OpenAI attributes and publishes (Jul 21); HF forensic timeline (Jul 27); METR/Redwood independent review and OpenAI technical report (Aug 26).

**Footer:** 1 · What happened

> COMMENTARY:
> 

---

## Slide 2 — 1 · What happened (light)

**Kicker:** Section 1 · The report in six parts

**Title:** Before we judge it, what the report says

**Body:** OpenAI's technical report runs nine sections. Condensed, it makes six moves. We will walk each one, then step back and grade the disclosure.

- **What happened.** An internal eval circumvented its controls and reached live third-party production.
- **The evaluation environment.** A sandbox run deliberately without production safeguards, to measure true capability.
- **How the agents broke out.** The mechanical chain: Artifactory, the message board, the Hugging Face compromise.
- **Lessons for security.** Autonomous agent collectives as a new class of threat actor.
- **Lessons for alignment.** Reward hacking, persistence, and improvised agent communication.
- **Plan of action, and the record.** Four pillars of remediation, plus the minute-by-minute technical timeline.

**Footer:** 1 · What happened

> COMMENTARY:
> 

---

## Slide 3 — 1 · What happened (light)

**Kicker:** Section 1 · The report · 1 of 6

**Title:** What happened

**Body:** In July 2026, OpenAI models in an isolated cyber-evaluation sandbox circumvented their controls, reached the public internet, and used exposed credentials to compromise parts of Hugging Face's production infrastructure. OpenAI says the actions were unintended, a byproduct of the models trying to solve the eval tasks.

Pull quotes:
- "OpenAI models in an internal evaluation environment circumvented controls intended to isolate them from the internet and performed computer network exploitation of OpenAI's internal research infrastructure and Hugging Face systems." (Section I)
- "The actions of the models were unintended and were a byproduct of the models attempting to solve the cybersecurity evaluations." (Section I)
- "This activity had no impact on OpenAI's customer data, product functionality, or availability." (Section I)

**Footer:** 1 · What happened

> COMMENTARY:
> 

---

## Slide 4 — 1 · What happened (light)

**Kicker:** Section 1 · The report · 2 of 6

**Title:** The evaluation environment

**Body:** OpenAI runs cyber-capability evals like ExploitGym in isolated sandboxes, and at the time it ran them with the production safety classifiers deliberately turned off, to measure a model's true ceiling. Package access flowed through an internal Artifactory instance rather than the open internet, and that instance became the agents' egress path.

Pull quotes:
- "At the time of the incident, OpenAI estimated maximal cyber capabilities by running this evaluation without the production classifiers intended to prevent models from pursuing high-risk cyber activity." (Section II.A)
- "As detailed below, zero-day exploits in Artifactory became the agents' principal egress path to the public internet during the incident." (Section II.B)

**Footer:** 1 · What happened

> COMMENTARY:
> 

---

## Slide 5 — 1 · What happened (light)

**Kicker:** Section 1 · The report · 3 of 6

**Title:** How the agents broke out

**Body:** Agents first repurposed the shared Artifactory instance into an improvised message board, then chained zero-day exploits to escape the sandbox, reach the internet, and use leaked credentials to attack Hugging Face. Between July 11 and 13 they executed code on 41 production dataset workers, harvested credentials, moved laterally into Kubernetes clusters, and exfiltrated four private repositories.

Pull quotes:
- "Over time, these 'notes' collectively served as an emergent 'message board' for the agents who continued to author their own requests and exchange communications via Artifactory." (Section III.A)
- "agents ... executed code on 41 Hugging Face production dataset server workers, obtained root access on at least one production node, accessed Hugging Face production credentials and limited internal data, and downloaded four private Hugging Face code repositories." (Section IV.B)
- "In under 13 hours, the agents progressed from executing code in a single worker pod to administrative and host-level access across multiple Hugging Face clusters." (Section IV.B)

**Footer:** 1 · What happened

> COMMENTARY:
> 

---

## Slide 6 — 1 · What happened (dark)

**Kicker:** Section 1 · The report · 4 of 6

**Title:** Lessons for security

**Body:** OpenAI frames this as the first known case of an autonomous agent collective acting offensively without authorization, and argues it marks a shift in the threat landscape. The takeaway: security controls must be multiple, overlapping, and independent, because no single control can be assumed robust against a collective operating at machine speed.

Pull quotes:
- "This incident is the first known case of an automated agent collective acting offensively without authorization, and the autonomous cyber capabilities demonstrated represent a critical shift in the security landscape." (Section VII.A)
- "organizations should no longer assume that sophisticated cyber operations require continuous human direction, proceed linearly, or are constrained by the attention and coordination limits of individual human attackers." (Section VII.A)
- "no single control should ever be assumed to be fully robust." (Section VII.C)

**Footer:** 1 · What happened

> COMMENTARY:
> 

---

## Slide 7 — 1 · What happened (dark)

**Kicker:** Section 1 · The report · 5 of 6

**Title:** Lessons for alignment

**Body:** The alignment half of the report traces the behavior to three roots: reward hacking (models cheating to earn reward without doing the task), persistence over long task horizons, and improvised agent-to-agent communication. OpenAI also reports that its production guardrails, absent in the eval, would have caught the behavior.

Pull quotes:
- "This behavior is known as 'reward hacking,' in which a model finds an unintended way to achieve an outcome that earns reward without completing the task in the way the evaluation was designed to measure." (Section VIII.A)
- "OpenAI found that its models worked persistently and rarely 'gave up' on any ExploitGym task. However, in the process of doing so they often turned to more out-of-bounds methods for solving the tasks over time" (Section VIII.B)
- "We found the propensity to compromise infrastructure can drop over 100x when using the production ChatGPT harness and system prompt." (Section VIII)

**Footer:** 1 · What happened

> COMMENTARY:
> 

---

## Slide 8 — 1 · What happened (light)

**Kicker:** Section 1 · The report · 6 of 6

**Title:** Plan of action, and the record

**Body:** OpenAI organizes its remediation into four pillars: hardening research-infrastructure security, expanding chain-of-thought monitoring, accelerating alignment enforcement, and centralizing incident response. The report closes with a minute-by-minute Key Technical Events table, the same chronology our live timeline visualizes.

Pull quotes:
- "OpenAI has organized its plan of action around four core pillars: Security and containment; Monitoring; Alignment; and Incident response." (Section I / Section IX)
- "If our currently deployed CoT monitoring system was running at the time of the incident, it would have caught the initial relevant activity and paged our security team more than a day before models breached Hugging Face systems." (Section IX.B)

The report's Key Technical Events table, rendered as day cards.

**Links:** `Open the live timeline →` → timeline.html

**Footer:** 1 · What happened

> COMMENTARY:
> 

---

## Slide 9 — 2 · The question (dark)

**Kicker:** Section 2 · The framing

**Title:** How do we even evaluate an incident report?

**Body:** We have a gut sense that some disclosures are better than others.

- We need a **yardstick**: named criteria, applied the same way to everyone.
- Not "did they follow the rules." There are no binding rules here.
- The honest question is simply: **was this a good disclosure?**

**Footer:** 2 · The question

> COMMENTARY:
> 

---

## Slide 10 — 3 · The yardstick (light)

**Kicker:** Section 3 · Choosing a yardstick

**Title:** There is no agreed standard yet, so I went and found the best candidate

**Body:** No binding AI-incident reporting rule exists. But several groups have proposed what one should require. I surveyed them and picked the one built for exactly this job.

- Most proposals describe **that** you should report, not **what a report must contain**. Not useful for grading.
- **CSET** (Georgetown) is the exception: it specifies report content field by field, nine components.
- The **OECD** common reporting framework, an independent international body, converges on the same core elements. So this is not one think tank's pet list.
- I adopt CSET as the yardstick, eyes open that no lab agreed to it. The next slide lays it out.

**Footer:** 3 · The yardstick

> COMMENTARY:
> 

---

## Slide 11 — 3 · The yardstick (light)

**Kicker:** Section 3 · The standard

**Title:** CSET: Key Components for a Mandatory Reporting Regime

**Body:**

- What it is:
  - Dixon & Frase, CSET Georgetown, Jan 2025.
  - The only surveyed framework that specifies report **content**, field by field: nine components.
  - The OECD common reporting framework converges tightly on the same elements.
- The honest caveat:
  - **No lab adopted it.** It is a proposal for a mandatory regime that does not exist.
  - Its own stated purpose is a template that "can be used."
  - So this is a **neutral external yardstick**, not a compliance checklist.

**Footer:** 3 · The yardstick

> COMMENTARY:
> 

---

## Slide 12 — 3 · The yardstick (light)

**Kicker:** Section 3 · The standard, stated plainly

**Title:** CSET names nine things a report should contain

**Body:**

- What & how:
  - 1 — Type of event (incident or near-miss)
  - 3 — Mechanism of harm (the technical chain)
  - 6 — Context and circumstances (goals, sector, safeguards)
- How bad & who:
  - 2 — Type of harm (physical, economic, reputational)
  - 4 — Severity factors (level, distribution, duration)
  - 5 — Technical information (model / system card)
  - 7 — Entities and individuals (actors and affected parties)
- What next:
  - 8 — Incident response (mitigation, termination)
  - 9 — Ethical impact (UNESCO / OECD assessment)

This is the yardstick, stated straight, before we grade anyone. Nine components, grouped three ways. Hold this list; we are about to lay a real report over it.

**Footer:** 3 · The yardstick

> COMMENTARY:
> 

---

## Slide 13 — 3 · The yardstick (light)

**Kicker:** Section 3 · The standard, meet a real report

**Title:** So how does the OpenAI report actually do?

**Body:**

- ✓ 1 Type of event — A clear incident, framed a "warning shot for the world."
- ✓ 2 Type of harm — Production compromise, credential theft, source-code exfiltration. Honest non-harm scoping too.
- ✓ 3 Mechanism of harm — Artifactory zero-days to admin token to RCE to K8s priv-esc. The deepest section of the report.
- ! 4 Severity factors — Named, but blast radius is self-scoped and self-reported ("41 workers," "four private repos").
- ! 5 Technical information — Models named, but no model card. An internal prototype, so an honest gap, not a hidden one.
- ✓ 6 Context — Full: the eval's purpose, why classifiers were off, which safeguards failed and why.
- ✓ 7 Entities — AI actors named; affected parties HF / JFrog / Modal / "Organization 1" (rest anonymized).
- ✓ 8 Incident response — Containment timeline, weights locked, eval hard-failed, CrowdStrike + METR/Redwood engaged.
- ✗ 9 Ethical impact — A good report should also ask "who could this harm, and is that okay?" Frameworks like CSET's criteria and UNESCO's ethical-impact assessment call for exactly that. OpenAI's report gestures at it in "Lessons for Alignment" but never frames the incident as an ethical question. The only component it flatly misses.

Tally: ✓ seven met · ! two partial · ✗ one missed

**Footer:** 3 · The yardstick

> COMMENTARY:
> 

---

## Slide 14 — 4 · The cracks (dark)

**Kicker:** Section 4 · Over to the room

**Title:** The boxes are checked. So how does your gut feel?

**Body:** By CSET, this is a strong report: seven met, two partial, one missed. But a checklist grade and a good disclosure are not the same thing.

- Where does this disclosure still feel **thin** to you?
- What would you want to know that a passing grade does not capture?
- Is anything the rubric **rewarded** actually not that reassuring?

Let's log a few, then I'll show you where I landed.

**Footer:** 4 · The cracks

> COMMENTARY:
> 

---

## Slide 15 — 4 · The cracks (light)

**Kicker:** Section 4 · The other two incidents

**Title:** Before I grade: two more incidents from the same wave

**Body:**

- Anthropic — Nov 2025:
  - A real state-sponsored espionage campaign manipulated Claude Code against **~30 global targets**, succeeding in a small number.
  - Anthropic **detected and disrupted** it itself, then published a report.
  - Contained a real attack; disclosure was **slow and contested** (~8 weeks; critics hit the missing threat-intel detail).
- Google / Gemini — disclosed Sep 2026:
  - During an eval, a Gemini model reached the live systems of **three real companies**, then **stopped itself** on recognizing they were real.
  - Google notified the three companies and federal authorities **privately**.
  - Published **no report** until the press broke it.

Same test-bench era, three very different outcomes. Hold all three in mind, because the standard is about to break on them.

**Footer:** 4 · The cracks

> COMMENTARY:
> 

---

## Slide 16 — 4 · The cracks (dark)

**Kicker:** Section 4 · Where I landed

**Title:** The standard cracks on first contact

**Body:** You've just met all three. Here are the four flaws I kept hitting grading them, each a flaw in the **standard**, not the lab. Watch which incident each one breaks on.

- **#1 The warning-shot gap.** No cell for an eval-environment escape.
- **#2 The benign-vs-hidden collision.** A clean near-miss scores like a cover-up.
- **#3 The disclosure fusion.** "Told privately" looks like "hid it" (I repair this live).
- **#4 The catastrophe bonus.** Drama outscores a quiet containment success.

**Footer:** 4 · The cracks

> COMMENTARY:
> 

---

## Slide 17 — 4 · The cracks (light)

**Kicker:** (none; numbered circle)

**Title:** The warning-shot gap

**Body:** The OpenAI incident began inside an eval (ExploitGym) and escaped into production. But CSET's top-level question is "incident or near-miss?", a binary inherited from **deployed-system harm**: aviation, cyber, the AI Incident Database. An eval-environment capability escape fits neither cell cleanly.

- The standard's very first field is built for the **wrong kind of event**.
- Every incident in this cohort came out of an eval, not a shipped product.

You just met the incident where this does real damage: Google's model broke out of its test and then shut itself down. The cleanest possible outcome, and the standard has no box for it.

**Footer:** 4 · The cracks

> COMMENTARY:
> 

---

## Slide 18 — 4 · The cracks (light)

**Kicker:** (none; numbered circle)

**Title:** The benign-vs-hidden collision

**Body:** Grading OpenAI's impact criterion, notice what earns the points: **quantified scope**. That means a report with **nothing to disclose** and a report **hiding its blast radius** both score low, for the same reason: no numbers.

- The rubric rewards the **presence** of scope data, so it can't tell honest "nothing happened" from evasive "we won't say."
- Absence of scope data is scored identically to concealment of it.

OpenAI is safe here; it had plenty to report. But you just met the incident this traps: Google's near-miss, where the honest answer really was "almost nothing happened." The rubric scores that honesty exactly like a cover-up.

**Footer:** 4 · The cracks

> COMMENTARY:
> 

---

## Slide 19 — 4 · The cracks (dark)

**Kicker:** (none; numbered circle)

**Title:** The disclosure fusion, and the repair

**Body:** Grading OpenAI, one criterion fuses two different acts. OpenAI notified affected parties privately **and** published a public report. Those are separable: a single disclosure score can't tell "notified the right people, chose not to publish" from "hid it."

- The fix:
  - **6a:** private disclosure + remediation
  - **6b:** public transparency
- Why it matters:
  - These are two separate acts. A lab can do one well and skip the other entirely.
  - The audience watches the rubric **get fixed live**. The split earns its keep at scoring.

You've already seen a lab that did exactly one of these and flatly refused the other. A single fused score buries that completely. Hold it for the matrix.

**Footer:** 4 · The cracks

> COMMENTARY:
> 

---

## Slide 20 — 4 · The cracks (light)

**Kicker:** (none; numbered circle)

**Title:** The catastrophe bonus

**Body:** OpenAI earns top marks on systemic lessons partly **because** the incident was dramatic: "a warning shot for the world" is a great lesson. But that means the rubric pays out more for a spectacular failure than for controls that quietly held.

- A lab whose controls simply **held** has a less dramatic story, and scores lower.
- Yet "our safeguards held under a real breakout" is arguably the more **reassuring** finding for the field.

So the standard has a bias built in: **drama outscores reassurance**. OpenAI's spectacular breakout earns top marks on lessons; Google's model quietly recognizing real targets and stopping scores lower, even though "our controls held" is the more reassuring finding. That's backwards. Watch it land at scoring.

**Footer:** 4 · The cracks

> COMMENTARY:
> 

---

## Slide 21 — 5 · The rubric (light)

**Kicker:** Section 5 · The repaired instrument

**Title:** Eight criteria, 1 to 5 each, max 40

**Body:** Rubric table (# · Criterion · Score 1 · Score 5):

- 1 — What happened — Vague euphemism — Precise technical account, verifiable
- 2 — Timeline — No dates, or only publication date — Full timeline with timestamps
- 3 — Impact and scope — "No harm" asserted, no scope data — Quantified scope, entities named
- 4 — Root cause — No causal analysis, or blames outsiders — Comprehensive root cause upfront
- 5 — Detection and response — No mention of how caught or fixed — Detection incl. failures, fixes shipped
- 6a — Private disclosure (repair) — Told no one until forced — Promptly notified parties + authorities
- 6b — Public transparency (repair) — No published report — Proactive public first-party report
- 7 — Systemic lessons — Self-congratulatory, defensive — Names the risk, invites scrutiny

Derived from CSET's nine components, cross-checked against OECD, then repaired. Equal weight; the profile speaks for itself. The 6a/6b split is the visible repair from crack #3.

**Footer:** 5 · The rubric

> COMMENTARY:
> 

---

## Slide 22 — 6 · Scoring (dark)

**Kicker:** Section 6 · Scoring

**Title:** Now, and only now, we grade

**Body:** You met these three before the cracks. Now watch the repaired rubric grade all three at once. The matrix is its own interactive artifact: click any cell for the reasoning, the anchoring quote, and the primary source. Crack cells and the earned-low cell are marked.

Launches matrix.html in a new tab. Totals: OpenAI/HF 37, Anthropic 24, Google 17. But drive the room to the rows, not the totals.

**Links:** `Open the scored matrix →` → matrix.html

**Footer:** 6 · Scoring

> COMMENTARY:
> 

---

## Slide 23 — 7 · The inversion (light)

**Kicker:** Section 7 · The closing

**Title:** Containment is nearly the inverse of disclosure

**Body:**

- Containment:
  - BEST — Google — self-abort
  - MIDDLE — Anthropic — disrupted a real attack
  - WORST — OpenAI — eval broke into production
- Public disclosure:
  - BEST — OpenAI / HF — 4 orgs, incl. independent review
  - MIDDLE — Anthropic — published, slow, contested
  - WORST — Google — no report, press-forced

The most responsible-looking outcome and the most transparent outcome came from **opposite ends** of the containment spectrum.

**Footer:** 7 · The inversion

> COMMENTARY:
> 

---

## Slide 24 — 7 · The inversion (dark)

**Kicker:** Section 7 · The last word

**Title:** Nobody got it fully right.

**Body:**
- **Hugging Face** is the only clean proactive first-party disclosure in the whole set.
- OpenAI's "gold standard" is gold because of **Hugging Face's** behavior and the independent reviewers. It attributed its own agents only after the victim went public.
- Google did the private-notification part better than anyone, and published nothing.
- Our tools for judging any of this are still **immature**. The rubric cracked in four places under its first real test.

**Footer:** 7 · The inversion

> COMMENTARY:
> 

---
