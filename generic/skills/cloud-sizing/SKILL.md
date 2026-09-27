---
name: cloud-sizing
description: Size and compare cloud servers in Singapore across AWS, Google Cloud, Azure, Alibaba Cloud, Tencent Cloud and Huawei Cloud. Use when the user asks which cloud or instance to pick, how much a server costs in Singapore, or wants a price comparison between cloud providers.
---

# Cloud sizing (Singapore, multi-cloud)

Uses the `mcloud` MCP server tools: `list_clouds`, `compare_instances`.

## Workflow

1. **Pin down the requirement.** You need at least vCPU and memory. If the user only
   describes a workload, estimate conservatively and state your assumption:
   - Small website / API, low traffic: 2 vCPU, 4-8 GiB
   - Typical business app or MySQL/PostgreSQL for a small team: 4 vCPU, 16 GiB
   - Busy database, Java services, CI runners: 8 vCPU, 32 GiB
   Ask only if the budget or a required provider is unclear and it would change the answer.
2. **Call `compare_instances`** with `min_vcpu`, `min_memory_gib`, plus `category`
   (general / compute / memory), `arch`, `providers` or `max_monthly_usd` when the user
   gave them. Use `term: "one_year"` when the workload runs all year.
   Burstable types (AWS t*, Azure B*) are hidden by default; set `include_burstable`
   only for light, spiky loads such as small test or dev servers.
3. **Present a short table**: provider, instance type, vCPU/memory, and for each price
   shown the list price, discount % and final monthly price. Show both on-demand and
   1-year when both exist: the 1-year saving is usually the strongest argument.
   Recommend one option and say why in one sentence (price, ecosystem fit, services the
   user already uses on that cloud, China connectivity for Alibaba/Tencent/Huawei).
4. **Always state** that these are compute-only Linux prices, excluding storage,
   bandwidth, public IPs and taxes.
5. If `providers_without_data` or `stale_providers` is not empty, say which clouds are
   missing or out of date instead of implying they were compared.

Reply in the user's language. Offer to turn the choice into a quote (see the `cloud-quote` skill).
