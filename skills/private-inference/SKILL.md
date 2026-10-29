---
name: private-inference
description: Ask a private model on OffRouter, or compare several, with the prompt encrypted to a GPU enclave. Use for a second opinion on sensitive code, contracts, strategies or anything that should not reach a model provider in the clear.
---

# Private inference with OffRouter

## When to use

- The user wants a second opinion on code, a smart contract or a plan without sending it to a model provider in the clear.
- The user asks for a specific open model (DeepSeek, Qwen, GLM, Kimi, Gemma, gpt-oss and others).
- The user wants to compare how several models answer the same question.

## Instructions

1. If you have not checked the enclave yet in this session, call `verify_enclave` and report the result in one line.
2. Call `list_models` if you need to pick a model. Prefer one whose context length fits the input, and a vision model when sending an image.
3. Build the prompt. Include only the code and context the question needs, and redact secrets such as private keys, seed phrases and API keys.
4. Call `ask` with the model and prompt, or `compare` with two to four models for the same prompt.
5. Give the user the answer, then one line with the model, the cost and the receipt link.
6. If a call fails because the free demo is used up, say so and explain that a prepaid key (`OFFROUTER_API_KEY`) or a wallet (`OFFROUTER_WALLET_KEY`) lifts the limit, as described in the plugin's README.
