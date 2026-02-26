# Laserify: Supplementary Materials

Official repository for the CHI 2026 Late-Breaking Work:
**"Laserify: From Multimodal Input to Fabrication-Ready Laser Cut Plans"**

## Overview

Laserify is a hybrid pipeline that transforms images of laser-cut objects into fabrication-ready 2D cut plans. It uses a neurosymbolic approach, combining the semantic reasoning of Vision-Language Models (VLMs) with the geometric precision of deterministic algorithms.

## Models Used

Our evaluation identified specific models that excelled at different stages of the reasoning chain:

- **Stage 1 — Reference image generation:** OpenAI Sora (image generation)
- **Stage 2a — Scene and part discovery:** gemini-3-pro-preview (gpt-4o, gpt-5.1, claude sonnet 4.5 were also tested, with inferior results)
- **Stage 2b — Geometric scaffolding:** gemini-3-pro-preview
- **Stage 2c — Outline extraction:** gpt-5.1-2025-11-13 (gemini was also tested, producing more hallucinations and lack of adherence with instructions)
- **Baseline Comparisons:** GPT-5.1 for direct extraction; Gemini-3 for Image-to-OpenSCAD.

### Laserify Prompts

The `prompts/laserify/` folder contains the structured prompts used in Stage 2 (VLM-driven Semantic Interpretation):

- `stage2a.txt` — Scene analysis and part identification
- `stage2b.txt` — Construction planes and bounding rectangles
- `stage2c.json` — Per-part binary mask generation (multi-turn protocol)

**Note on Stage 2c:** This stage uses a multi-turn conversation protocol. The JSON file contains three prompts: `system_prompt` (sets the model's role), `initial_prompt` (provides scene context and rules), and `followup_prompt` (requests individual part generation). The initial prompt is sent once with the source image and a part list extracted from Stage 2b output; the followup prompt is then called iteratively for each part.

### Baseline Prompts

The `prompts/baselines/` folder contains prompts used for the comparison baselines in our evaluation:

- `direct-outline-extraction.txt` — Single-step Image-to-outlines generation
- `image-to-openscad.txt` — Single-step Image-to-CAD (OpenSCAD) generation

## Laserify is a research project developed at the Technion - Israel Institute of Technology (Haifa, Israel).

-- Ziv Botzer — ziv.botzer@campus.technion.ac.il
-- Guy Austern — guyaustern@technion.ac.il
-- Yoav Sterman — sterman.yoav@technion.ac.il
