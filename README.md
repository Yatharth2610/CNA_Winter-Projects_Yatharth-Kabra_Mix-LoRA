# CNA_Winter-Projects_Yatharth-Kabra_Mix-LoRA
MixLoRA: Multi-Skill Models via Low-Rank Adapter Mixing
📌 Project Overview

Large language models are expensive to fine-tune for every new task.
LoRA (Low-Rank Adaptation) enables efficient fine-tuning by learning small task-specific adapters while keeping the base model frozen.

This project implements MixLoRA — an extension of LoRA where multiple task-specific adapters are blended at inference time to create a multi-skilled model, demonstrating model reuse with minimal compute.

The system is designed to work under strict hardware constraints (16 GB RAM) while remaining fully runnable, modular, and extensible.

🎯 Original Problem Statement

Implement the “Mix LoRA” concept — blending multiple low-rank adaptation layers trained on different tasks to produce a multi-skilled model. Experiment with combinations like sentiment + summarization or art styles in diffusion models. It demonstrates powerful model reuse with minimal compute.

✅ What This Project Achieves

Trains multiple LoRA adapters on different tasks

Blends adapters dynamically to create a multi-skill model

Uses one frozen base model (no retraining)

Demonstrates efficient model reuse

Runs fully on 16 GB RAM without external APIs

Extends beyond the baseline with learned routing and sparse activation

🧠 High-Level Architecture
Frozen Base Model (TinyLlama 1.1B)
 ├── LoRA Adapter: Sentiment
 ├── LoRA Adapter: Summarization
 └── Gating Network (learned)
        ↓
   Sparse Adapter Selection (Top-1)

🛠️ Step-by-Step Solution
Step 1 — Lightweight Base Model

Used TinyLlama (1.1B) to ensure fast execution on limited hardware

Base model remains frozen throughout the project

Why:
Keeps compute cost low and enables adapter reuse.

Step 2 — Task-Specific LoRA Adapters

Two LoRA adapters are trained independently:

Sentiment Adapter → captures emotional polarity

Summarization Adapter → captures compression and abstraction behavior

Each adapter:

Trains only a small number of parameters

Is saved and reused independently

Why:
Encapsulates skills modularly without modifying the base model.

Step 3 — MixLoRA (Adapter Blending)

Both adapters are loaded into a single model instance.

At inference:

The effective model weights are:

W_final = W_base + α₁·ΔW_sentiment + α₂·ΔW_summary

Why:
This is the core MixLoRA idea — skill composition without retraining.

Step 4 — Learned Gating Network

A small MLP gating network is introduced to:

Read the prompt embedding

Predict which adapter should be used

The gating network outputs adapter weights automatically.

Why:
Removes manual routing logic and makes the system adaptive.

Step 5 — Sparse Routing (Top-1)

Instead of activating all adapters:

Only the most relevant adapter is activated per prompt

Why:

Faster inference

Reduced interference

Scales to many adapters (MoE-style behavior)

Step 6 — End-to-End Training

LoRA adapters are trained first

Gating network is trained separately using lightweight supervision

Base model is never updated

Why:
Ensures stability and avoids catastrophic forgetting.

✨ Features Summary
Feature	Description
LoRA adapters	Efficient task-specific fine-tuning
MixLoRA	Adapter blending for multi-skill behavior
Learned gating	Automatic adapter selection
Sparse routing	Activates only the most relevant adapter
Minimal compute	Runs on 16 GB RAM
Modular design	New skills can be added easily
🧪 Example Capabilities

Sentiment analysis

Text summarization

Automatic switching between tasks based on prompt intent

Example prompt:

"Summarize the emotional tone of this review..."


The model:

Detects summarization intent

Activates the appropriate adapter

Produces a coherent, task-appropriate output

⚙️ Hardware & Runtime Constraints

RAM: 16 GB

GPU: Optional (CPU-only supported)

No external APIs

No API keys required

This makes the project:

Easy to reproduce

Suitable for coursework, research demos, and interviews

🚀 Why This Matters

This project demonstrates that:

Large models do not need full retraining for every task

Skills can be learned once and reused forever

Adapter mixing enables modular, scalable AI systems

It reflects real-world trends in:

Parameter-efficient fine-tuning

Mixture-of-Experts style routing

Continual and modular learning

📌 Limitations & Extensions
Current Scope

Focused on LLM MixLoRA

Uses small synthetic datasets for demonstration

Possible Extensions

Diffusion LoRA style mixing (image generation)

Token-wise routing

Adapter contribution visualization

Larger task libraries

🧠 Key Takeaway

MixLoRA enables multi-skill intelligence by blending lightweight task adapters on top of a single frozen model, achieving powerful reuse with minimal compute.
