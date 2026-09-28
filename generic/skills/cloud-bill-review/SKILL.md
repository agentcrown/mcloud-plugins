---
name: cloud-bill-review
description: Review the customer's own cloud bill (billed through their reseller) and find savings. Use when the user asks what they spent on cloud last month, why their cloud bill went up, which products or instances cost the most, or how to cut their cloud costs.
---

# Cloud bill review

Uses the `mcloud` MCP server tools: `get_cost_report`, `list_savings`, and for follow-up
pricing `compare_instances` and `build_quote`.

These tools read only the caller's own accounts; the API key decides which accounts. Bills
are fetched once a day, so the current month is incomplete. Default to last month.

## Workflow

1. **Call `get_cost_report`** with `month` (`YYYY-MM`, or omit for last month).
   - If `status` is `no_billing_accounts`, repeat its `message` and stop. Do not guess figures.
2. **Summarise the month** in a few lines:
   - Total (`total_usd`) and change versus the previous month (`change_pct`)
   - What they saved against list price (`saved_vs_list_usd`)
   - Split by cloud (`by_provider`) and by billing mode (`by_pay_mode`)
   - The biggest products (`top_products`) and instances (`top_instances`)
   - If `change_pct` is large, point to the products or instances that explain it.
3. **Call `list_savings`** for the same month when the user asks about saving money, or when
   on-demand spend is a large share of the total.
   - For each suggestion, show the instance, hours run, current monthly cost, estimated saving
     and its `basis`. Say "estimate" when the basis says so.
   - Give the monthly total (`total_saving_per_month_usd`) and repeat every entry in `notes`.
4. **Offer next steps**: a quote for a 1-year commitment on the suggested instances (via
   `compare_instances` and `build_quote`), or a talk with their account manager.

## Rules

- Never invent or extrapolate figures that did not come from the tools.
- Amounts are in USD. Mention `data_fetched_at` if the user asks how fresh the data is.
- Suggestions change nothing in their cloud accounts; buying a commitment goes through the
  account manager (see the `cloud-quote` skill for `request_purchase`).
- Reply in the user's language.
