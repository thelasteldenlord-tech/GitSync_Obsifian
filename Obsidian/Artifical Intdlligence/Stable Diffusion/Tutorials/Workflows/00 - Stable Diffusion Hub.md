# Stable Diffusion Hub

Your comprehensive guide to AI image generation using Stable Diffusion and ComfyUI.

> [!info] Overview
> This hub organizes all resources for learning and using Stable Diffusion for AI image generation, including workflows, checkpoints, prompts, and technical documentation.

---

## Quick Start

**New to Stable Diffusion?**
1. Start with [[1.0 TLD - Stable Diffusion Flow Tree|Workflow Overview]]
2. Learn [[1.1 Generating Images from Text|Text-to-Image Basics]]
3. Understand [[1.1A Components and Definitions|Core Components]]
4. Explore [[ComfyUI Workflows|ComfyUI Workflow Templates]]

**Quick Reference:**
- [[Checkpoints|Model Checkpoints Guide]]
- [[Lora Triggers|LoRA Activation Keywords]]
- [[Safetensors|Safetensors Format Info]]
- [[Prompts|Prompt Library]]

---

## Learning Path

### 1. Foundations
- [[1.0 TLD - Stable Diffusion Flow Tree|Complete Workflow Tree]] - Overview of the generation process
- [[1.1 Generating Images from Text|Text to Image Generation]] - Core concept
- [[1.1A Components and Definitions|Components & Definitions]] - Technical terminology

### 2. ComfyUI Workflows
- [[ComfyUI Workflows|Workflow Template Library]]
- [[Txt2Img ZImage-Turbo with Pixel Art LoRa|Txt2Img with LoRa Example]]
- [[Vaulted/Private inVault ComfyUI|Private ComfyUI Workflows]]

### 3. Advanced Topics
- [[Local AI Solutions for Privacy|Privacy-Focused AI Setup]]
- Model training and fine-tuning
- Advanced prompt engineering

---

## Model Resources

### Checkpoints (Base Models)
- [[Checkpoints|Checkpoint Overview & Guide]]
- [[Checkpoint - Illustrij BTTR|Illustrij BTTR]]
- [[Illustrij BTTR|Illustrij BTTR Details]]
- [[Blue Diver-Illustrious-BTTR-1.0|Blue Diver Illustrious]]
- [[Real Dream Flux Dev-4|Real Dream Flux Dev-4]]

**From Clippings:**
- [[Hyphoria Illu & NAI - v0.01  Illustrious Checkpoint  Civitai|Hyphoria Illustrious NAI]]
- [[WAI-illustrious-SDXL-Checkpoint|WAI Illustrious SDXL]]

### LoRAs (Style Modifications)
- [[Lora Triggers|LoRA Trigger Keywords Reference]]
- Character LoRAs
- Style LoRAs
- Concept LoRAs

### Understanding File Formats
- [[Safetensors|Safetensors Format]] - Modern, safe model format

---

## Workflows by Use Case

### Text-to-Image (Txt2Img)
- [[Txt2Img ZImage-Turbo with Pixel Art LoRa|Basic Txt2Img with LoRa]]
- Standard character generation
- Environment/background generation

### Image-to-Image (Img2Img)
*Placeholder: Create workflows for image variations*

### Specialized Workflows
- [[Z Image Turbo Article|Z-Image Turbo Details]]
- Pixel art generation
- Anime/illustration style
- Photorealistic generation

---

## Prompt Engineering

### Prompt Library
- [[Prompts|Master Prompt Collection]]
- [[Results/Nier Automata - Yorha Prompt Results|NieR Automata Character Prompts]]
- Quality tags and modifiers
- Negative prompts best practices

### Prompt Structure
```
[Quality tags], [Style], [Subject], [Details], [Composition], [Lighting]
```

**Example Quality Tags:**
- `score_9, score_8_up, score_7_up`
- `masterpiece, best quality, highly detailed`
- `8k, ultra detailed, hyperrealistic`

---

## Results & Gallery

### Project Results
- [[Results/Nier Automata - Yorha Prompt Results|NieR Automata YoRHa Generations]]
- [[Results|Other Generation Results]]

### Reference Projects
- [[Elden Ring Prompt|Elden Ring Style Reference]]
- Character design explorations
- Environment studies

---

## Technical Setup

### Software & Tools
- **ComfyUI** - Node-based workflow interface [[ComfyUI Workflows|→ Workflows]]
- **Automatic1111** - Alternative web UI
- **Model Managers** - Organization and loading

### System Requirements
- GPU recommendations
- VRAM considerations
- Storage needs for models

### Privacy Considerations
- [[Local AI Solutions for Privacy|Local Setup for Privacy]]
- Offline generation capabilities
- Data security

---

## Organization System

### Folder Structure
```
Stable Diffusion/
├── 00 - Stable Diffusion Hub.md (This file)
├── Learning/ (Guides and tutorials)
├── My Checkpoints/ (Your model collection)
├── Prompts/ (Prompt library)
├── Results/ (Generated images and notes)
└── Vaulted/ (Archived or private content)
```

### [[Vaulted|Vaulted Content]]
- [[Vaulted/Private inVault ComfyUI|Private ComfyUI Workflows]]
- [[Vaulted/Z-Image-Turbo|Z-Image Turbo Archive]]
- Experimental workflows
- Personal projects

---

## Quick Reference Sheets

### Common LoRA Triggers
See [[Lora Triggers|Complete LoRA Trigger List]]

### Checkpoint Comparison
| Checkpoint | Best For | Style | VRAM |
|------------|----------|-------|------|
| [[Checkpoint - Illustrij BTTR\|Illustrij BTTR]] | Illustrations | Anime/Semi-real | ~6GB |
| [[Blue Diver-Illustrious-BTTR-1.0\|Blue Diver]] | Versatile | Mixed | ~6GB |
| [[Real Dream Flux Dev-4\|Real Dream Flux]] | Photo-real | Realistic | ~8GB |

### Essential Negative Prompts
```
lowres, bad anatomy, bad hands, text, error, missing fingers,
extra digit, fewer digits, cropped, worst quality, low quality,
normal quality, jpeg artifacts, signature, watermark, username, blurry
```

---

## Learning Resources

### External References
- Civitai - Model sharing community
- Stable Diffusion documentation
- ComfyUI documentation
- Community tutorials

### Practice Projects
- [ ] Generate a character in 3 different art styles
- [ ] Create a scene with consistent lighting
- [ ] Master LoRA mixing for unique styles
- [ ] Build a custom ComfyUI workflow
- [ ] Generate a character turnaround

---

## Related Content

- [[00 - Nier Automata Hub|NieR Automata Hub]] - For character references
- [[Elden Ring Prompt|Elden Ring Style Guide]]
- [[../Canvas Notes|Visual Canvas Notes]]

---

## Tags
`#stable-diffusion` `#ai-art` `#comfyui` `#text-to-image` `#checkpoints` `#lora` `#prompts` `#image-generation`

---

[[00 - Vault Index|← Back to Vault Index]]

---

*Last Updated: 2026-01-13*
*For offline use: This hub provides comprehensive SD guidance without internet access*
