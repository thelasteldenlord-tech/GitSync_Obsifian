 #image-generation  #general #tutorial

## Detailer and Prompt Travel

Since you have the 'Classic Manager' up and running, you’re in a great spot. To build a robust 1.5x [#detailer](https://keep.google.com#label/detailer)  and prompt-travel workflow for 2B, we’ll use a mix of native logic and a few "power-user" nodes.


### 1. The "Prompt Travel" / Dynamic Node

For the ``{variable|variable}`` syntax to actually iterate (rather than just picking one at random), you need the ``ComfyUI-DynamicPrompts`` node or ``FizzNodes``.

 * Node to find: Dynamic Prompts (from the ``comfyui-dynamicprompts`` repo).

 * The Logic: Instead of a standard CLIP Text Encode, use the Dynamic Prompt node.

 * How to "Travel": If you set your Batch Count in the Latent node to 4, the Dynamic Prompt node will automatically cycle through your bracketed options for each image in that batch.

2. The 1.5x Latent Upscale & Detailer Flow

This is the "standard resolution to high-res" pipeline you asked for.

Step A: Base Generation

 * Empty Latent Image: Use an SDXL-friendly resolution like 1024x1024 (Square) or 1216x832 (Landscape).

 * KSampler (Base): Standard settings.

   * Checkpoint: Illustrious.

   * Prompt: Use the Dynamic Prompt node mentioned above.

Step B: The 1.5x "Locked Proportion" Upscale

To avoid manual math, we use a ratio-based node.

 * Node to find: Latent Scale by Ratio (Found in Derfuu_ComfyUI_ModdedNodes or KikoTools).

 * Settings:

   * samples: Connect the LATENT output from your first KSampler.

   * modifier / ratio: Set to 1.5.

   * upscale_method: Use bislerp or bicubic (these handle "Anime Realistic" textures better than nearest-exact).

Step C: The Detailer Pass (High-Res Fix)

 * KSampler (Detailer): Connect the upscaled latent here.

 * Crucial Settings:

   * Denoise: Set to 0.4 or 0.5. This is the "magic number"—it’s high enough to add lace detail to 2B's dress but low enough to keep her face from morphing into someone else.

   * Prompt: Use the same prompt as the base, but you can add ultra high definition, sharp focus to the end.

 * VAE Decode & Save: Finally, decode the latent from this sampler to get your finished 1.5x image.

3. Strong 2B "Anime-Realistic" Prompt Example

Since you're using Illustrious, try this for the bracketed subject:

> Positive: masterpiece, best quality, {semi-realistic anime | digital painting | sharp illustrative style}, 1girl, solo, 2B (Nier Automata), silver hair, black blindfold, beauty mark, black gothic dress, {standing in a field of white flowers | sitting on a rusted mechanical arm | overlooking a flooded city ruins}, {dramatic sunset lighting | soft cinematic moonlight}, intricate lace, mechanical detail, wind-blown hair, highly detailed background, scenery, (no humans:1.2).

> Negative: (human, people, man, crowd:1.4), (worst quality, low quality:1.4), blurry, logo, watermark, signature, extra limbs, bad anatomy.

> 

Pro-Tip for Landscapes

Since you struggled with humans appearing in landscapes, try adding the "Empty City" or "Nature" concept before the subject in your prompt. Illustrious prioritizes the first few tokens heavily. If "scenery" and "landscape" come first, the model "frames" the shot for a wide view before it even thinks about 2B.

Would you like me to find the specific GitHub URLs for those "Scale by Ratio" nodes so you can install them via the "Install via Git URL" feature in your Manager?