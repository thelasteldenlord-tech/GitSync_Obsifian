# Stable Diffusion Quick Reference Card

Fast reference for image generation settings and best practices.

---

## Common Settings

### Resolution Recommendations

**SD 1.5:**
- Portrait: 512x768
- Landscape: 768x512
- Square: 512x512

**SDXL:**
- Portrait: 832x1216 or 896x1152
- Landscape: 1216x832 or 1152x896
- Square: 1024x1024

**Flux:**
- More flexible, 1024x1024 or higher

---

## Sampling Methods

### Best General Purpose
- **DPM++ 2M Karras** - Fast, good quality
- **DPM++ SDE Karras** - High quality, slower
- **Euler a** - Fast, creative
- **UniPC** - Very fast, decent quality

### For Specific Needs
- **LMS** - Older, stable
- **Heun** - High quality, slow
- **DDIM** - Deterministic (same seed = identical output)

---

## CFG Scale (Guidance)

| CFG | Effect | Best For |
|-----|--------|----------|
| 1-5 | Very loose interpretation | Abstract, experimental |
| 6-8 | Balanced (recommended) | Most general use |
| 9-12 | Strict prompt following | Detailed scenes, specific compositions |
| 13+ | Over-saturated, burnt | Usually avoid |

**Sweet Spot:** 7-8 for most purposes

---

## Steps

| Steps | Quality | Speed | Notes |
|-------|---------|-------|-------|
| 10-20 | Draft | Fast | Quick tests |
| 20-30 | Good | Medium | Standard quality |
| 30-50 | High | Slow | Diminishing returns after 30 |
| 50+ | Minimal improvement | Very slow | Usually wasteful |

**Sweet Spot:** 25-30 steps

---

## Prompt Structure

### Optimal Format
```
[Quality tags], [Style], [Subject], [Details], [Composition], [Lighting], [Atmosphere]
```

### Example
```
masterpiece, best quality, highly detailed,
digital painting, cyberpunk style,
female character, silver hair, neon blue eyes, leather jacket,
close-up portrait, rule of thirds,
dramatic lighting, rim light,
moody atmosphere, rain
```

---

## Essential Positive Prompt Tags

### Quality Boosters
```
masterpiece, best quality, highly detailed, 8k, ultra detailed,
sharp focus, professional, award winning
```

### For Anime/Illustration
```
score_9, score_8_up, score_7_up, source_anime,
detailed face, detailed eyes, beautiful lighting
```

### For Photorealistic
```
photorealistic, photo-realistic, RAW photo, 8k uhd,
dslr, soft lighting, high quality, film grain
```

---

## Essential Negative Prompts

### Universal Base
```
lowres, bad anatomy, bad hands, text, error, missing fingers,
extra digit, fewer digits, cropped, worst quality, low quality,
normal quality, jpeg artifacts, signature, watermark, username, blurry
```

### For Characters
```
bad anatomy, bad hands, bad face, bad eyes, bad proportions,
extra limbs, extra fingers, missing limbs, fused fingers,
too many fingers, mutated hands, poorly drawn hands, poorly drawn face
```

### For Photorealistic
```
cartoon, anime, painting, illustration, 3d render, cgi,
unrealistic, low resolution, blurry
```

---

## LoRA Usage

### Loading LoRAs
```
<lora:name_of_lora:strength>
```

**Strength Values:**
- 0.3-0.5 = Subtle influence
- 0.6-0.8 = Balanced (recommended)
- 0.9-1.0 = Strong influence
- 1.0+ = Very strong (can break images)

### Mixing Multiple LoRAs
```
masterpiece, best quality,
<lora:style_lora:0.7> <lora:character_lora:0.8> <lora:concept_lora:0.5>,
your prompt here
```

**Tip:** Keep total LoRA strength under 2.5-3.0

---

## Checkpoint Quick Comparison

| Checkpoint Type | Best For | Style | Prompt Sensitivity |
|----------------|----------|-------|-------------------|
| [[Checkpoints\|Illustrious-based]] | Anime/illustrations | Anime | High |
| [[Checkpoints\|Realistic SDXL]] | Photos, realism | Photorealistic | Medium |
| [[Checkpoints\|Artistic SDXL]] | Art, paintings | Varied | Medium-High |
| [[Checkpoints\|SD 1.5]] | General, fast | Varied | Low-Medium |

See: [[00 - Stable Diffusion Hub#Model Resources|Model Resources]]

---

## Troubleshooting

### Problem: Blurry Images
- **Solution:** Increase steps to 25-30, check resolution, add "sharp focus" to prompt

### Problem: Wrong Colors
- **Solution:** Lower CFG scale, be more specific with color terms in prompt

### Problem: Bad Anatomy
- **Solution:** Add anatomy terms to negative, lower LoRA strength, try different checkpoint

### Problem: Not Following Prompt
- **Solution:** Increase CFG scale, rephrase prompt, emphasize key terms with (parentheses)

### Problem: Over-saturated/Burnt
- **Solution:** Lower CFG scale to 6-8, reduce step count

### Problem: Artifacts/Noise
- **Solution:** Change sampler, adjust steps, check for conflicting LoRAs

---

## Emphasis Syntax

### Increase Attention
- `(keyword)` = 1.1x attention
- `((keyword))` = 1.21x attention
- `(keyword:1.5)` = 1.5x attention

### Decrease Attention
- `[keyword]` = 0.9x attention
- `(keyword:0.5)` = 0.5x attention

### Example
```
(masterpiece:1.4), (beautiful lighting:1.3), woman, red dress, [background:0.8]
```

---

## CLIP Skip

**What it does:** Skips final layers of CLIP text encoder

| CLIP Skip | Effect | Best For |
|-----------|--------|----------|
| 1 | Standard | Photorealistic, SDXL |
| 2 | More artistic | Anime, illustrations, SD 1.5 |
| 3+ | Very loose | Experimental |

**Most anime checkpoints:** Use CLIP skip 2

---

## Batch Processing Tips

### Testing Prompts
- Use batch size 4-8 with same seed
- Vary one parameter at a time
- Keep notes on what works

### Production
- Lock in settings from tests
- Use different seeds for variety
- Organize output folders

---

## Workflow Checklist

- [ ] Choose appropriate checkpoint for style
- [ ] Set correct resolution for model type
- [ ] Write structured prompt (positive + negative)
- [ ] Load LoRAs if needed (total weight < 3.0)
- [ ] Set CFG scale (7-8 typical)
- [ ] Set steps (25-30 typical)
- [ ] Choose sampler (DPM++ 2M Karras)
- [ ] Set CLIP skip if needed
- [ ] Generate test batch
- [ ] Refine and iterate

---

## Quick Links

- [[00 - Stable Diffusion Hub|Stable Diffusion Hub]]
- [[1.0 TLD - Stable Diffusion Flow Tree|Workflow Tree]]
- [[ComfyUI Workflows|ComfyUI Workflows]]
- [[Checkpoints|Checkpoint Library]]
- [[Lora Triggers|LoRA Reference]]
- [[Prompts|Prompt Library]]

---

## Tags
`#quick-reference` `#stable-diffusion` `#settings` `#offline-study` `#cheat-sheet`

---

*Keep this handy for quick lookups during generation sessions*
