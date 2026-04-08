---
name: Architecture
assignee: null
project: adapter-benchmark
---

# Task: Design a URL Shortener Service

Design the architecture for a URL shortener service (like bit.ly). Produce a design document, not code.

## Requirements

- Shorten long URLs to short codes (e.g., `https://short.ly/abc123`)
- Redirect short URLs to the original URL
- Track click analytics (count, timestamp, referrer, geo)
- Support custom short codes
- Handle 10,000 redirects/second at peak
- URLs expire after a configurable TTL (default: 1 year)
- REST API for CRUD operations

## Expected deliverable

A design document covering:

1. **API Design**: REST endpoints with request/response schemas
2. **Data Model**: Database schema for URLs and analytics
3. **Short Code Generation**: Algorithm for generating unique codes (length, charset, collision handling)
4. **System Architecture**: Components, data flow, caching strategy
5. **Scaling Considerations**: How to handle 10k redirects/sec (caching, read replicas, CDN)
6. **Trade-offs**: Decisions made and alternatives considered

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| API design is complete and RESTful | 15% |
| Data model handles all requirements | 20% |
| Short code algorithm is sound (collision-free, efficient) | 15% |
| Architecture handles scale requirements | 20% |
| Caching strategy is practical | 15% |
| Trade-offs are identified and discussed | 15% |
