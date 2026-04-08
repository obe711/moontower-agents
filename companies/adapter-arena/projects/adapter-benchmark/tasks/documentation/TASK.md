---
name: Documentation
assignee: null
project: adapter-benchmark
---

# Task: Document an Event Emitter

Generate comprehensive API documentation for the following event emitter module. Include JSDoc comments in the code and a separate API reference document.

## Code to document

```typescript
// event-emitter.ts
type Listener<T = any> = (data: T) => void;

export class EventEmitter {
  private listeners: Map<string, Set<Listener>> = new Map();
  private onceListeners: Map<string, Set<Listener>> = new Map();

  on<T>(event: string, listener: Listener<T>): () => void {
    if (!this.listeners.has(event)) {
      this.listeners.set(event, new Set());
    }
    this.listeners.get(event)!.add(listener);
    return () => this.off(event, listener);
  }

  once<T>(event: string, listener: Listener<T>): () => void {
    if (!this.onceListeners.has(event)) {
      this.onceListeners.set(event, new Set());
    }
    this.onceListeners.get(event)!.add(listener);
    return () => this.onceListeners.get(event)?.delete(listener);
  }

  off(event: string, listener: Listener): void {
    this.listeners.get(event)?.delete(listener);
    this.onceListeners.get(event)?.delete(listener);
  }

  emit<T>(event: string, data: T): void {
    this.listeners.get(event)?.forEach(fn => fn(data));
    const once = this.onceListeners.get(event);
    if (once) {
      once.forEach(fn => fn(data));
      once.clear();
    }
  }

  removeAllListeners(event?: string): void {
    if (event) {
      this.listeners.delete(event);
      this.onceListeners.delete(event);
    } else {
      this.listeners.clear();
      this.onceListeners.clear();
    }
  }

  listenerCount(event: string): number {
    return (this.listeners.get(event)?.size ?? 0) +
           (this.onceListeners.get(event)?.size ?? 0);
  }
}
```

## Expected output

1. The code above with complete JSDoc comments on every public method
2. A separate API reference document with:
   - Overview section
   - Constructor docs
   - Method reference (each method: signature, description, parameters, return value, example)
   - Usage examples showing common patterns

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| All public methods documented | 20% |
| JSDoc comments are accurate and complete | 20% |
| API reference is well-structured and navigable | 20% |
| Code examples are correct and useful | 20% |
| Parameter/return types correctly described | 10% |
| Edge cases and caveats noted | 10% |
