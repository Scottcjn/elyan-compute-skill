# Elyan Labs Compute Skill

Conway Automaton skill for accessing GPU compute via x402 USDC micropayments.

Part of the [Beacon Protocol](https://github.com/Scottcjn/beacon-skill) ecosystem — uses [`beacon_skill.compute_marketplace`](https://github.com/Scottcjn/beacon-skill/blob/main/beacon_skill/compute_marketplace.py) and [`openclaw-x402`](https://github.com/Scottcjn/openclaw-x402) for payment.

## Install

Conway agents can install this skill:

```
installSkill("https://github.com/Scottcjn/elyan-compute-skill", "elyan-compute")
```

Or fetch the SKILL.md directly:

```
installSkillFromUrl("https://raw.githubusercontent.com/Scottcjn/elyan-compute-skill/main/SKILL.md", "elyan-compute")
```

## Endpoints

| Endpoint | Price | Hardware |
|----------|-------|----------|
| `/api/compute/inference` | $0.01 | POWER8 512GB (Ollama) |
| `/api/compute/vision` | $0.05 | BAGEL-7B on V100 |
| `/api/compute/tts` | $0.02 | XTTS on RTX 4070 |
| `/api/compute/video` | $0.50 | ComfyUI on V100 32GB |

## Payment

All endpoints return HTTP 402 with x402 payment requirements. Compatible with any x402 client library. Payments in USDC on Base (chain ID 8453).

Dual economy: also accepts RustChain RTC tokens (1 RTC = $0.10 USD) via `X-RTC-Payment` header.

## Hardware

12 GPUs totaling 192GB VRAM across V100 32GB, V100 16GB, RTX 5070, RTX 4070, RTX 3060, and M40 cards. Plus IBM POWER8 S824 with 128 threads and 512GB RAM for large model inference. Hailo-8 TPU and 2x Alveo U30 FPGA for specialized workloads.

All infrastructure located in Baton Rouge, LA.

## Ecosystem

- [Beacon Protocol](https://github.com/Scottcjn/beacon-skill) — Agent orchestrator (13 transports, scorecard dashboard)
- [openclaw-x402](https://github.com/Scottcjn/openclaw-x402) — x402 payment middleware (used by this skill)
- [BoTTube](https://bottube.ai) — AI video platform
- [RustChain](https://github.com/Scottcjn/Rustchain) — Proof-of-Antiquity blockchain
- [Silicon Archaeology](https://github.com/Scottcjn/silicon-archaeology-skill) — Vintage hardware cataloging
- [Grazer](https://github.com/Scottcjn/grazer-skill) — Multi-platform discovery
- [Beacon Atlas](https://rustchain.org/beacon/) — Live agent directory (31+ agents)
- [Compute Catalog](https://rustchain.org/beacon/api/compute/catalog)

## License

MIT
