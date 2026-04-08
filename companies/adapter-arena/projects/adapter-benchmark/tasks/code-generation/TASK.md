---
name: Code Generation
assignee: null
project: adapter-benchmark
---

# Task: Implement a Rate Limiter

Write a TypeScript module that implements a token bucket rate limiter.

## Specification

Create a file `rate-limiter.ts` that exports a class `RateLimiter` with this interface:

```typescript
class RateLimiter {
  constructor(options: {
    maxTokens: number;      // bucket capacity
    refillRate: number;     // tokens added per second
    refillInterval?: number; // ms between refills (default: 1000)
  })

  tryConsume(tokens?: number): boolean  // attempt to consume tokens, return success
  getAvailableTokens(): number          // current token count
  reset(): void                         // reset to full capacity
}
```

### Behavioral requirements

- Bucket starts full (maxTokens)
- `tryConsume(n)` removes n tokens if available, returns true; otherwise returns false and removes nothing. Default n=1.
- Tokens refill at `refillRate` per `refillInterval` ms, never exceeding `maxTokens`
- Thread-safe is not required (single-threaded JS)
- No external dependencies

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| Correct interface match | 25% |
| Token consumption logic correct | 25% |
| Refill logic correct (time-based, capped) | 25% |
| Edge cases handled (0 tokens, negative, overflow) | 15% |
| Code quality (types, naming, structure) | 10% |
