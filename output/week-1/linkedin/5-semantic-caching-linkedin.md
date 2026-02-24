# Save 30-40% on LLM Costs with Semantic Caching - LinkedIn Post

## Post

We tracked $500K in daily LLM spending across Portkey's AI Gateway last month, and we noticed something that hurts to watch:

Engineering teams are paying OpenAI and Anthropic thousands of dollars to generate the exact identical tokens over and over again.

In a typical enterprise RAG app or e-commerce chatbot, up to 40% of queries are variations of the same 50 questions:
- "What's the refund policy?"
- "How do I return this?"
- "Can I get my money back?"

If your app hits the LLM provider API for every single one of these, you are lighting money on fire. 

Here is the modern optimization strategy: Semantic Caching.

1️⃣ Vector-Based Intelligence
→ Simple caching only works if strings perfectly match. Semantic caching uses high-speed vector embeddings to calculate the mathematical meaning behind a query.
→ If the semantic similarity of the new prompt matches a cached prompt by 95%, the Gateway intercepts it.

2️⃣ 100% Cost Savings on Cache Hits
→ By intercepting the request at the edge, you never touch the expensive LLM. A cached query costs you $0 in API credits. 
→ Our customers typically see their monthly AI bills drop by 30-40% within 48 hours of enabling this.

3️⃣ Millisecond Latency
→ Because the gateway doesn't wait on generative token generation, the response is beamed back to the user in less than 50 milliseconds. The UI feels instantaneous.

The best part? Because we built this into Portkey's open-source foundational layer, enabling Semantic Caching takes exactly 3 lines of JSON configuration—no need to stand up your own Redis or Milvus instances.

With 125M daily requests and a $15M Series A validating our architecture, Portkey is built to ensure you never pay twice for the same LLM inference.

Key takeaways:
• Generating the same response twice is an architectural anti-pattern.
• Implement Semantic (not just Simple) caching to handle human nuance and typos.
• Put your cache at the Gateway layer, decoupled from your core Python/JS application code.

What percentage of your LLM traffic do you think is redundant?

---

## First Comment

Link: https://portkey.ai/docs/product/ai-gateway/cache-simple-and-semantic
Read our step-by-step coding blog on implementing Semantic Caching in 3 minutes.

Open-source gateway (17K+ stars):
https://github.com/Portkey-AI/gateway

---

## Carousel Slides (optional)

Slide 1: "Stop Paying Twice for the Same Prompt"
Slide 2: "User 1 vs User 2" (Graphic showing the 3 differently worded refund policy questions)
Slide 3: "The Simple Cache Mismatch" (Diagram showing simple cache failing)
Slide 4: "Semantic Caching via Vector Math" (Diagram showing the 95% similarity match -> Cache Hit)
Slide 5: "The Results" (-40% Cost, 50ms Latency)
Slide 6: "Enable inside Portkey in 3 lines of config → link in comments"

---

## Posting Notes

- Best times: 8 AM or 12 PM IST (Tuesday-Thursday)
- Hashtags in comment: #AI #LLM #ProductionAI #AIInfrastructure #FinOps #Caching
- Reply to comments within first 2 hours
- Tag FinOps leads, CTOs, and Backend engineers handling latency
