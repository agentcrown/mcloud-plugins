---
name: cloud-models
description: Compare where to buy AI model APIs (Claude, GPT, Nova, Qwen, Kimi and others) through the major clouds, per million tokens at the customer's reseller discount, with a monthly cost estimate and data-residency options. Use when the user asks what a model costs, which cloud to buy Claude or another model through, how much an LLM workload will cost per month, or whether a model can run with data staying in Singapore.
---

# Cloud models

Uses the `mcloud` MCP server tool `compare_models`.

Model usage bought through a cloud (for example Claude on AWS Bedrock) is billed on the
customer's cloud account at their reseller discount.

## Workflow

1. **Pin down the need**: the model or model family, and if they know it, monthly volume in
   millions of input and output tokens. Ask whether data must stay in the region (for example
   Singapore) if the use involves personal or regulated data.
   - Rough guide when volume is unknown: a chat assistant for 100 staff is often 50-200
     million input and 10-40 million output tokens a month. Say it is an assumption.
2. **Call `compare_models`** with `model` (a name or part of it), `input_mtok_per_month`,
   `output_mtok_per_month`, and `data_must_stay_in_region: true` when residency matters.
3. **Present a short table**: model, cloud and platform, region, tier, input / output price
   per million tokens (list, discount %, final), and the monthly estimate when volumes were
   given. Repeat every entry in `notes`.
   - `tier`: `regional` = processed in that region; `datazone` = stays within a
     multi-country zone; `global` = may be routed to any country. Point this out whenever
     the cheapest option is not regional.
   - Mention `price_note` when present (e.g. tiered pricing), and say when `price_stale` is true.
4. For a formal quote or to start buying, hand over to the account manager; model usage is
   not ordered through `request_purchase`.

Never invent prices or claim a model is available where the tool did not return it. Reply
in the user's language.
