---
title: Hyphoria [Illu & NAI] - v0.01 | Illustrious Checkpoint | Civitai
source: https://civitai.com/models/1595884/hyphoria-illu-and-nai?modelVersionId=1805971
author:
  - "[[ecaj]]"
published: 2025-05-18
created: 2025-12-26
description: An experimental merge of various models I like, using an algorithm that takes the strengths of each. Thanks to @epiTune for the advice and guidance...
tags:
  - "#comfyui"
  - "#Models"
  - "#BaseModel"
---

## Hyphoria Illu & NAI

| Type | CheckpointMerge |
| --- | --- |
| Stats | 14,951  3.7m  2.6m |
| Generation | Buzzing! |
| Reviews | [Overwhelmingly Positive](https://civitai.com/models/1595884/reviews?modelVersionId=1805971)  (5,009) |
| Published | May 18, 2025 |
| Base Model | Illustrious |
| Usage Tips |  |
| Hash | AutoV2  416DAECFBE |
| AIR | `civitai:``1595884` `@` `1805971` |

Full Model fp16 (6.46 GB)

[Download](https://civitai.com/api/download/models/1805971?type=Model&format=SafeTensor&size=full&fp=fp16)

Verified:7 months ago

SafeTensor

License:

[Illustrious License](https://freedevproject.org/faipl-1.0-sd/)

[![7V28XKRR38FJGPCN6JS210MKX0-LOOP-Videoboltnet.webp](https://image.civitai.com/xG1nkqKTMzGDvpLrqFT7WA/955147b8-8cd1-48b2-b28e-8da508acfab6/anim=false,width=450,optimized=true/7V28XKRR38FJGPCN6JS210MKX0-LOOP-Videoboltnet.jpeg)](https://civitai.com/images/77879909)

[![2025-05-11-205747_00000.png](https://image.civitai.com/xG1nkqKTMzGDvpLrqFT7WA/b42c05ee-d5c9-4632-94f4-686231f068c2/anim=false,width=450,optimized=true/2025-05-11-205747_00000.jpeg)](https://civitai.com/images/77143964)

[![2025-05-18-170736_merged_illustrious_811517180938008.png](https://image.civitai.com/xG1nkqKTMzGDvpLrqFT7WA/0e701265-65cb-48e3-b6a3-b3e01d6c3adf/anim=false,width=450,optimized=true/2025-05-18-170736_merged_illustrious_811517180938008.jpeg)](https://civitai.com/images/77142108)

An experimental merge of various models I like, using an algorithm that takes the strengths of each. Thanks to [@epiTune](https://civitai.com/user/epiTune) for the advice and guidance, I still have a lot to learn and much to do.

The focus of Hyphoria was first and foremost prompt adherence. That is, what you put in the prompt box, the model will do its damndest to make it happen. I built this on top of many great models, which enabled Hyphoria to bridge that prompt understanding with great visuals and the ability to fill in gaps to make beautiful images.

I also wanted style flexibility, of course you can use LORAs as you would expect, but there are so many great artists and art styles hidden in the depths of these models, it is amazing what can be done. I recommend you explore a bit; I know I am!

Lastly, I like semi-realism, so I ensured this model was capable of doing that comfortably without too much trouble, as such it has a bias for that by default. That doesn't mean it can't do pure anime or 2D styles, quite the contrary, just tag what you want to see, and you will get it (though note, that excessive quality tags will impede some style choices).

- **Steps:** 20-35 (I have always liked 35, but lower is just as good)
- **CFG:** 2.5-6
	- I use 3, it is my sweet spot, but with a robust enough prompt you can go as low as 1, especially if you want a dim and grungy look.
- **Sampler:** DPM++ 2M SDE (or DPM++ 2M on CIVITAI Gen)
- **Scheduler:** Karras
- **Resolution:** I recommend 1024x1024 - 1280x1280 for normal generation. Supports up to 1536x1536 without breaking, but can suffer some body extension. Any aspect ratio that equals the same number of pixels should work.
- **Prompting**: This model listens to your prompts, like really listens, so avoid the fluff and keep your prompts focused.
	- **Recommended Positive**: `masterpiece, best quality, absurdres`
	- **Recommended Negative**: `worst quality, low quality`
	- You can often omit pos or neg quality tags depending on what you're trying to make, grungy images for instance will want to pull out some of those quality tags. Some of the other quality tags do work if you want those types of images.

### Models Used

- IllustriousXL V2.0 Stable **\- Used as base merge target**
- Rouwei v0.7 eps
- IllumiYume v3.1
- Hassaku v1.3 Style A
- ionsyx v3.0
- Wicked Illustrious Mix v1.1
- mdntIllus Syn v1
- Kokio v2.0
- Diving Illustrious Anime v11
- Bismuth Illustrious Mix v2.0
- NoobAI v1.1 eps
- Unreleased Merge
- Plant Milk Hemp II
- Plant Milk Coconut

Using an algorithm, each model's UNET and CLIP were compared and the best was chosen tensor by tensor, using weights I set as **my** subjective adjustment to influence how likely they would be chosen. I can't tell you exactly what part of what model is used where, my merge script just chose what it considered the best.

For future versions I will be experimenting with different models, along with more granular adjustments (at the block level, or even more granular than that).

SDXL - [CreativeML Open RAIL++-M](https://github.com/Stability-AI/generative-models/blob/main/model_licenses/LICENSE-SDXL1.0)  
Illustrious - [https://freedevproject.org/faipl-1.0-sd/  
](https://freedevproject.org/faipl-1.0-sd/%EF%BF%BCNoobAI-XL)NoobAI-XL - [https://civitai.com/models/license/1140829](https://civitai.com/models/license/1140829)

Copied the above license list from [Plant Milk's](https://civitai.com/models/1162518/plant-milk-model-suite) page.

## Discussion

This is one of the only Illustrious models where I can extract a Lora when I finetune it. Almost all other Illus models get stuck at step 65. Any idea what is different? The other models only work if I don't do the text encoder but then they also don't work as well.

10/10 💛