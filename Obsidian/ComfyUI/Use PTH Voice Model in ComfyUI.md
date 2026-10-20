#Voice-Cloning #ComfyUI #setup_guides #tutorial 

#todo  #publish
# Use PTH Voice Model in ComfyUI

To use a `.pth` voice model in ComfyUI,
you need to integrate it via a compatible custom node. 
I recommend using either **TTS-Audio-Suite** 
or if that one causes conflits you can try **ComfyUI-VoiceCraft**.
Just follow the steps below, assuming you already 
have installed [ComfyUI](https://127.0.0.1:8188). If not you can visit my guide
[[How to run ComffyUI on Intel Arc GPU(Desktop Version)]] or
[[How to run ComfyUI on Intel Core Ultra Laptops]]
[[How to run ComfyUI on AMD chips (EASY))]]

Here’s how to get it going , including a link to a website hosting TONs of pretrained celeb voices in pth format!

### **1. Install Required Custom Nodes**
- **TTS-Audio-Suite**: This is the primary node suite for voice cloning and conversion in ComfyUI.
  - Install it via the **Custom Nodes Manager** in ComfyUI (go to `Manager` > `Custom Nodes Manager` > search for `TTS Audio Suite`).
  - This node includes the **`Load RVC Character Model`** node, which is used to load `.pth` RVC voice models.

### **2. Place Your `.pth` Model File**
- Copy your RVC `.pth` model file (e.g., `claire.pth`) into:
  ```
  ComfyUI/models/RVC/
  ```
- If your model includes a **FAISS index file** (`.index`), place it in:
  ```
  ComfyUI/models/RVC/.index/
  ```

### **3. Load the Model in ComfyUI**
- In your ComfyUI workflow:
  - Add the **`Load RVC Character Model`** node.
  - Set the **`model`** parameter to your `.pth` file (e.g., `claire.pth`).
  - Optionally, specify the **`index_file`** if you have a `.index` file.
  - Enable **`auto_download`** (default: True) to automatically fetch the model if missing.

### **4. Connect to Voice Changer**
- The loaded model (`rvc_model` output) must be connected to the **`Voice Changer`** node as the `narrator_target` input.
- This enables real-time voice conversion using your custom voice.

> ✅ **Tip**: Ensure **espeak-ng** is installed on your system (required for text-to-speech preprocessing).  
> 📌 **Note**: For **VoiceCraft** models (`.pth` files from Hugging Face), use the **`voicecraft_model_loader`** node instead, which supports models like `giga830M.pth`.

### **Troubleshooting**
- **Model not found?** Verify file paths and restart ComfyUI. Use **symbolic links** if models are stored elsewhere.
- **Auto-download fails?** Check internet connection and permissions.
- **No model listed?** Reload the ComfyUI browser page after placing files.

For advanced workflows, explore **FLOAT** for audio-driven talking portraits or **ComfyUI-VoiceCraft** for text-to-speech synthesis with voice control.