---
title: "Planning a Multi-Tiered AI Dev Stack with Commodity Hardware"
layout: post
date: 2025-04-18
tags: [ai, transformers, devtools, fine-tuning, ssh, local-llm]
summary: A structured plan for building a hybrid AI development stack across Mac, Windows (WSL), and GPU-backed compute environments.
fluid: true
---

I'm building a development and experimentation environment that spans:

- **MacBook (M2)**: My primary creative machine for writing, editing, and publishing
- **Windows Gaming Laptop (4070 GPU)**: A compute node for fine-tuning small transformer models, running quantized local inference, and developing a deeper understanding of transformer internals
- **WSL2 on Windows**: A reproducible Linux dev environment for Git, SSH, scripting, and headless CLI workflows, giving me parity with typical CI/production setups

## Objectives

1. Maintain complete control over the environment (no mandatory cloud dependencies)
2. Build or adapt small, performant models that understand my workflows, language, and code
3. Use the hosted large models only where needed: transcription, tagging, and one-time heavy processing
4. Create tooling and documentation that allow the same setup to be rebuilt across machines

## Workflow Overview

- Authoring happens on the MacBook using VS Code and Git
- Changes sync via Git remotes to the dev repo, with SSH authentication on all machines
- WSL2 serves as a cross-platform testbed and early staging environment
- The Windows laptop runs GPU-accelerated local inference (e.g. `llama.cpp`, QLoRA-based models)
- Where needed, hosted models (e.g. GPT-4, Whisper) are used to enrich data for downstream use

## Model Experimentation Strategy

I plan to move beyond RAG (Retrieval Augmented Generation) into lightweight fine-tuning or parameter-efficient finetuning (PEFT) for small-scale transformer models.

| Task                              | Technique                     |
|-----------------------------------|-------------------------------|
| Add personal voice and tone       | LoRA / QLoRA / Adapters       |
| Rewriting blog content with flavor| Instruction tuning on tagged examples |
| Embedding prior work contextually | RAG layer or vector database  |

Target models include:
- TinyLlama (1.1B)
- Phi-2 (2.7B, Microsoft)
- CodeLlama (quantized)
- Any GGUF/ggml-compatible format for efficient CPU/GPU use

## Audio Metadata for Tone

I'm keeping voice recordings not for transcription, but for their expressive cues. Even if I don't process the audio directly, I may use them to derive or annotate tone markers (e.g. `<snark>`, `<dry>`, `<sincere>`), which can then:

- Be added to training data for small models
- Serve as prompts or soft tokens during generation
- Enable rewriting or summarizing that preserves affect

Initial tone tagging may be manual or driven by hosted models, with downstream fine-tuning applied to smaller models once a base corpus exists.

## Summary

This is a hybrid-local pipeline with the goal of:

- Understanding the limits of small, locally-run LLMs
- Building tools that serve *my* workflow and voice
- Minimizing cloud dependence while making smart use of hosted inference for bootstrapping

Commodity hardware is the constraint and the proving ground. Once the system breaks those limits, then—and only then—I'll consider scaling to more powerful builds.