# AI Models Guide: Open, Licensed, Closed, Local and Specialized Models

> A practical list of useful AI models, with an emphasis on models that developers can actually build with, download, self-host, or access through an API.
>
> **Updated:** September 2026
>
> This is not a list of every AI model on the internet. There are thousands of foundation models and an even larger number of fine-tunes, quantizations and adapters. The goal here is to keep a practical shortlist of important and sometimes overlooked models.

---

## Table of Contents

- [How to Read This Guide](#how-to-read-this-guide)
- [Open Source vs Open Weight vs Closed](#open-source-vs-open-weight-vs-closed)
- [AI Models by Category](#ai-models-by-category)
- [General AI / LLMs](#general-ai--llms)
- [Coding Models](#coding-models)
- [Multimodal Models](#multimodal-models)
- [Reasoning Models](#reasoning-models)
- [Image Generation](#image-generation)
- [Image Matting and Background Removal](#image-matting-and-background-removal)
- [Audio and Speech](#audio-and-speech)
- [Retrieval, Embeddings and RAG](#retrieval-embeddings-and-rag)
- [Lightweight and Edge AI](#lightweight-and-edge-ai)
- [Document AI and OCR](#document-ai-and-ocr)
- [Computer Vision](#computer-vision)
- [Video Generation](#video-generation)
- [Translation and Language](#translation-and-language)
- [Agents and Computer Use](#agents-and-computer-use)
- [Commercial / Closed Models](#commercial--closed-models)
- [Hardware Recommendations](#hardware-recommendations)
- [How to Choose a Model](#how-to-choose-a-model)
- [Important Notes About VRAM](#important-notes-about-vram)

---

# How to Read This Guide

There are four things worth checking before choosing a model:

1. **What job does it actually do?**
2. **Can I download the weights, or do I need an API?**
3. **What does the license allow?**
4. **Can my hardware run it comfortably?**

A model with 70B parameters is not automatically better for every task. A 1B OCR model can be a much better choice for OCR than a 70B general-purpose language model.

---

# Open Source vs Open Weight vs Closed

The AI industry uses "open source" rather loosely. In this document, the following terminology is used.

| Type | Meaning | Typical examples |
|---|---|---|
| **Open / permissive** | Weights are available and the license is relatively permissive | Qwen, Mistral open models, DeepSeek-R1, Phi, Whisper |
| **Open-weight / custom license** | Weights are downloadable, but the license has additional conditions | Llama, Gemma |
| **Open model + API** | You can download the model and/or use a hosted API | Qwen, Mistral, Gemma, many Hugging Face models |
| **Closed + API** | Weights are not publicly downloadable; access is through a hosted product/API | GPT, Claude, Gemini, Grok |
| **Specialized open model** | Built mainly for one job rather than general chat | OCR, embeddings, speech, segmentation, reranking |

**Always read the exact license for the model version you plan to ship.** A company can release some models under an open/permissive license and other models under a different license.

---

# AI Models by Category

## 1. General AI / LLMs

General-purpose language models are useful for:

- chat
- summarization
- writing
- question answering
- planning
- tool calling
- structured output
- general reasoning

### Recommended models

| Model | Params | Context | Type | API | License / access | Best for |
|---|---:|---:|---|---|---|---|
| [Qwen3](https://huggingface.co/Qwen) | 0.6B–235B+ variants | Model dependent | Open | Yes | Apache 2.0 for many releases | General AI, multilingual, reasoning |
| [DeepSeek](https://huggingface.co/deepseek-ai) | Multiple sizes | Model dependent | Open | Yes | Model dependent | Reasoning, coding |
| [Mistral Small](https://huggingface.co/mistralai) | Multiple | Model dependent | Open | Yes | Apache 2.0 for open releases | General AI, local/enterprise |
| [Llama](https://huggingface.co/meta-llama) | Multiple | Model dependent | Open-weight | Yes | Llama license | General AI, local AI |
| [Gemma](https://ai.google.dev/gemma) | 270M–27B+ | Up to 128K on relevant Gemma 3 sizes | Open-weight | Yes | Gemma Terms | Local AI, multimodal, edge |
| [Phi](https://huggingface.co/microsoft) | Small models | Model dependent | Open | Yes | Model-specific | Small/local AI |
| [Granite](https://huggingface.co/ibm-granite) | Multiple | Model dependent | Open | Yes | Model-specific | Enterprise, RAG |
| [GLM](https://huggingface.co/THUDM) | Multiple | Model dependent | Open / mixed | Yes | Model-specific | General AI, reasoning |
| [MiniCPM](https://huggingface.co/openbmb) | Small-to-medium | Model dependent | Open | Yes | Model-specific | Local multimodal AI |

### Good starting points

- **Small/local:** Gemma, Phi, Qwen small variants
- **General local:** Qwen, Mistral, Llama
- **Reasoning:** DeepSeek reasoning models, Qwen reasoning models
- **Enterprise:** Granite, Mistral

---

# Coding Models

Coding models are trained or tuned to understand source code, repositories, tool calls and software-engineering tasks.

| Model | Approx. size | Context | API | License / access | Best for |
|---|---:|---:|---|---|---|
| [Qwen Coder](https://huggingface.co/Qwen) | Multiple | Model dependent | Yes | Model-specific | General coding |
| [Devstral](https://huggingface.co/mistralai) | Small to large variants | Up to 256K on relevant releases | Yes | Model-specific | Coding agents, repositories |
| [Codestral](https://huggingface.co/mistralai) | ~22B class | Large context | Yes | Model-specific | Code completion |
| [DeepSeek Coder](https://huggingface.co/deepseek-ai) | Multiple | Model dependent | Yes | Model-specific | Coding and code reasoning |
| [StarCoder2](https://huggingface.co/bigcode) | 3B–15B | 16K | Hosted options | OpenRAIL-style license | Code generation |
| [Granite Code](https://huggingface.co/ibm-granite) | Multiple | Model dependent | Yes | Model-specific | Enterprise coding |
| [Seed-Coder](https://huggingface.co/ByteDance-Seed) | Small/medium variants | Model dependent | Hosted/community options | Model-specific | Efficient coding |

### Coding model selection

Use a specialized coding model when the job is:

```text
Repository
    ↓
Understand code
    ↓
Find relevant files
    ↓
Edit code
    ↓
Run tests
    ↓
Fix errors
```

For simple autocomplete, a smaller coding model is often enough. For repository-level agents, use a model designed for tool use and software engineering.

---

# Multimodal Models

Multimodal models accept more than text.

Typical inputs:

- text
- images
- audio
- video
- documents

| Model | Text | Image | Audio | Video | Local |
|---|---|---|---|---|---|
| [Gemma 3](https://ai.google.dev/gemma/docs/core/model_card_3) | Yes | Yes | No | No | Yes |
| [Gemma 3n](https://ai.google.dev/gemma/docs/gemma-3n/model_card) | Yes | Yes | Yes | Yes | Yes |
| [Qwen-VL](https://huggingface.co/Qwen) | Yes | Yes | Some variants | Some variants | Yes |
| [InternVL](https://huggingface.co/OpenGVLab) | Yes | Yes | Model dependent | Model dependent | Yes |
| [MiniCPM-V](https://huggingface.co/openbmb) | Yes | Yes | Model dependent | Model dependent | Yes |
| [Pixtral](https://huggingface.co/mistralai) | Yes | Yes | No | No | Some variants |
| [LLaVA](https://huggingface.co/llava-hf) | Yes | Yes | No | No | Yes |

Multimodal is particularly useful for:

- screenshot understanding
- PDF/document analysis
- image Q&A
- UI understanding
- visual assistants
- image-based search

---

# Reasoning Models

Reasoning models are designed for multi-step problems rather than simply generating the most likely response.

Useful for:

- mathematics
- coding
- planning
- scientific problems
- complex analysis
- agent planning

| Model | Type | Local | API | Best for |
|---|---|---|---|---|
| [DeepSeek-R1](https://huggingface.co/deepseek-ai/DeepSeek-R1) | Open | Yes | Yes | Reasoning, math, coding |
| [Qwen reasoning models](https://huggingface.co/Qwen) | Open | Yes | Yes | Reasoning, coding |
| [DeepSeek-V3 family](https://huggingface.co/deepseek-ai) | Open | Yes | Yes | General + reasoning |
| [Magistral](https://huggingface.co/mistralai) | Open/hosted variants | Yes for open releases | Yes | Reasoning |
| [Gemini reasoning models](https://ai.google.dev/gemini-api/docs/models) | Closed | No | Yes | General reasoning |
| [GPT reasoning models](https://platform.openai.com/docs/models) | Closed | No | Yes | Reasoning, agents |
| [Claude reasoning models](https://www.anthropic.com/claude) | Closed | No | Yes | Reasoning, coding |

A reasoning model is not a special "decision-making machine". It is still a language model. It can help analyze alternatives, but important real-world decisions should use reliable data, explicit rules and human review.

---

# Image Generation

Image models are separate from text LLMs.

| Model | Type | Local | API | License / access | Best for |
|---|---|---|---|---|---|
| [FLUX](https://huggingface.co/black-forest-labs) | Image generation | Yes for relevant releases | Yes | Model/version dependent | High-quality images |
| [Stable Diffusion](https://huggingface.co/stabilityai) | Image generation | Yes | Yes | Model/version dependent | Local image generation |
| [SDXL](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0) | Image generation | Yes | Yes | OpenRAIL-style | General image generation |
| [PixArt](https://huggingface.co/PixArt-alpha) | Image generation | Yes | Community hosted | Model-specific | Efficient image generation |
| [HunyuanImage](https://huggingface.co/tencent) | Image generation | Yes for released variants | Hosted options | Model-specific | Image generation |

### Image generation hardware

A 7B language model and a diffusion image model do not have the same VRAM requirements. Always check the exact model's inference guide.

---

# Image Matting & Background Removal

This is an area where specialized models are usually better than general AI.

| Model | Purpose | Local | Best for |
|---|---|---|---|
| [RMBG](https://huggingface.co/briaai/RMBG-2.0) | Background removal | Yes | Product photos, portraits |
| [SAM 2](https://github.com/facebookresearch/sam2) | Segmentation | Yes | Object masks |
| [MODNet](https://github.com/ZHKKKe/MODNet) | Portrait matting | Yes | Human portraits |
| [U2Net](https://github.com/xuebinqin/U-2-Net) | Salient object segmentation | Yes | Background removal |
| [BiRefNet](https://huggingface.co/ZhengPeng7/BiRefNet) | Background removal | Yes | High-quality segmentation |

Typical pipeline:

```text
Image
  ↓
Segmentation / Matting
  ↓
Mask
  ↓
Transparent background
```

For a simple background-removal feature, don't start with a giant LLM.

---

# Audio & Speech

## Speech-to-text

| Model | Size | Local | Best for |
|---|---:|---|---|
| [Whisper](https://github.com/openai/whisper) | Multiple | Yes | Speech recognition |
| [Whisper.cpp](https://github.com/ggml-org/whisper.cpp) | Runtime | Yes | CPU/mobile deployment |
| [Parakeet](https://huggingface.co/nvidia) | Multiple | Yes | Fast transcription |
| [FunASR](https://github.com/modelscope/FunASR) | Multiple | Yes | Speech recognition |

## Text-to-speech

| Model | Approx. size | Local | Best for |
|---|---:|---|---|
| [Kokoro-82M](https://huggingface.co/hexgrad/Kokoro-82M) | 82M | Yes | Fast TTS |
| [Piper](https://github.com/rhasspy/piper) | Small | Yes | Offline TTS |
| [F5-TTS](https://github.com/SWivid/F5-TTS) | ~300M+ | Yes | Voice synthesis/cloning |
| [XTTS](https://huggingface.co/coqui/XTTS-v2) | ~500M+ | Yes | Multilingual TTS/voice cloning |

For mobile/offline applications, small speech models can be much more practical than a general AI API.

---

# Retrieval, Embeddings and RAG

A common mistake is to think RAG is just:

```text
LLM + database
```

A better architecture is:

```text
                 User question
                       ↓
                 Embedding model
                       ↓
                  Vector search
                       ↓
                    Reranker
                       ↓
                Relevant documents
                       ↓
                     LLM
                       ↓
                    Answer
```

## Embedding models

| Model | Size | Local | Best for |
|---|---:|---|---|
| [Qwen3 Embedding](https://huggingface.co/Qwen) | Small → large | Yes | Multilingual RAG/search |
| [BGE-M3](https://huggingface.co/BAAI/bge-m3) | ~568M | Yes | Multilingual retrieval |
| [Nomic Embed](https://huggingface.co/nomic-ai) | Small | Yes | Semantic search |
| [E5](https://huggingface.co/intfloat) | Multiple | Yes | Retrieval |
| [EmbeddingGemma](https://huggingface.co/google/embeddinggemma-300m) | ~300M | Yes | Lightweight retrieval |

## Rerankers

| Model | Best for |
|---|---|
| [BGE Reranker](https://huggingface.co/BAAI) | RAG result ranking |
| [Jina Reranker](https://huggingface.co/jinaai) | Search/RAG |
| [Cohere Rerank](https://cohere.com/rerank) | Enterprise retrieval |

For a private Slack assistant, company knowledge base or documentation bot, embeddings and reranking can be just as important as the final LLM.

---

# Lightweight & Edge AI

This category matters when the model must run on:

- laptop CPU
- low-memory PC
- Android
- edge device
- Raspberry Pi
- small server

| Model | Size | Approx. class | Best for |
|---|---:|---|---|
| [Gemma 3 270M](https://ai.google.dev/gemma/docs/core/model_card_3) | 270M | Tiny | Classification, simple text |
| [Gemma 3 1B](https://ai.google.dev/gemma/docs/core/model_card_3) | 1B | Small | Local text |
| [Gemma 3 4B](https://ai.google.dev/gemma/docs/core/model_card_3) | 4B | Small | Local multimodal |
| [Gemma 3n E2B/E4B](https://ai.google.dev/gemma/docs/gemma-3n/model_card) | E2B/E4B | Edge | Mobile multimodal |
| [Phi-4-mini](https://huggingface.co/microsoft/Phi-4-mini-instruct) | ~3.8B | Small | Local reasoning/chat |
| [Qwen small models](https://huggingface.co/Qwen) | 0.6B+ | Small | General/coding |
| [Mistral Small / Ministral](https://huggingface.co/mistralai) | Small | Small | Local/general AI |
| [SmolLM](https://huggingface.co/HuggingFaceTB) | Small | Tiny | Edge/local experiments |

Google specifically positions Gemma 3 270M and 1B for mobile devices/single-board computers, while Gemma 3n E2B/E4B is designed for mobile and low-resource multimodal use. citeturn0search7

Gemma 3 also supports 128K context on its 4B, 12B and 27B sizes, while the 270M and 1B versions use 32K context. citeturn0search0

---

# Document AI and OCR

OCR is one of the most interesting areas for small specialized models.

| Model | Size | Local | Best for |
|---|---:|---|---|
| [PaddleOCR-VL](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.5) | ~1B | Yes | Document OCR |
| [GLM-OCR](https://huggingface.co/GLM-Edge) | Small | Yes/hosted | OCR + document understanding |
| [OvisOCR2](https://huggingface.co/AAI-ASC/OvisOCR2) | ~0.9B | Yes | OCR |
| [DeepSeek-OCR](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2) | ~3B | Yes | Document OCR |
| [Surya OCR](https://huggingface.co/datalab-to/surya) | ~0.7B class | Yes | OCR/layout |
| [LightOnOCR](https://huggingface.co/lightonai) | ~1B | Yes | Document OCR |
| [Granite-Docling](https://huggingface.co/ibm-granite/granite-docling-258M) | ~258M | Yes | Document parsing |
| [NuExtract](https://huggingface.co/numind) | Multiple | Yes | Structured extraction |

Hugging Face's current OCR index shows nearly 2,000 OCR-tagged models, including PaddleOCR-VL, OvisOCR2, Surya OCR, LightOnOCR, DeepSeek-OCR, Granite-Docling and others. citeturn0search6

### Example

```text
Invoice image
      ↓
OCR model
      ↓
Raw text + layout
      ↓
Extraction model / LLM
      ↓
{
  "invoice": "INV-123",
  "total": 450,
  "currency": "USD"
}
```

---

# Computer Vision

Computer vision models work with images and video without necessarily being language models.

| Model | Task | Local | Best for |
|---|---|---|---|
| [SAM 2](https://github.com/facebookresearch/sam2) | Segmentation | Yes | Object masks/video |
| [DINOv2](https://huggingface.co/facebook/dinov2-base) | Visual embeddings | Yes | Similarity/search |
| [YOLO](https://github.com/ultralytics/ultralytics) | Detection | Yes | Real-time object detection |
| [RT-DETR](https://github.com/lyuwenyu/RT-DETR) | Detection | Yes | Real-time detection |
| [Depth Anything](https://github.com/LiheYoung/Depth-Anything) | Depth estimation | Yes | 3D/depth |
| [MiDaS](https://github.com/isl-org/MiDaS) | Depth estimation | Yes | Monocular depth |
| [MobileSAM](https://github.com/ChaoningZhang/MobileSAM) | Segmentation | Yes | Lightweight segmentation |

This category is especially useful for Android camera applications.

---

# Video Generation

| Model | Local | API | Best for |
|---|---|---|---|
| [Wan 2.x](https://huggingface.co/Wan-AI) | Yes for released variants | Hosted options | Video generation |
| [LTX-Video](https://github.com/Lightricks/LTX-Video) | Yes | Hosted options | Local video generation |
| [HunyuanVideo](https://github.com/Tencent/HunyuanVideo) | Yes for released variants | Hosted options | Video generation |
| [CogVideoX](https://github.com/THUDM/CogVideo) | Yes | Hosted options | Text/image to video |
| [Open-Sora](https://github.com/hpcaitech/Open-Sora) | Yes | Community | Research/open video generation |

Video models usually need considerably more GPU memory than small language models.

---

# Translation and Language

| Model | Purpose | Local | Best for |
|---|---|---|---|
| [NLLB](https://huggingface.co/facebook/nllb-200-distilled-600M) | Translation | Yes | 200-language translation |
| [M2M100](https://huggingface.co/facebook/m2m100_418M) | Translation | Yes | Multilingual translation |
| [MADLAD-400](https://huggingface.co/google/madlad400-3b-mt) | Translation | Yes | Large multilingual coverage |
| [TranslateGemma](https://ai.google.dev/gemma/docs/translate) | Translation | Yes | Translation |
| [SeamlessM4T](https://huggingface.co/facebook/seamless-m4t-v2-large) | Speech/text translation | Yes | Speech + language translation |

---

# Agents and Computer Use

An agent is not necessarily a new model architecture. Often it is:

```text
LLM
 +
Tools
 +
Memory
 +
Planning
 +
Execution loop
```

Useful models:

| Model | Agent capability | Local | Best for |
|---|---|---|---|
| [Devstral](https://huggingface.co/mistralai) | Software agent | Yes for open releases | Coding |
| [UI-TARS](https://huggingface.co/ByteDance-Seed/UI-TARS-1.5-7B) | GUI agent | Yes | Computer interaction |
| [Qwen](https://huggingface.co/Qwen) | Tool calling / agent workflows | Yes | General agents |
| [Llama](https://huggingface.co/meta-llama) | Tool use | Yes | Local agents |
| [Claude](https://www.anthropic.com/claude) | Tool use | No | Coding/research agents |
| [GPT](https://platform.openai.com/docs/models) | Tool use | No | General agents |
| [Gemini](https://ai.google.dev/gemini-api/docs/models) | Tool use/multimodal | No | General agents |

For agents, model quality is only part of the system. Tool reliability, permissions, state management and error recovery matter just as much.

---

# Commercial / Closed Models

These models are usually accessed through an API or hosted application.

| Model family | Company | Local weights | API | Typical use |
|---|---|---|---|---|
| [GPT](https://platform.openai.com/docs/models) | OpenAI | No | Yes | General AI, reasoning, coding, agents |
| [Claude](https://www.anthropic.com/claude) | Anthropic | No | Yes | Coding, reasoning, enterprise |
| [Gemini](https://ai.google.dev/gemini-api/docs/models) | Google | No for Gemini | Yes | Multimodal, reasoning, agents |
| [Grok](https://x.ai/api) | xAI | No for current flagship models | Yes | Reasoning, coding, agents |
| [Cohere Command](https://cohere.com/command) | Cohere | Some open releases / mixed | Yes | Enterprise/RAG |
| [Amazon Nova](https://aws.amazon.com/bedrock/) | AWS | No for main hosted models | Yes | Enterprise/AWS |

The important point is that **API access does not mean the model is open source**.

For example:

```text
Closed model:

Your app
   ↓
API
   ↓
Company server
   ↓
Model
```

Whereas:

```text
Open-weight model:

Your app
   ↓
Local runtime
   ↓
Downloaded model
   ↓
Your GPU/CPU
```

---

# Open Model + API vs Open Model Without API

You can have both.

## Open model + hosted API

```text
Qwen
   ↓
Downloadable weights
   +
Cloud providers
   ↓
API
```

## Open model + self-hosting

```text
Qwen
   ↓
Download
   ↓
Ollama / vLLM / llama.cpp
   ↓
Your machine
```

## Closed model + API

```text
GPT / Claude / Gemini
       ↓
Provider API
       ↓
Provider GPU
```

---

# Model Selection Criteria

Before choosing a model, check:

### 1. Task

What are you actually trying to solve?

```text
Chat       → LLM
Coding     → Coding model
OCR        → OCR model
Search     → Embedding + reranker
Image      → Vision model
Speech     → Speech model
Video      → Video model
Agent      → Tool-capable LLM
```

### 2. Model size

Rough rule:

```text
< 1B       Tiny
1B–4B      Small
4B–14B     Small/medium
14B–32B    Medium
32B–70B    Large
70B+       Heavy
```

These are practical categories, not official industry standards.

### 3. Context

Context tells you approximately how much input the model can process in one request.

Example:

```text
4K
16K
32K
64K
128K
256K
1M+
```

More context is useful for:

- large documents
- repositories
- long conversations
- RAG
- research

But a large context window does not automatically mean the model will reason equally well over every token.

### 4. License

Check:

- commercial use
- redistribution
- modification
- attribution
- model hosting
- acceptable-use restrictions

### 5. Hardware

A model may be downloadable but still impractical for your machine.

### 6. Quantization

Common formats:

```text
FP32
FP16
BF16
INT8
INT4
Q8
Q6
Q5
Q4
```

Quantization reduces memory requirements, usually with some quality tradeoff.

---

# Hardware-Based Recommendations

These are **rough practical recommendations**, not exact requirements. Actual memory use depends on architecture, quantization, context length, runtime and batch size.

## CPU only

Good candidates:

| Model | Suggested use |
|---|---|
| Gemma 270M | Tiny text tasks |
| Gemma 1B | Small local assistant |
| Qwen 0.6B–1.7B class | Small general/coding tasks |
| Phi small models | Local text |
| Kokoro-82M | TTS |
| Whisper tiny/base | Speech recognition |
| Small OCR models | OCR |
| Embedding models | RAG/search |

Expect slower generation than GPU inference.

---

## 8 GB VRAM

Good target:

| Model class | Typical target |
|---|---|
| 0.3B–4B | Excellent |
| 7B–8B 4-bit | Usually practical |
| 12B–14B 4-bit | Possible depending on runtime/context |
| OCR 0.5B–3B | Good |
| Vision models | Depends heavily on architecture |
| Embedding/reranker models | Usually easy |

For an 8 GB GPU, **7B/8B 4-bit models are often a sweet spot**.

---

## 24 GB VRAM

Good target:

| Model class | Typical target |
|---|---|
| 7B–14B | Very comfortable |
| 20B–32B 4-bit | Often practical |
| 70B 4-bit | Generally requires careful memory management/offload and may exceed a single 24 GB card depending on runtime |
| Vision models | Much more flexibility |
| OCR | Very comfortable |
| Coding agents | Good |
| Embeddings/RAG | Excellent |

24 GB is a very useful local-AI tier.

---

# Comparison Table

The following table is intended as a quick starting point.

| Model | Params | Context | VRAM target* | License / access | Best For |
|---|---:|---:|---:|---|---|
| Gemma 3 270M | 270M | 32K | <2 GB | Gemma Terms | Tiny/local |
| Gemma 3 1B | 1B | 32K | ~2–3 GB | Gemma Terms | Small AI |
| Gemma 3 4B | 4B | 128K | ~4–8 GB | Gemma Terms | Multimodal/local |
| Phi-4-mini | ~3.8B | Model dependent | ~4–8 GB | MIT/model terms | Local reasoning |
| Qwen small | 0.6B+ | Model dependent | ~2–8 GB | Model-specific | Local/general |
| Mistral Small | Small/medium | Model dependent | ~8–16+ GB | Model-specific | General AI |
| DeepSeek-R1 distilled | 1.5B–70B | Model dependent | ~2–48+ GB | MIT/model terms | Reasoning |
| DeepSeek Coder | Multiple | Model dependent | ~4–24+ GB | Model-specific | Coding |
| Devstral | Multiple | Up to 256K on relevant releases | ~16–24+ GB | Model-specific | Coding agents |
| BGE-M3 | ~568M | Model dependent | <4 GB | Open | RAG retrieval |
| Qwen Embedding | Small → large | Model dependent | <4–16+ GB | Model-specific | RAG/search |
| Kokoro | 82M | N/A | <2 GB | Apache 2.0 | TTS |
| Whisper | Multiple | Audio window | <4–8 GB | MIT | Speech-to-text |
| PaddleOCR-VL | ~1B | Model dependent | ~4–8 GB | Open | OCR |
| DeepSeek-OCR | ~3B | Model dependent | ~8 GB+ | Model-specific | OCR |
| Granite-Docling | ~258M | Model dependent | <4 GB | Apache 2.0 | Document AI |
| SAM 2 | Multiple | Video dependent | ~4–12 GB | Apache 2.0 | Segmentation |
| DINOv2 | Multiple | N/A | ~2–8 GB | Apache 2.0 | Vision embeddings |
| YOLO | Multiple | N/A | <8 GB | Model-specific | Object detection |
| FLUX | Large | Model dependent | Often 12–24+ GB | Model-specific | Image generation |
| Wan | Large | Model dependent | Often 16–24+ GB+ | Model-specific | Video generation |

\* **VRAM values are practical estimates, not official hardware requirements.** Quantization, context length, runtime and batching can change memory usage substantially.

---

# Example: Building a Local AI Assistant

A useful local assistant does not need one giant model.

For example:

```text
                   LOCAL AI ASSISTANT
                           │
          ┌────────────────┼────────────────┐
          │                │                │
       Chat/Coding        RAG             OCR
          │                │                │
       Qwen/Mistral    Qwen Embed        OCR model
       /Gemma          + BGE             + parser
          │                │                │
          └────────────────┼────────────────┘
                           ↓
                    Local knowledge
                           ↓
                    Final response
```

For a Slack knowledge assistant:

```text
Slack
  ↓
Message ingestion
  ↓
Chunking
  ↓
Embedding model
  ↓
Vector database
  ↓
Reranker
  ↓
Local LLM
  ↓
Answer
```

You could use:

```text
Embedding  → Qwen3 Embedding / BGE-M3
Reranking  → BGE Reranker
LLM        → Qwen / Mistral / Gemma / DeepSeek
OCR        → PaddleOCR-VL / Granite-Docling
Runtime    → Ollama / llama.cpp / vLLM
```

---

# Example: Android AI Application

For an Android application, the architecture can be:

```text
Android
   │
   ├── On-device
   │      ├── Small LLM
   │      ├── OCR
   │      ├── Speech
   │      └── Vision
   │
   └── Cloud
          ├── Large reasoning model
          ├── Large coding model
          └── Large multimodal model
```

For on-device AI, look first at:

- Gemma small models
- Gemma 3n
- Phi small models
- Qwen small models
- Whisper/Whisper.cpp
- Kokoro/Piper
- MobileSAM
- small OCR models

Google explicitly lists Gemma 3 270M/1B for mobile devices and Gemma 3n for mobile multimodal workloads. citeturn0search7turn0search8

---

# Model Selection Cheat Sheet

| If you need... | Start with... |
|---|---|
| Tiny local chatbot | Gemma 270M/1B, Qwen small |
| Local general AI | Gemma, Qwen, Mistral |
| Local reasoning | DeepSeek distilled, Qwen reasoning |
| Coding | Qwen Coder, Devstral, DeepSeek Coder |
| Coding agent | Devstral |
| OCR | PaddleOCR-VL, DeepSeek-OCR, Granite-Docling |
| RAG | Qwen Embedding + BGE Reranker |
| Semantic search | BGE-M3, Qwen Embedding, Nomic |
| Speech-to-text | Whisper |
| Offline TTS | Kokoro, Piper |
| Voice cloning | F5-TTS, XTTS |
| Background removal | RMBG, BiRefNet, MODNet |
| Object segmentation | SAM 2 |
| Object detection | YOLO |
| Visual embeddings | DINOv2 |
| Image generation | FLUX, Stable Diffusion |
| Video generation | Wan, LTX-Video, HunyuanVideo |
| Translation | NLLB, MADLAD, TranslateGemma |
| GUI automation | UI-TARS |
| Enterprise RAG | Granite, Cohere, Mistral |
| Cloud frontier AI | GPT, Claude, Gemini, Grok |

---

# Important: Don't Choose a Model by Parameter Count Alone

This is a common mistake:

```text
70B > 14B > 7B > 3B
```

That is **not a universal rule**.

A better way to think about it is:

```text
                TASK
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
      OCR       Coding     RAG
       │          │          │
    OCR model   Code model  Embed
       │          │          │
       ↓          ↓          ↓
     Best fit  Best fit    Best fit
```

A 1B OCR model may be more useful for OCR than a 70B general LLM.

A 300M embedding model may be more useful for retrieval than a 70B chatbot.

An 82M TTS model may be more useful for speech synthesis than a giant multimodal model.

---

# A Practical Ranking by Hardware

## Very low hardware

```text
< 8 GB RAM / VRAM
```

Look at:

- Gemma 270M
- Gemma 1B
- Qwen 0.6B–1.7B class
- Phi small models
- Kokoro
- Whisper tiny/base
- small OCR models
- embedding models

## Mid-range

```text
8–16 GB VRAM
```

Look at:

- Gemma 4B/12B depending on quantization
- Qwen 7B/14B class
- Mistral small models
- Phi
- DeepSeek distilled models
- coding models around 7B–14B
- OCR/VLM models

## High-end consumer

```text
24 GB VRAM
```

Look at:

- Qwen 14B–32B class
- larger Mistral models
- larger coding models
- multimodal models
- 4-bit larger models with careful configuration
- image/video models

## Server

```text
48 GB+
```

You can start considering:

- 70B-class models
- larger MoE models
- large multimodal models
- video generation
- multiple concurrent users
- high-context workloads

---

# Where to Download / Run Models

### Hugging Face

The biggest general-purpose model hub:

**https://huggingface.co/models**

Use it for:

- model weights
- model cards
- licenses
- quantized versions
- adapters
- community fine-tunes

### Ollama

**https://ollama.com**

Good for quickly running local LLMs.

```bash
ollama run qwen3
```

### llama.cpp

**https://github.com/ggml-org/llama.cpp**

Excellent for CPU/GPU local inference and GGUF models.

### vLLM

**https://github.com/vllm-project/vllm**

Better suited to serving models as an API, especially on GPUs.

### Google Gemma

**https://ai.google.dev/gemma**

### Mistral

**https://huggingface.co/mistralai**

### Qwen

**https://huggingface.co/Qwen**

### DeepSeek

**https://huggingface.co/deepseek-ai**

### Microsoft

**https://huggingface.co/microsoft**

### Meta Llama

**https://huggingface.co/meta-llama**

---

# Final Takeaway

There isn't one "best AI model".

There are different winners for different jobs:

```text
General AI
    → GPT / Claude / Gemini / Qwen / Llama / Mistral

Reasoning
    → DeepSeek / Qwen / GPT / Gemini / Claude

Coding
    → Devstral / Qwen Coder / DeepSeek Coder / GPT Codex / Claude

OCR
    → PaddleOCR-VL / DeepSeek-OCR / Granite-Docling

RAG
    → Qwen Embedding / BGE-M3 + reranker

Speech
    → Whisper / Parakeet / Kokoro

Image
    → FLUX / Stable Diffusion

Segmentation
    → SAM 2

Object detection
    → YOLO

Video
    → Wan / LTX-Video / HunyuanVideo

Translation
    → NLLB / MADLAD / TranslateGemma

Small / Edge
    → Gemma / Phi / Qwen small / SmolLM

Computer agents
    → UI-TARS / Devstral + tools
```

The most useful skill is therefore not memorizing model names. It is learning to ask:

> **What is the task, what hardware do I have, what license do I need, and do I need local inference or an API?**

---

## Sources and further reading

- [Hugging Face Models](https://huggingface.co/models)
- [Google Gemma](https://ai.google.dev/gemma)
- [Google Gemma model card](https://ai.google.dev/gemma/docs/core/model_card_3)
- [Google Gemma releases](https://ai.google.dev/gemma/docs/releases)
- [Mistral Models](https://docs.mistral.ai/models/)
- [OpenAI Models](https://platform.openai.com/docs/models)
- [Anthropic Claude](https://www.anthropic.com/claude)
- [Qwen on Hugging Face](https://huggingface.co/Qwen)
- [DeepSeek on Hugging Face](https://huggingface.co/deepseek-ai)
- [Microsoft Models](https://huggingface.co/microsoft)
- [Meta Llama](https://huggingface.co/meta-llama)
- [Ollama](https://ollama.com)
- [llama.cpp](https://github.com/ggml-org/llama.cpp)
- [vLLM](https://github.com/vllm-project/vllm)
- [OpenAI Whisper](https://github.com/openai/whisper)
- [SAM 2](https://github.com/facebookresearch/sam2)

---

## Disclaimer

Model availability, versions, context limits, licenses and API pricing change frequently. Always check the official model card and license before using a model in a commercial product.

The VRAM figures in this document are practical estimates for common quantized deployments, not vendor guarantees. Actual memory requirements depend on quantization, context length, runtime, batch size and whether part of the model is offloaded to system RAM.
