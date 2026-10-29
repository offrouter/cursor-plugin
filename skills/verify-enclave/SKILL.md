---
name: verify-enclave
description: Check from this machine that OffRouter's models really run in a GPU enclave, and show the key prompts are encrypted to. Use when the user asks whether OffRouter is private, or before sending anything sensitive.
---

# Verify the enclave

## When to use

- The user asks "is this really private?" or "can OffRouter read my prompts?"
- Before the first private call with sensitive input in a session.

## Instructions

1. Call `verify_enclave`.
2. Explain the result in plain words:
   - the hardware quote verified up to Intel's root certificate;
   - the report was made just now for a fresh nonce, so it is not a replay;
   - the boot log matches the measured, open-source enclave gateway;
   - the public key prompts are encrypted to.
3. If any check fails, say so clearly and do not send sensitive input until it passes.
4. Mention what stays visible either way: the model chosen, settings, sizes, timing, the IP address and who paid. The prompt and the answer do not.
