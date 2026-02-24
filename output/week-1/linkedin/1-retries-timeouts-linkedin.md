# Production AI Reliability: Retries, Timeouts, and Circuit Breakers - LinkedIn Post

## Post

We processed over 500B tokens across 125M daily requests through our AI Gateway at Portkey last year. 

Here are the 3 reliability patterns that separate resilient enterprise AI apps from fragile Saturday-night prototypes:

If you are building an AI app with a direct connection to a single LLM provider, your entire application is at the mercy of their uptime. And let's face it—APIs timeout, networks fail, and rate limits trigger 429 errors every day. 

Here's what production-ready AI infrastructure looks like:

1️⃣ Automatic Retries with Exponential Backoff
→ If OpenAI fails due to a network blip or rate limit, your app shouldn't immediately crash.
→ The AI Gateway catches the error, waits a strategically increasing amount of time (e.g., 2s, 4s, 8s), and retries.
→ 90% of transient API errors resolve themselves on the second or third attempt.

2️⃣ Request Timeouts
→ LLMs are notorious for hanging indefinitely during generation, eating up your UI latency budget.
→ Enforce strict gateway timeouts. If an API doesn't respond in 15 seconds, terminate the connection and automatically retry or fallback to a faster, smaller model (like Claude Haiku).

3️⃣ Circuit Breakers
→ If Anthropic is down and returning 500 errors on 10 consecutive requests, stop hammering them.
→ A circuit breaker trips, instantly failing fast or routing to OpenAI without wasting latency or triggering abuse limits.

The key insight?

These patterns belong at the infrastructure layer, not in your application code. Wrapping every single API call in Python `try/except` blocks with custom `time.sleep()` logic is a maintenance nightmare.

An AI Gateway handles all of this automatically with a single JSON configuration. Zero code rewrites. Zero downtime.

Key takeaways:
• Start with retries — they solve the vast majority of rate limit and network errors.
• Set strict timeouts — your users won't stare at a loading spinner forever.
• Put these guardrails at the gateway layer, not scattered across your microservices.

What's the #1 reliability challenge you face when scaling LLMs in production?

---

## First Comment

Link: https://portkey.ai/docs/product/ai-gateway/reliability
Read our docs on implementing Retries, Timeouts, and Fallbacks with zero code changes.

Open-source gateway (17K+ stars):
https://github.com/Portkey-AI/gateway

---

## Carousel Slides (optional)

Slide 1: "3 Reliability Patterns for Production AI Apps"
Slide 2: "Pattern 1: Retries with Exponential Backoff" (diagram showing 429 error -> wait -> success)
Slide 3: "Pattern 2: Request Timeouts" (diagram showing slow response -> terminate -> fallback to fast model)
Slide 4: "Pattern 3: Circuit Breakers" (flow diagram illustrating tripped circuit protecting the app)
Slide 5: "The Architecture" (AI Gateway handling all this invisibly between your app and the provider)
Slide 6: "Configure in 2 minutes → link in comments"

---

## Posting Notes

- Best times: 8 AM or 12 PM IST (Tuesday-Thursday)
- Hashtags in comment: #AI #LLM #ProductionAI #AIInfrastructure #SRE #Reliability
- Reply to comments within first 2 hours
- Tag CTOs, AI engineers, and SRE leads when relevant
