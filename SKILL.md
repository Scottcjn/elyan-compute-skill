---
name: elyan-compute
description: "Submit inference, vision, text-to-speech, and video generation jobs to Elyan Labs GPU compute endpoints (V100, RTX 5070, POWER8) via x402 USDC micropayments on Base chain. Use when the user wants to run remote inference, rent cloud GPU compute, generate images or video, convert text to speech, or access pay-per-request GPU endpoints."
auto-activate: true
requires:
  tools: [x402_fetch]
---

# Elyan Labs Compute Marketplace

Submit compute jobs to Elyan Labs' GPU infrastructure in Baton Rouge, LA. All endpoints use x402 USDC micropayments on Base (chain 8453).

## Request Lifecycle

1. Send a POST request to the endpoint with the required JSON body.
2. If no payment is attached, the endpoint returns **HTTP 402** with x402 payment requirements.
3. The `x402_fetch` tool handles USDC payment automatically on Base chain.
4. On success, the endpoint returns **HTTP 200** with the result (JSON for inference/vision, WAV audio for TTS, video URL for video).
5. On failure, expect **HTTP 400** (malformed request), **HTTP 402** (payment failed or insufficient), or **HTTP 503** (GPU unavailable). Retry 503 after a brief delay.

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

## Response Validation

- **Inference/Vision**: Verify the JSON response contains a non-empty `response` or `result` field before presenting to the user.
- **TTS**: Confirm the returned WAV data is non-empty (Content-Length > 0) before saving or playing audio.
- **Video**: Check that the response includes a valid URL and that the video file is accessible before sharing with the user.

## Alternative Payment

Also accepts RustChain RTC via `X-RTC-Payment` header (1 RTC = $0.10 USD).

## Discovery

- Agent Card: `http://50.28.86.131:8070/beacon/.well-known/agent-card.json`
- Compute Catalog: `http://50.28.86.131:8070/beacon/api/compute/catalog`
- x402 Pricing: `http://50.28.86.131:8070/beacon/api/x402/pricing`
