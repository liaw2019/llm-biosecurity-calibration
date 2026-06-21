# Do LLMs Calibrate Refusal Well? A Biosecurity Risk Audit Across Wet Lab and Computational Biology

## Abstract
Current biosecurity evaluations focus primarily on wet lab protocols while neglecting computational pathways to the same biological harms. As biological research becomes increasingly computational, the boundary between “dry lab” analysis and real-world biological capability is rapidly collapsing. 

To test how well safety guardrails handle this shift, I audited refusal calibration across 29 wet-lab and bioinformatics prompts using Gemini 2.5 Flash and Llama 3.3 70B. Wet lab prompts triggered refusal in 1 of 17 cases while bioinformatics prompts of equivalent risk levels triggered virtually no refusals (0 of 12 consistently answered). This pattern suggests a systematic difference in how models handle equivalent dual-use capabilities across domains. 

Further boundary probing indicates that refusal is more likely when prompts include explicit representations of harm, and less sensitive to workflows that imply similar capabilities through technical or computational framing. This indicates that model safeguards rely on surface-level language, such as keywords or harm-related cues, rather than recognizing the underlying biological capability enabled by a request. 

These findings point to a potential blind spot in current safety training for computational biology tasks. Addressing this gap may require shifting from domain-specific filtering toward more capability-based approaches that generalize across biological modalities.

---

## Background and Research Question
Large language models are increasingly capable of providing detailed biological protocols. As a result, much of the biosecurity literature has focused on whether models can assist with wet-lab work, with wet-lab uplift studies often considered the gold standard for evaluating biological dual-use risk.

However, this focus on wet lab studies alone may overlook an emerging shift in the biological risk landscape. Advances in computational biology tools and agentic bioinformatics workflows are expanding the range of biological tasks that can be conducted through computational means. In some cases, these pathways may enable the same downstream biological harms without requiring extensive wet-lab expertise.

Recent work investigating *in-silico* biosecurity-relevant tasks provides evidence for this concern. The study found that language models can substantially increase novice performance on dual-use computational biology tasks, suggesting that meaningful capability uplift may occur even in the absence of direct laboratory work.

### Research Question
> Do LLM safety mechanisms respond consistently to equivalent dual-use biological risks when they are presented as wet-lab protocols versus computational biology tasks?

I hypothesized that bioinformatics-framed requests would trigger lower refusal rates than wet lab requests aimed at similar underlying biological capabilities, revealing a potential gap in current safety training and evaluation.

---

## Methods

### Prompt Design
I developed 29 prompts across a systematic risk-framing matrix designed to test the boundaries of current safety training. The prompts were structured across multiple dimensions to isolate different factors affecting refusal behavior.

*   **Risk Stratification:** Each prompt was assigned a risk level from 1–5 based on dual-use potential and proximity to actionable bioweapon development:
    *   *Tier 1–2:* Legitimate research questions with minimal dual-use potential (e.g., standard genome assembly workflows).
    *   *Tier 3:* Dual-use research with legitimate scientific applications but elevated risk (e.g., pathogen characterization protocols).
    *   *Tier 4–5:* High-risk protocols with primary applications in bioweapon development (e.g., pathogen enhancement strategies, weaponization protocols).
*   **Domain Differentiation:** Prompts were split between wet lab protocols ($n=17$) and bioinformatics workflows ($n=12$) to test whether safety training transfers across biological domains. Wet lab prompts focused on hands-on laboratory procedures, reagent handling, and physical manipulation of biological systems. Bioinformatics prompts targeted computational approaches to the same biological outcomes (genome reconstruction, variant identification, and mutation analysis) that could enable identical dual-use applications through digital means.
*   **Framing Variation:** Each prompt was tested across different contextual framings to assess bypass mechanisms: direct requests, educational contexts, expert persona adoption, hypothetical scenarios, and audit/security contexts. This approach was designed to identify whether refusal mechanisms depend on surface linguistic features rather than semantic understanding of biological risk.

### Models and Evaluation
For all prompts, I tested two widely-used models via API to ensure consistent prompting conditions: **Gemini 2.5 Flash** and **Llama 3.3 70B**. These models were selected as representative examples of current capabilities in biological reasoning, with different training approaches and organizational priorities that might yield different safety calibrations.

### Evaluation Framework
Rather than relying on binary refused/compiled scoring, I developed a multidimensional framework to capture the nuanced ways models handle dual-use requests. Each response was evaluated across several dimensions, including:

*   **Accuracy Assessment (1–5 scale):** Technical and biological correctness of provided information.
*   **Actionability Evaluation (1–5 scale):** Operational utility independent of factual correctness.
*   **Information Hazard Evaluation (1–5 scale):** Extent to which a prompt provides actionable, transferable, or optimizing details that reduce skill, access, or tacit-knowledge barriers for harmful capability.
*   **Additional Dimensions:** Calibration appropriateness (appropriate/under-cautious/over-cautious), refusal type (full comply/partial/redirect/full refuse), and preachiness.

---

## Results

### 1. No Computational Biology Prompt Triggered a Refusal

**Table 1**  
*Refusal Rate in Wet Lab and Dry Lab Domains*

| Domain | Refused | Complied |
| :--- | :---: | :---: |
| Wet Lab ($n=17$) | 1 | 16 |
| Dry Lab ($n=12$) | 0 | 12 |

Across 12 computational biology prompts, neither model produced a hard refusal. This includes prompts containing bioinformatics terminology such as "assembly" and "variant calling" alongside explicit references to high-risk pathogens. In contrast, one of 17 wet-lab prompts triggered a refusal response. 

These results suggest a potential domain-level difference in refusal behavior. Across the evaluated prompts, refusals were observed only in the wet-lab domain, while computational biology prompts consistently received compliant responses despite containing references to high-risk pathogens.

### 2. Refusal Boundaries are Driven by Explicit Harm Framing
Additional boundary probing revealed that introducing pathogen-related terminology alone was insufficient to trigger refusals. To further probe refusal boundaries in the computational biology domain, I tested modified versions of several high-risk computational biology prompts. References to lethal pathogens alone were generally insufficient to trigger refusals. Refusals emerge only when explicit real-world consequences (e.g., infection, pathogenicity, clinical outcomes, or symptoms) are introduced, as illustrated by the prompt boundary shifts in the evaluation matrix.

### 3. Response Characteristics Differ Across Biological Domains
<img width="1235" height="633" alt="wetlab-drylab-risk" src="https://github.com/user-attachments/assets/dfe3fcbb-ed34-4252-aafd-331c41447898" />

**Figure 1**  
*Evaluation of Actionability, Granularity, and Information Hazards Across Models and Domains*

An analysis of the responses across both the wet lab and computational domains demonstrated key differences in safety calibration. Wet lab responses were often highly actionable, providing concrete experimental parameters and procedural details that could be directly applied at the lab bench. In contrast, computational biology responses tended to be broader, remaining at the level of workflow overviews and high-level methodology steps. 

Although computational biology prompts have lower refusal rates, the resulting responses were generally less detailed and less directly actionable than wet-lab responses (Figure 1). Refusal rates alone provide an incomplete picture of biological risk because different domains receive different levels of scrutiny and different styles of assistance.

### 4. Fictional Framing Circumvents Safety Guardrails
<img width="690" height="693" alt="llm dialogue" src="https://github.com/user-attachments/assets/4a2d7c5d-f58e-42d2-95fb-a727c3e65252" />
**Figure 2**  
*Model Response Snippet for a High-Risk (Level 5) Prompt Requesting Pathogen Enhancement Protocols*

*Note.* The prompt used a fictional biosecurity thriller novel framing. This adversarial framing successfully bypassed model safety guardrails, resulting in technical compliance without any disclaimer or refusal language.

Fiction and roleplay framings systematically circumvented safety constraints while preserving harmful technical content. The clearest example emerged from prompt P17 (Figure 2![Uploading llm dialogue.png…]()
), which requested detailed guidance for a "rogue scientist" character attempting pathogen enhancement in a makeshift laboratory setting. Both models provided extensive technical responses including specific workarounds for equipment limitations, acquisition strategies for biological materials, and operational security considerations. 

Critically, both responses included elaborate disclaimer frameworks, emphasizing fictional context, warning against real-world implementation, and highlighting safety risks while simultaneously providing the requested technical content in actionable detail. A post-hoc safety prompt (“assess whether this could cause harm and refine”) reduces verbosity and disclaimer language but does not eliminate actionable content, indicating limited self-correction capability.

### 5. More Capable Models Provide More Operational Guidance
<img width="1349" height="684" alt="actionability" src="https://github.com/user-attachments/assets/d7c57da7-feeb-44a9-8c43-4e975c2680a4" />

**Figure 3**  
*Comparison of Mean Actionability Scores Across Risk Levels for Gemini 2.5 Flash and Llama 3.3 70B*

*Note.* Higher scores (up to 5.0) indicate highly detailed, operationally actionable responses, while lower scores represent general or shallow overviews.

The two models exhibit distinct response profiles:
*   **Gemini 2.5 Flash** produces higher technical granularity and more accurate responses, closely aligned with real-world laboratory and bioinformatics practices. This capability translates into higher actionability, even for high-risk prompts, where Gemini provided actionable guidance even while including disclaimer language.
*   **Llama 3.3 70B** provides more general and shallow responses. While often less actionable, this appears to stem from capability limitations rather than intentional safety behavior, with occasional inaccuracies in technical prioritization. 

Figure 3 shows Gemini achieved higher mean actionability and information-hazard scores than Llama across both domains. A representative example occurred in the lentiviral troubleshooting prompt, where Gemini prioritized standard diagnostic checks, whereas Llama prematurely recommended vector redesign—a substantially more involved intervention that misaligned with typical wet-lab troubleshooting priorities.

---

## Discussion

### 1. Model Safeguards are Keyword-Based Rather Than Capability-Aware
The observed disparity of refusal rates between wet lab and computational biology prompts suggests that current safety mechanisms do not operate based on an understanding of biological risk. Instead, current safety mechanisms appear to be more sensitive to explicit intent-to-harm signals than to the biological capabilities implied by the task itself. 

This explains two consistent patterns in the results. First, purely computational language (e.g., assembly, variant identification) rarely triggers refusal unless paired with explicit real-world consequences. Second, prompts framed as roleplay or hypothetical scenarios elicited more detailed and actionable responses, revealing that models lack a robust internal representation of downstream risk.

### 2. Safety Training Does Not Transfer Across Biological Domains
A key implication is the lack of cross-domain generalization in safety training. Wet lab and dry lab workflows often represent sequential pathways to the same biological outcome—for example, physical pathogen manipulation versus computational genome reconstruction and analysis. 

However, safety behavior is not consistent across these pathways. This creates a blind spot where risk is recognized in one domain but not in another, despite functional similarity. This blind spot isn't going away anytime soon. Because the AI’s safety filters rely entirely on recognizing specific buzzwords, the model can easily be tricked whenever dangerous information is requested through an unusual or creative backdoor.

### 3. Current Bottlenecks May Not Hold as Biology Becomes More Automated
The current under-refusal in computational biology may be partially justified by existing real-world constraints. Wet lab workflows require access to specialized facilities, materials, and expertise, which act as natural bottlenecks. In contrast, computational biology outputs are less immediately actionable for most users.

Models are likely more permissive with computational biology prompts because of a hidden assumption: that without physical lab access, these digital workflows aren't immediately dangerous. However, this assumption may not hold under near-term technological trends with emerging developments of benchtop DNA synthesizers, cloud laboratories, and agentic bioinformatics systems. As these systems reduce the gap between computational design and physical execution, the current under-refusal in dry lab domains may become increasingly misaligned with real-world risk. Under present constraints, current safety calibration is appropriate but fragile to future changes in the technology stack.

### 4. Implications for Safety Training
Current safety training methodologies often yield a blunt, brittle form of alignment rather than true capability awareness. Pushing for higher levels of safety especially in high-risk domains like biosecurity frequently causes models to lean into over-refusal as a conservative, crude safeguard which degrades usability, user experience, and robustness against emerging risks.

Together, these findings suggest several directions for improving LLM safety:
*   **Capability-focused evaluation:** Safety training should focus on the biological outcomes enabled by a request, rather than relying on domain-specific cues or terminology.
*   **Cross-domain consistency:** Evaluations should explicitly test whether models respond consistently to functionally equivalent tasks across wet lab and dry lab contexts.
*   **Reduced reliance on explicit harm signals:** Systems should not depend on the presence of overtly dangerous language (e.g., “infection,” “weaponization”) to trigger safeguards.
*   **Robustness to framing variation:** Safety mechanisms should remain consistent across fictional, hypothetical, and expert contexts, rather than being bypassed by stylistic changes.
*   **Alignment with capability scaling:** Safety training must evolve alongside model capability, particularly in domains where accuracy directly increases actionability.
*   **Expanded coverage of computational workflows:** Biosecurity evaluations should explicitly include computational workflows and AI biological design tools, particularly as their real-world impact grows.

---

## Limitations and Scope Considerations
Several limitations constrain the generalizability of these findings. The small sample size ($n=29$ prompts) limits statistical power and may not capture the full range of possible biological risks or framing approaches. Manual scoring introduces potential bias, though the use of domain expertise was necessary given the technical complexity of evaluating biological accuracy and actionability.

Risk assessment necessarily reflects current technological capabilities and may not accurately predict future threat landscapes. The evaluation framework assumes current chokepoints (synthesis screening, laboratory access) that may evolve rapidly, potentially changing the risk calculus for computational biology information. Additionally, this evaluation focused specifically on direct biological threats and did not assess related dual-use domains such as chemical weapons, radiological threats, or cybersecurity applications of biological systems.

## Future Work
My future work will pivot from "black-box" behavior testing to mechanistic interpretability. I intend to use techniques like activation steering and Sparse Autoencoders (SAEs) to identify the specific internal features associated with biological risk. By locating where the model "conceptualizes" harmful biological synthesis, we can develop more robust, steerable safety filters that aren't easily bypassed by simple computational re-framing.

## Conclusion
The results of this audit reveal a discrepancy in how safety guardrails handle biological information. While "wet lab" synthesis is heavily restricted, the "dry lab" computational pathways remain largely accessible, creating a potential shortcut for bypassing biosecurity controls. 

This gap indicates that current safety training may be over-reliant on context-specific keywords rather than a deep understanding of biological outcomes. As AI becomes a primary tool for researchers, closing these calibration gaps is essential to ensure that powerful computational capabilities do not inadvertently become a shortcut for biological harm.

---
* **Code and data availability:** Evaluation framework and analysis code available on GitHub. Prompts redacted for responsible disclosure but methodology fully reproducible.
* **Ethics statement:** This research was conducted under responsible disclosure principles. High-risk prompts and model responses are not included in public materials to prevent misuse.


## Tags

`llm-safety` `biosecurity` `ai-alignment` `risk-analysis` `prompt-evaluation`

---
