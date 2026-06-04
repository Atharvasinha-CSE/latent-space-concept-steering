# Latent-Space Concept Steering on Gemma-2B

This repository contains a mechanistic interpretability proof-of-concept that dynamically steers the outputs of an open-source LLM (Gemma-2B) at inference time, without requiring fine-tuning or retraining.

## 🎯 Project Objective
The goal of this project was to enforce strict symbolic constraints on a language model by manipulating its internal representations (hidden states). Specifically, I hunted down the mathematical representation of "Deception" and successfully erased it (and mathematically forced it) during live text generation.

## 🛠️ Tools & Methodology
* **Model:** Google's `gemma-2b-it`
* **Mechanistic Interpretability:** `sae-lens` (Sparse Autoencoders / Gemma Scope)
* **Framework:** PyTorch
* **Compute:** Google Colab (NVIDIA T4 GPU)

## 🔬 How it Works
1. **Concept Extraction:** Used Contrastive Activation Extraction—passing both "honest" and "deceptive" prompts through a Sparse Autoencoder (SAE) on Layer 12 to isolate the exact feature vector representing deception.
2. **Dynamic Steering:** Implemented a PyTorch forward hook (`stealth_hook`) using in-place modification (`.add_()`) to safely mathematically alter the model's hidden states mid-sentence, bypassing short-term memory positional crashes.
3. **Mathematical Formalism:** Applied the latent-space steering equation to inject the vector dynamically.

## 🚀 Usage
To run this project, you will need:
1. A Hugging Face account and an Access Token (`HF_TOKEN`).
2. A GPU (A free Google Colab T4 is sufficient).
3. Open the `.ipynb` notebook in Colab, securely add your `HF_TOKEN` to the Colab Secrets tab, and run all cells.
