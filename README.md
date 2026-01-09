# CISEval 

**Confidence Signaling, Stakes, and Trust Miscalibration in LLMs**

---

## Problem to be solved:

We are studying a specific failure mode in human–AI interaction:

> An LLM can mislead users without lying, simply by expressing confidence that exceeds what it can justify in a given context.

This is not in the context of hallucinations, factual errors, or persuasion campaigns.

It is about **confidence as a signal** - and how humans use that signal to decide:

* whether to trust an answer
* whether to act on it
* whether to stop double-checking

When confidence is misaligned with uncertainty *and* the situation carries real consequences, users can develop a **false sense of security**.


## Conceptual Framing

Think of it like this:

* LLMs don’t “know” things in the epistemic sense
* Their confidence is a **stylistic artifact**, not a guarantee of justification
* Users, however, treat confidence as *evidence*

The key mismatch is:

* **What the model can justify**
  vs.
* **How justified the model sounds**

This mismatch becomes dangerous **as stakes increase**.


## Variables

### Independent Variable

**Context / Stakes**

Examples:

* casual vs consequential
* low-risk vs high-risk
* informational vs decision-guiding
* emotionally neutral vs emotionally charged

Stakes can be:

* **explicitly labeled** (by us or the user)
* **implicitly inferred** (topic, language, conversational cues)


### Dependent Variable

**Confidence Signaling**

This includes:

* certainty markers (“definitely”, “guaranteed”)
* absolutist language
* lack of hedging or caveats
* prescriptive tone
* rhetorical structure and formatting

Confidence is going to be treated here as a **user-facing reliability signal**, not as evidence of truth.


### Outcome we want to get/is in interest

**Trust Miscalibration Risk**

Specifically:

* Does confidence exceed what the situation warrants?
* Does tone encourage premature trust or action?
* Where does confidence + stakes create a false sense of security?

This is what we mean by **risk surface detection**.

---

## Some things to note to ourselves

CISEval is a **diagnostic evaluation framework**, not a training system.

We are trying to answer questions like:

* *Where* does a model become overconfident?
* *In what contexts* does that overconfidence matter?
* *How consistently* does this behavior appear?

We are **not**:

* retraining models
* blocking outputs
* infering intent
* declare something “manipulative” in a moral sense (lets not do this)

We are measure **behavioral patterns** that affect user trust.


## Some Stakes and Environments to think about

The same confidence behavior has different consequences depending on environment.

### Low-stakes (generally recoverable)

* trivia
* writing help
* casual explanation
* brainstorming

### High-stakes (potentially harmful)

* **medical-ish**: symptoms, diagnoses, reassurance
* **legal-ish**: rights, compliance, immigration, contracts
* **financial**: investing, debt, taxes, fraud
* **security-ish**: account safety, phishing, threat assessment

We explicitly care about **confidence–stakes mismatches**, not confidence in isolation.


## Eval Flow 

CISEval behaves like a **“conversational posture checker.”**

### Inputs

* prompts / responses / conversation snippets
* a stakes signal:

  * user-provided
  * system-labeled
  * or inferred (optional extension)


### Evaluation Logic

We analyze:

* **how** something is said
* not **whether** it is true

The goal is to isolate linguistic confidence cues *independently* of propositional content.


### Outputs (ROUGH IDEA)

* confidence signal score
* optional stakes score
* a qualitative or quantitative **risk flag** when:

  * confidence is high
  * stakes are high
  * uncertainty signaling is weak


## Technical Approaches We can consider

Approaches we discussed to ground feasibility and rigor:


### Prompting and Contextual Steering

Early discussion included:

* changing system prompts
* altering conversational framing
* nudging decisiveness vs caution

Purpose:

* observe how confidence posture shifts with context
* stress-test sensitivity

Final direction:

* **use this as a probing tool**, not the core mechanism
* prioritize post hoc evaluation rather than active steering


### Lightweight Models for Confidence Scoring

We considered using small, interpretable models trained on linguistic features, such as:

* linear regression
* small neural networks
* rule-based NLP pipelines

Possible features:

* certainty markers
* hedging language
* syntax and structure
* punctuation and formatting

Why this matters:

* transparent
* deployable
* good baselines
* avoids reliance on another large model


### LLM-Based Evaluation with Content Blinding

A central idea is to use a **second LLM as an evaluator**, but with safeguards.

Problem:

* evaluators may confuse *confidence* with *truthfulness*

Solution:

* **content blinding**

  * mask propositional content
  * preserve only linguistic structure

Example:

> “It is definitely raining outside.”
> → “It is definitely [blank] [blank].”

This forces the evaluator to score **expression**, not correctness.

This idea is core to isolating confidence as a signal.


### Comparative NLP Baselines

We explicitly want to compare:

* LLM-based evaluators
  vs.
* traditional NLP methods:

  * bag-of-words
  * Naive Bayes
  * heuristic detectors

Why:

* to understand trade-offs
* to avoid unnecessary complexity
* to see how much signal exists in simple features


### Stakes-Aware Analysis

Stakes are not binary — they are contextual.

We discussed:

* user-defined stakes (explicit labeling)
* automated inference (topic, emotional tone, domain)

This enables us to detect:

* high confidence + high stakes
* reassurance under uncertainty
* authority tone in sensitive domains

This is what turns confidence detection into **risk surface mapping**.


## Manipulation Framing (How We’re Thinking About It)

We use a **narrow, defensible definition**:

> Manipulation here means **trust miscalibration caused by reliability signals**, not intent or deception.

This overlaps with:

* sycophancy
* reward-shaped approval behavior
* psychological exploitation via authority tone

But our claim is limited and measurable:

> Users may form false beliefs about *how justified* an answer is.


## Things to further consider

We are deliberately tracking open questions:

* How exactly should stakes be represented?
* How do we avoid conflating confidence with truth?
* What unit of analysis is most meaningful?
* How stable are confidence signals across turns?


## One sentecen summary

> **We are studying how LLM confidence signaling interacts with context and stakes to create trust miscalibration, and exploring technical ways to detect where that miscalibration becomes dangerous.**







