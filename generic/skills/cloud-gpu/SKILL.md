---
name: cloud-gpu
description: Compare and quote GPU cloud servers (H100, H200, A100, L40S, L4, T4 and others) across clouds in Singapore and nearby APAC regions, at the customer's reseller discount. Use when the user asks where to rent GPUs, which cloud has a card in stock or cheapest, the cost of a GPU cluster for training or inference, or wants to buy GPU capacity.
---

# Cloud GPU

Uses the `mcloud` MCP server tools: `compare_gpu`, `build_quote`, `request_purchase`.

The newest cards are often not offered in Singapore, so results also cover nearby regions
(Jakarta, Tokyo, Mumbai or Pune, Hong Kong, Bangkok). Always say which region each option is in;
latency and data-residency needs may rule some out.

## Workflow

1. **Pin down the need**: card (or "any card with at least N GB of GPU memory"), GPUs per
   server, number of servers, how long (hours, months, a year), and region limits
   (e.g. data must stay in Singapore). Ask for what is missing, or state assumptions.
   - Rough guide when the user only names a workload: inference of small models or
     video: L4 or T4; mid-size models: L40S or A100; training or large-model inference:
     H100 or H200; multi-server training needs 8-GPU servers.
2. **Call `compare_gpu`** with `gpu_model`, `min_gpus`, and `regions` if limited. Use
   `term: "one_year"` for commitments of a year or more.
3. **Present options** as a short table: cloud, region, instance type, card x count, GPU
   memory, price per GPU per month, server price per month (list price, discount %, final),
   and `availability`. Repeat every entry in `notes`.
   - `availability`: `in_stock`, `low_stock` and `sold_out` come from the cloud;
     `confirm_with_account_manager` means the cloud does not report stock.
   - If `discount_configured` is false, the row is at list price; say so.
4. **Quote** with `build_quote` using the chosen `offer_id`s, as in the `cloud-quote` skill.

## When the user wants to buy

Follow the `cloud-quote` purchase steps, and for GPU items also collect, before calling
`request_purchase`:

- `end_user_company`: the company that will use the GPUs
- `ultimate_parent_company`: that company's ultimate parent
- `end_user_country`: where the end user is based
- `end_use`: what the GPUs will be used for

These are needed for export-control screening; the request is refused without them. Tell
the user their account manager will confirm capacity and complete a short review before
the final quote.

Never invent prices, stock or regions that did not come from the tools. Google Cloud GPU
prices are not included yet. Reply in the user's language.
