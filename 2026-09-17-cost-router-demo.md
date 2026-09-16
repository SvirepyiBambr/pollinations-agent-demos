# cost-router — live demo (quest #15017)

Deployed agent: `e8c40381-a80e-492c-a33e-635044f95c16`
Callable model: `SvirepyiBambr/cost-router`
Date: 2026-09-17 (~02:3x MSK)

Three requests with different complexity, routed to three different models
(nvidia/nemotron-3.5-lightning → x-ai/grok-4.3 → x-ai/grok-4.20).
Verified via /v1/responses router_trace (reason includes tier, input score,
price, health and fresh p50):

## LIGHT (/v1/responses)

prompt: Hi there, quick check 1789601893: what is 2+2?

router_trace: {"model": "nvidia/nemotron-3.5-lightning", "reason": "LIGHT tier (input score 0.4) · picked nvidia/nemotron-3.5-lightning at $0.25/1M tok · health 99.4% · fresh p50 1800ms"}

## STANDARD (/v1/responses)

prompt: Review this TypeScript snippet and fix the bugs:
```ts
function debounce(fn: any, ms: number) {
  let t: any;
  return (...args: any[]) => { clearTimeout(t); t 

router_trace: {"model": "x-ai/grok-4.3", "reason": "STANDARD tier (input score 2.1) · picked x-ai/grok-4.3 at $2.81/1M tok · health 97.7% · fresh p50 9404ms"}

## DEEP (/v1/responses)

prompt: Design a distributed rate limiter for a multi-region API gateway. Compare token bucket, sliding window log, and GCRA approaches in detail; prove the GCRA admiss

router_trace: {"model": "x-ai/grok-4.20", "reason": "DEEP tier (input score 3.7) · picked x-ai/grok-4.20 at $6.00/1M tok · health 98.9% · fresh p50 981ms"}

## LIGHT (chat/completions)

body.model: accounts/fireworks/models/***
router_trace: "(none)"

## STANDARD (chat/completions)

body.model: accounts/fireworks/models/***
router_trace: "(none)"

## DEEP (chat/completions)

body.model: accounts/fireworks/models/***
router_trace: "(none)"
