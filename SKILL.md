---
name: elyan-compute
description: "Access Elyan Labs GPU compute marketplace — V100, RTX 5070, POWER8 inference endpoints via x402 USDC micropayments"
auto-activate: true
requires:
  tools: [x402_fetch]
---

# Elyan Labs Compute Marketplace

You have access to Elyan Labs' GPU compute infrastructure in Baton Rouge, LA. All endpoints accept x402 USDC micropayments on Base (chain 8453).

## Available Endpoints

### LLM Inference — $0.01/request
```
POST http://50.28.86.131:8070/beacon/api/compute/inference
Content-Type: application/json

{"model": "llama3.2:3b", "prompt": "Your prompt here", "system": "optional system prompt"}
```
Hardware: IBM POWER8 S824, 512GB RAM, 128 threads. Models: llama3.2:3b, llama3.1:8b, qwen2.5:14b, deepseek-r1:32b.

### Vision Understanding — $0.05/request
```
POST http://50.28.86.131:8070/beacon/api/compute/vision
Content-Type: application/json

{"image_url": "https://example.com/photo.jpg", "prompt": "Describe this image"}
```
Hardware: BAGEL-7B-MoT on V100 16GB (NF4 quantized).

### Text-to-Speech — $0.02/request
```
POST http://50.28.86.131:8070/beacon/api/compute/tts
Content-Type: application/json

{"text": "Hello world", "language": "en"}
```
Hardware: XTTS on RTX 4070 8GB. Returns WAV audio.

### Video Generation — $0.50/request
```
POST http://50.28.86.131:8070/beacon/api/compute/video
Content-Type: application/json

{"prompt": "A robot walking through a swamp at sunset", "width": 720, "height": 720}
```
Hardware: LTX-2 / ComfyUI on V100 32GB.

## Discovery

- Agent Card: `http://50.28.86.131:8070/beacon/.well-known/agent-card.json`
- Compute Catalog: `http://50.28.86.131:8070/beacon/api/compute/catalog`
- x402 Pricing: `http://50.28.86.131:8070/beacon/api/x402/pricing`

## Payment

All endpoints return HTTP 402 with x402 payment requirements if called without payment. Your x402 client handles USDC payment automatically on Base chain.

Also accepts RustChain RTC via `X-RTC-Payment` header (1 RTC = $0.10 USD).

## Hardware Inventory

| GPU | VRAM | Count |
|-----|------|-------|
| V100 32GB | 32GB | 2 |
| V100 16GB | 16GB | 3 |
| RTX 5070 | 12GB | 2 |
| RTX 4070 | 8GB | 1 |
| RTX 3060 | 12GB | 2 |
| M40 | 12GB | 2 |

**Total: 12 GPUs, 192GB VRAM** + IBM POWER8 S824 (128 threads, 512GB RAM) + Hailo-8 TPU + 2x Alveo U30 FPGA

Built by [Elyan Labs](https://github.com/Scottcjn) in Baton Rouge, LA.
