# Zap configuration — "Summarize webhook data with Claude and send to Slack"

Zapier doesn't support a single-file portable export the way n8n and Make.com do, so this documents the exact real step configuration from the live Zap instead.

## Step 1: Trigger — Webhooks by Zapier (Catch Hook)

- **Event:** Catch Hook
- Zapier generates a unique webhook URL that accepts any posted JSON payload.
- No external account connection needed — this is Zapier's own native webhook trigger.

## Step 2: Action — Anthropic (Claude) → Send Message

- **Connection:** real Anthropic API key, authenticated directly (Zapier has no built-in AI gateway the way n8n/Make do — this is the one integration of the four that required genuine API key setup, the same pattern a client's own production environment would use).
- **Model:** Claude Sonnet 5.5
- **User Message:**
  ```
  Summarize the following text in 2-3 concise sentences:

  {{1. Submission Text}}
  ```
  (`{{1. Submission Text}}` pulls the `submission_text` field straight from step 1's webhook payload.)
- **System prompt / Memory Key:** left blank — stateless, single-turn summarization.

## Step 3: Action — Slack → Send Channel Message

- Left deliberately unconfigured (no Slack connection) — same honest call as the n8n and Make.com builds. Parish doesn't use Slack day-to-day, so faking a connection would misrepresent the build. Fully wired up to Claude's output; just needs a real Slack OAuth connection to go live.

## Tested live

Fired a real webhook payload directly via `curl`. Zapier's trigger caught the real record, then the Claude step ran for real — confirmed via a genuine Anthropic completion ID in Zapier's own execution log, with accurate summary text returned.
