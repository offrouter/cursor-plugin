# OffRouter for Cursor

Private inference inside Cursor. [OffRouter](https://offrouter.org) runs open models (DeepSeek, Qwen, GLM, Kimi, Gemma, gpt-oss and more) inside GPU enclaves, Intel TDX with an NVIDIA confidential GPU. This plugin adds the OffRouter MCP server, which encrypts your prompt on your own machine to a key the enclave proves it holds. The gateway in between only ever sees ciphertext, and every answer comes back with a signed receipt.

Use it for a second opinion on code, contracts or plans you would rather not send to a model provider in the clear.

## What's inside

| | |
| --- | --- |
| MCP server `offrouter` | the open-source [OffRouter MCP server](https://github.com/offrouter/mcp), run locally with `npx` |
| Skill `private-inference` | ask one private model, or compare two to four, and report cost and receipt |
| Skill `verify-enclave` | check the enclave from your machine and explain what was verified |
| Rule `offrouter` | when to reach for a private model, and never to paste secrets into a prompt |

Tools: `list_models`, `ask`, `compare`, `account` and `verify_enclave`.

## Install

Install **OffRouter** from the Cursor Marketplace, or try it from this repository:

```bash
git clone https://github.com/offrouter/cursor-plugin ~/.cursor/plugins/local/offrouter
```

Then run **Developer: Reload Window**. Node 20 or newer is needed for the MCP server.

## Try it, then add a key

With nothing configured, the server uses OffRouter's free demo: one model and a few calls a day. Ask the agent something like "use OffRouter to verify the enclave" or "ask a private model on OffRouter to review this function".

For every model, give the `offrouter` MCP server one of these in Cursor's MCP settings (its `env`):

| Variable | How it pays |
| --- | --- |
| `OFFROUTER_API_KEY` | a prepaid key (`off_sk_…`), billed per token. Get one at [offrouter.org/dashboard](https://offrouter.org/dashboard) |
| `OFFROUTER_WALLET_KEY` | pay per call in stablecoins from a wallet, capped by `OFFROUTER_MAX_USD` (default $0.10). Use a dedicated wallet with a small balance |

Every variable is listed in the [MCP server's README](https://github.com/offrouter/mcp#configuration).

## What stays private

- The gateway cannot read your prompts or the answers, and holds no key that could open them.
- Before anything is sent, the server checks the enclave's hardware report up to Intel's root, for a fresh nonce, against the measured open-source enclave gateway. If a check fails, nothing is sent.
- Still visible: the model you picked, settings like `max_tokens`, the size of the ciphertext, timing, your IP address and who paid. Cursor itself sees the prompt and the answer, since that is where they come from and go to.

## Links

- [offrouter.org](https://offrouter.org) · [Docs](https://docs.offrouter.org) · [Models](https://offrouter.org/models)
- [OffRouter MCP server](https://github.com/offrouter/mcp)
- [@OffRouter on X](https://x.com/OffRouter)

## License

MIT
