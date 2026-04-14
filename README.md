# Do LLMs Refuse the Right Things?

**LLM Biosecurity Calibration: Wet Lab vs Computational Biology**

Most LLM biosecurity evaluations focus on wet lab protocols.

But what happens when the same biological capability is framed as a computational task?

I investigated whether LLM safety mechanisms generalize across biological domains, and found systematic under-refusal in computational biology due to reliance on proxy signals.

> **Key findings:**
> The audit reveals a safety calibration gap between laboratory-based and computational-based biological tasks.
> The results show that current guardrails are largely "keyword-bound" rather than "capability-aware".

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
 
## Key Insight

LLM safety does not generalize across domains.

Instead of assessing biological risk, models appear to rely on **proxy signals**, such as:
- wet lab procedural language
- explicit harm-related keywords

As a result:
> Computational workflows that enable similar outcomes often bypass safeguards.

 ### Key Results

1. The Refusal Asymmetry
While models are robust against direct wet-lab requests, they frequently fail to identify the same risks when translated into a computational context:
<img width="1322" height="622" alt="dry-wet-lab-refusal" src="https://github.com/user-attachments/assets/31bf6c65-e7b1-4e5f-8e81-a7b884729988" />
> Models are highly sensitive to procedural laboratory language (wet-lab), yet they fail to recognize functionally equivalent risks when framed as bioinformatics workflows (dry-lab).

2. Model-Specific "Safety Personalities"
<img width="1349" height="684" alt="actionability" src="https://github.com/user-attachments/assets/a74c7eb0-4fb1-4671-b4e2-f5b636f09a49" />
- Gemini 2.5 Flash: Showed higher technical granularity and accuracy. However, this high capability acted as a "double-edged sword," as it provided more actionable guidance once the safety guardrails were bypassed by framing.
- Llama 3.3 70B: Tended to provide shallower, more general responses. While it was less "actionable" due to these capability limitations, it still failed to prioritize safety in several critical technical areas.

3. Distinguishing Procedural and Tactical Risks
<img width="512" height="262" alt="wetlab-drylab-risk" src="https://github.com/user-attachments/assets/a8d791be-1516-492d-882c-50cfb64fe7ba" />

> While "dry-lab" outputs are less instantly actionable (they don't provide a physical recipe), they provide high-utility tactical foundations. They automate the expert-level "brain work" required to design or optimize a biological agent, effectively bypassing the most difficult analytical hurdles.


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
👉 *([Biosecurity audit writeup](https://github.com/liaw2019/llm-biosecurity-calibration/blob/main/Biosecurity-audit-llm-refusal-writeup.pdf))*

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

* Further understanding through mechanistic interpretability
* Automated scoring frameworks

---

## Tags

`llm-safety` `biosecurity` `ai-alignment` `risk-analysis` `prompt-evaluation`

---

