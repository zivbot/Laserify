# Laserify: Supplementary Materials

Supplementary materials for CHI 2026 submission:  
**"Laserify: From Multimodal Input to Fabrication-Ready Laser Cut Plans"**

## Models Used

- **Stage 1 — Reference image generation:** OpenAI Sora (image generation)
- **Stage 2a — Scene and part discovery:** gemini-3-pro-preview (gpt-4o, gpt-5.1, claude sonnet 4.5 were also tested, with inferior results)
- **Stage 2b — Geometric scaffolding:** gemini-3-pro-preview
- **Stage 2c — Outline extraction:** gpt-5.1-2025-11-13 (gemini was also tested, producing more hallucinations and lack of adherence with instructions)
- **Baseline — Direct outline extraction:** gpt-5.1-2025-11-13
- **Baseline — Image-to-OpenSCAD:** gemini-3-pro-preview

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
