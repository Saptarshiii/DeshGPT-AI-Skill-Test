# 🇮🇳 Hindi–English Conversational AI (LoRA Fine-tuning)

##  Overview
This project demonstrates building a **small-scale conversational AI model** fine-tuned for **Hindi + English (Hinglish)** using an **open-source LLM** from Hugging Face.  

The goal:
- **Intent Detection** → Understand the user’s request  
- **Context Retention** → Maintain conversation flow  
- **Hinglish Fluency** → Handle mixed Hindi–English language naturally  

We chose **BigScience BLOOMZ-7B1** as the base model and used **LoRA + 4-bit quantization** for memory-efficient fine-tuning on limited hardware.

---


##  Technical Approach

### **Model Choice**
- **Model ID:** `bigscience/bloomz-7b1`
- **Reason:** Supports Hindi and multilingual conversational tasks, well-suited for Hinglish.

### **Fine-tuning Method**
- **LoRA (Low-Rank Adaptation)** for parameter-efficient training
- **4-bit quantization** (`bitsandbytes`) to reduce GPU memory usage
- **AdamW** optimizer for weight updates
- **Causal LM** loss with labels = shifted input tokens

### **Dataset**
A small synthetic **Hinglish multi-turn dialogue dataset** covering:
- Weather updates
- Ticket bookings
- Jokes & riddles
- Reminders
- Banking queries
- News updates
- Context switching

**Example:**

User: Hi, kaise ho aap?
Assistant: Main theek hoon! Aap kaise hain?
Training Config
Parameter	Value
Epochs	1
Batch Size	4
Learning Rate	2e-4
Max Length	512 tokens
LoRA Rank (r)	8
LoRA Alpha	32
Target Modules	q_proj, v_proj
Dropout	0.05

Project Structure

```bash

├── fine_tune.py         # Main training script (Colab)
├── dataset_creation.py  # Dataset creation logic
├── README.md            # Project documentation
└── screenshots/         # Colab session screenshots & GPU error logs
```
## Steps to Run

Install dependencies

(All the secret are tokens are submitted with and the repo is currently please let me know after completion of evalution so that i can remove this repo)

pip install --upgrade pip
pip install transformers accelerate bitsandbytes datasets peft safetensors sentencepiece scikit-learn
Mount Google Drive (if using Colab)


from google.colab import drive
drive.mount('/content/drive')
Set HF Token and paths

OUTPUT_DIR = '/content/drive/MyDrive/hindi-ai-lora'
Run the training script

python fine_tune.py
 Challenges Faced
Unfortunately, Google Colab Free Tier GPU (T4, 15GB) ran out of memory while loading the 7B model weights even with 4-bit quantization.
The training process could not be completed — the code is fully prepared, but execution was interrupted during model loading.

## Error Cause:

BLOOMZ-7B1 requires > 20GB VRAM for standard loading.

Even with LoRA + quantization, the initial weight loading exceeded Colab free GPU limits.

## Planned Fixes:

Switch to a smaller base model (e.g., bloomz-560m or mistral-7b-instruct with offloading).

Use accelerate CPU/GPU offload to reduce VRAM pressure.

Try Kaggle GPU P100 or RunPod / Lambda Labs for higher memory.

Evaluate model on:

Intent detection: Verify it understands diverse tasks.

Context retention: Multi-turn conversations.

Export LoRA adapters for easy integration into chat applications.
