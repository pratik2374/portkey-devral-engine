# How We Saved Customers Millions After Raising Our $15M Series A - LinkedIn Post

## Post

We tracked $500K in daily LLM spending across our AI Gateway platform this month. 

The #1 cost driver wasn't expensive models like GPT-4o or Claude 3.5 Opus. 
It was redundant API calls and zero visibility.

When engineering teams roll out GenAI features, they typically have massive blind spots. They can see the aggregate API bill at the end of the month, but they can't answer:
"Which specific user or customer is driving 80% of these token costs?"

This is exactly why we raised our $15M Series A: to scale the unified control plane that brings sanity to production AI infrastructure. At 125M daily requests, we've seen every anti-pattern. Here's how the best teams optimize:

1️⃣ Metadata Tagging
→ Stop treating the OpenAI API like a black box.
→ Tag your requests with `_tenant_id` at the gateway layer.
→ Portkey's dashboards instantly show you your exact profit margins per customer.

2️⃣ Budget Caps & Rate Limits
→ Do not let a runaway scripting error bankupt your API credits.
→ Set strict token and cost budgets per user or per API key directly in Portkey. 
→ When a user hits $5 in generation costs, automatically block further requests.

3️⃣ Semantic Caching
→ You are likely paying to generate the exact same "Welcome message" thousands of times a day.
→ Enable Gateway-level Semantic Caching. If an LLM request mathematically matches a previous request's vector space by 95%, Portkey returns the cached result in milliseconds.
→ Typical savings: 30-40% on API costs.

The true cost of unoptimized LLM usage isn't just the API bill; it's the latency, the rate limit bottlenecks, and the engineering time spent writing custom dashboards.

Key takeaways:
• Observability must be granular; if you can't trace a cost to a user, you're flying blind.
• Preventative budget caps are mandatory in production.
• Caching belongs at the infrastructure layer, not the application layer.

What was the most surprising API cost spike your team has experienced?

---

## First Comment

Link: https://portkey.ai/docs/product/observability/custom-metadata
Read the docs on how to implement metadata tagging and budget caps with zero infrastructure work.

Open-source gateway (17K+ stars):
https://github.com/Portkey-AI/gateway

---

## Carousel Slides (optional)

Slide 1: "The True Cost of Unoptimized LLMs" (graphic showing API bill vs custom engineering cost)
Slide 2: "Step 1: Tag Everything" (code block showing metadata injection)
Slide 3: "Result: Granular Cost Tracking" (dashboard screenshot showing cost segmented by user)
Slide 4: "Step 2: Budget Caps" (diagram: User hits $10 limit -> Gateway blocks request)
Slide 5: "Step 3: Semantic Caching" (before/after cost reduction metric)
Slide 6: "Built for Scale" (125M requests, $15M Series A, 500B tokens)

---

## Posting Notes

- Best times: 8 AM or 12 PM IST (Tuesday-Thursday)
- Hashtags in comment: #AI #LLM #ProductionAI #AIInfrastructure #FinOps #SeriesA
- Reply to comments within first 2 hours
- Tag FinOps leads, CTOs, and AI engineers
