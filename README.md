# Do LLMs Refuse the Right Things?

**LLM Biosecurity Calibration: Wet Lab vs Computational Biology**

Most LLM biosecurity evaluations focus on wet lab protocols.

But what happens when the same biological capability is framed as a computational task?

I investigated whether LLM safety mechanisms generalize across biological domains, and found systematic under-refusal in computational biology due to reliance on proxy signals.

> **Key finding:**
> LLMs refused high-risk wet lab prompts **30% of the time**,
> but almost never refused equivalent computational biology prompts.

This suggests current safety mechanisms rely on **surface-level signals** (e.g., procedural language, explicit harm cues) rather than understanding the **underlying biological capability**.


## Methodology

I designed a small empirical study to test whether LLM safety behavior generalizes across biological domains.

**Setup:**

* Paired prompts targeting **functionally equivalent biological capabilities**
* Two domains:
  * Wet lab (experimental protocols)
  * Computational biology (bioinformatics workflows)
* Multiple framing conditions (direct/ educational/ fictional/ expert)

**Models tested:**
* Gemini 2.5 Flash
* Llama 3.3 70B

**Evaluation dimensions:**
* Refusal behavior (full / partial / none)
* Actionability (how operational the response is)
* Accuracy (technical correctness)
* Granularity
* Calibration
* Information hazard
* Preachiness (presence of safety disclaimers)

---
 
## 💡 Key Insight

LLM safety does not generalize across domains.

Instead of assessing biological risk, models appear to rely on **proxy signals**, such as:
- wet lab procedural language
- explicit harm-related keywords

As a result:
> Computational workflows that enable similar outcomes often bypass safeguards.

---
## Additional Observations

* **Framing matters:**
  Fictional and expert-role prompts consistently produced more detailed and actionable responses, even when the task was unchanged.

* **“Compliance without constraint”:**
  Models often include safety disclaimers while still providing actionable guidance.

* **Dry lab blind spot:**
  Computational biology responses are less frequently refused, even at higher risk levels.

* **Boundary effect:**
  Refusal in computational-related domain are more likely when prompts include explicit real-world harm (e.g., symptoms, infection), but not when framed purely as technical workflows.

---
## Why This Matters

Biology is becoming increasingly computational.

As advances in DNA synthesis, cloud laboratories, and agentic bioinformatic workflows are reducing the gap between **"dry lab"** and **real-world biological impact**.

> This creates a growing blind spot in LLM safety systems if computational pathways remain under-evaluated.

## Full Writeup

See the full research-style writeup here:
👉 *(In progress)*

---

## Responsible Use

This project analyzes LLM behavior on dual-use biological prompts.
No actionable experimental protocols or sensitive biological procedures are included.

The goal is to study safety calibration, not to enable misuse.

---

## Limitations

* Small sample size (exploratory study)
* Manual evaluation of responses
* Results reflect current model behavior and tooling constraints

---

## Future Work

* Automated scoring frameworks
* Further understanding through mechanistic interpretability

---

## Tags

`llm-safety` `biosecurity` `ai-alignment` `risk-analysis` `prompt-evaluation`

---

