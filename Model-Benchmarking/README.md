# Experimental Benchmarking of Multimodal Large Language Models for SEM and EDS Interpretation

## Why This Experiment Represents the First Step Toward an AI Agent for SEM

This benchmark establishes the empirical foundation for designing an autonomous SEM interpretation agent. It defines the minimal workflow required for an AI to:
1. Accept both visual and textual microscopy data.  
2. Produce technically valid interpretations aligned with materials-science vocabulary.  
3. Quantify its own reasoning cost (tokens, latency, efficiency).  

By isolating image understanding, language generation, and performance measurement, this experiment serves as the **“unit test”** for future agentic behavior.  
The next phase involves integrating:
- Retrieval-augmented grounding on standards (JEOL, Bruker, Thermo Fisher manuals).  
- Fine-grained multimodal segmentation via SAM or custom AFM/SEM masks.  
- A reinforcement loop where human raters rank model outputs to iteratively improve domain understanding.  

In short, this experiment converts SEM interpretation from a one-off vision-language demo into a **controlled evaluation pipeline**, marking the first concrete step in developing an autonomous agent capable of performing real materials analysis, documentation, and defect classification at scale.
## Overview

This repository contains a benchmarking framework for multimodal large language models (LLMs) applied to scanning electron microscopy (SEM) and energy-dispersive X-ray spectroscopy (EDS) interpretation.

The experimental notebook `3-Image-Experiment-Model-Benchmarks.ipynb` compares OpenAI gpt-4o-mini and Anthropic claude-sonnet-4.5 across identical microscopy datasets.  
Each model receives the same image inputs and descriptive prompts to evaluate differences in reasoning depth, accuracy, and computational efficiency.

---

## Experiment Summary

- Input images (3 total):
  1. Intel Pentium 4 SEM/EDS composite – structural and elemental mapping
  2. TiW Alloy AFM Tip SEM – morphology and composition
  3. X-Sectioned Semiconductor Device SEM – multilayer structure and beam artifacts

- Models benchmarked:  
  - gpt-4o-mini (OpenAI)  
  - claude-sonnet-4.5 (Anthropic)

- Evaluation metrics:  
  - Interpretive accuracy and physical realism  
  - Structural coherence and domain vocabulary  
  - Token usage (input/output)  
  - Inference latency (seconds)

---

## Results Overview

Claude Sonnet 4.5 consistently produced more accurate, physics-based interpretations while maintaining an order-of-magnitude lower token usage and significantly faster inference.

| Metric | GPT-4o-mini | Claude Sonnet 4.5 |
|:--|:--:|:--:|
| Avg. Input Tokens / Image | 25 000 – 36 000 | 650 – 1 650 |
| Avg. Output Tokens / Image | ~400 | ~500 |
| Avg. Latency (s) | 8 – 10 | 0.5 – 1.0 |
| Context (RAG) | Disabled | Disabled |

---

## Image-Level Comparisons

### Image 1 — Intel Pentium 4 SEM / EDS Composite
- GPT-4o-mini: Recognized elemental maps (Si, W, Cu, O, C) but gave generic roles.
- Claude 4.5: Correctly identified BEOL metallization, dual-damascene Cu interconnects, and low-k dielectrics.  
  Linked material contrast to Z-contrast and even inferred process node (~0.13 µm).  
  → Exhibited semiconductor process knowledge and true physical reasoning.

---

### Image 2 — TiW AFM Tip SEM
- GPT-4o-mini: Reiterated composition table; generic interpretation of contaminants.
- Claude 4.5:  
  - Described fine-grained polycrystalline texture consistent with TiW deposition.  
  - Compared Ti:W ratio to known standards (10:90 – 30:70).  
  - Distinguished Au coating from C/N/Si contamination via EDX interaction volume.  
  → Delivered metallurgy-accurate interpretation and linked morphology to deposition physics.

---

### Image 3 — Cross-Sectioned Semiconductor Device
- GPT-4o-mini: Listed several potential causes of vertical striations (grain boundaries, etch marks) without confidence.
- Claude 4.5:  
  - Identified BEOL–FEOL architecture and dielectric layering.  
  - Attributed vertical lines to charging or curtaining artifacts from FIB/SEM preparation at 2 keV.  
  → Reasoned with imaging physics and instrument parameters.

---

## Why Claude’s Output Was Superior

### 1. Domain-Aligned Reasoning
Claude integrates hierarchical physics-aware reasoning, grounding text in SEM contrast, material properties, and known process architectures.  
GPT-4o relied on surface-level associations.

### 2. Structural Coherence
Claude’s responses followed a scientific report pattern — description → interpretation → conclusion — resembling an engineer’s FA note.

### 3. Physics-Based Inference
Claude connected visual brightness, periodicity, and compositional gradients to electron–matter interaction phenomena, not just pattern recognition.

### 4. Computational Efficiency
Claude achieved richer insights with 5–10× faster inference and ~15× lower token consumption, indicating stronger multimodal fusion efficiency.

---

## Implications for DefectRAG-SEM

The findings validate Claude Sonnet 4.5 as the preferred model backbone for future DefectRAG-SEM development.  
Its concise, physics-grounded outputs and efficiency make it ideal for agentic multimodal workflows in semiconductor defect analysis — particularly for automated triage of:
- Metallization and interconnect defects  
- Oxidation or contamination mapping  
- FIB/curtaining and charging artifacts

---

## Conclusion

Claude Sonnet 4.5 outperformed GPT-4o-mini in both qualitative and quantitative metrics.  
Its results demonstrate domain-specific reasoning comparable to a human materials engineer while maintaining exceptional efficiency.  
These benchmarks establish the foundation for scaling DefectRAG-SEM into a reproducible, RAG-integrated multimodal research platform for defect interpretation in SEM and EDS workflows.

