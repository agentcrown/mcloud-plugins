---
name: cloud-quote
description: Produce an indicative multi-cloud price quote for Singapore servers at the customer's reseller discount, and pass a purchase request to the account manager. Use when the user asks for a quote, a cost estimate for a set of servers, a monthly or yearly budget, a comparison of total cost for an architecture, or says they want to buy or order.
---

# Cloud quote

Uses the `mcloud` MCP server tools: `compare_instances`, `build_quote`, `request_purchase`.

## Workflow

1. **List the components** of the architecture (e.g. 2 x web, 1 x database, 1 x worker)
   with a size for each. If sizes are missing, use the `cloud-sizing` guidance and state
   assumptions.
2. **Get offer ids** with `compare_instances` for each size. Keep all components on one
   provider unless the user asks for multi-cloud; mixing providers adds egress cost.
3. **Call `build_quote`** with `items` and `months` (default 12). Each item takes
   `offer_id`, `quantity`, `term` (`on_demand` or `one_year`), `disk_gb` (SSD per
   instance) and `egress_gb_month` (internet traffic for that line). Ask for disk and
   traffic if they matter and are unknown; a quote without them understates the cost.
4. **Present the quote**:
   - Line items: component, provider, instance type, term, quantity, and list price,
     discount % and final monthly price
   - Monthly total, term total, savings versus list price
   - `valid_until` date
   - Every entry from the result's `notes`, verbatim
5. If `unknown_offer_ids` is not empty, re-run `compare_instances` rather than guessing.

## When the user wants to buy

`request_purchase` notifies a real account manager, so never call it on your own initiative
or speculatively ("shall I send this?" is not a yes).

1. The user must say they want to buy or order.
2. Confirm in one short message: the exact items (instance type, quantity, term, disk,
   traffic), the contact name, and how to reach them (email, phone, WhatsApp or Telegram).
   Ask for anything missing. Add timing or special requirements to `notes`.
3. After the user confirms, call `request_purchase` once, with the same `items` and `months`
   as the quote.
4. Tell the user the lead number and that their account manager will contact them within one
   business day. The final price is set in the contract.

Never invent prices that did not come from the tools. Reply in the user's language.
This server never creates cloud resources; ordering happens with the account manager.
