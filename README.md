# Zapier: AI-Powered Zap

A Zap: a webhook trigger catches incoming data, Claude generates a summary, ready to route downstream.

## What it does

1. **Trigger** - a Zapier webhook catches an incoming POST request.
2. **AI step** - the payload is sent to Claude via a real Anthropic API key (not a platform-managed AI gateway), prompted to produce a summary.
3. **Output** - ready to route to any downstream Zapier step.

## Why this one's different from the n8n/Make builds

Zapier has no built-in Claude gateway, so this integration required setting up genuine API key authentication with Anthropic directly inside the Zap - the same pattern a client's own production environment would actually use, rather than a platform shortcut. Useful proof point for a client whose stack doesn't have a managed AI connector either.

## Tested live

Fired a real webhook payload - Claude returned an accurate summary, confirmed via a real Anthropic API completion ID visible in Zapier's own execution log.

## Zap export

`zap-steps.md` documents the exact step configuration (webhook trigger → Code/Webhooks step calling the Anthropic API → placeholder output action), since Zapier doesn't support a portable single-file export the way n8n/Make do.

---
Part of a small portfolio of tested automation/AI builds — see [ParishSynthMind](https://github.com/ParishSynthMind) for the others.
