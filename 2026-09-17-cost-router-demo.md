# cost-router — live demo (quest #15017)

Deployed agent: `e8c40381-a80e-492c-a33e-635044f95c16`
Callable model: `SvirepyiBambr/cost-router`
Date: 2026-09-17 (~02:2x MSK)

Three requests with different complexity, routed to different tiers.
`chat/completions` answers (top-level `model` field shows the actual inner model;
the full `X-Router-Reason` is visible on `/v1/responses` via `router_trace`).

## LIGHT

prompt: Hi there, quick check 1789601420: what is 2+2?

body.model: accounts/fireworks/models/***
content: Hi! 2 + 2 = 4.

## STANDARD

prompt: Review this TypeScript snippet and fix the bugs:
```ts
function debounce(fn: any, ms: number) {
  let t: any;
  return (...args: any[]) => { clearTimeout(t); t 

body.model: accounts/fireworks/models/***
content: ## Bug Analysis

The provided `debounce` function has a functional bug related to the JavaScript `this` context.

### The Problem

The retur

## DEEP

prompt: Design a distributed rate limiter for a multi-region API gateway. Compare token bucket, sliding window log, and GCRA approaches in detail; prove the GCRA admiss

body.model: accounts/fireworks/models/***
content: # Distributed Rate Limiter Design for Multi-Region API Gateway  
**Ticket:** 1789601420  

---

## 1. Overview & Design Goals
A distributed 

## /v1/responses trace check

body.model: accounts/fireworks/models/***
router_trace: {"model": "nvidia/nemotron-3.5-lightning", "reason": "LIGHT tier (input score 0.1) · picked nvidia/nemotron-3.5-lightning at $0.25/1M tok · health 99.4% · fresh p50 1661ms"}
