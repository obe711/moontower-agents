---
name: Test Writing
assignee: null
project: adapter-benchmark
---

# Task: Write Tests for a Stack Implementation

Write comprehensive tests for the following stack data structure. Use any popular testing framework (Jest, Vitest, Mocha). Cover happy paths, edge cases, and error conditions.

## Code under test

```typescript
// stack.ts
export class Stack<T> {
  private items: T[] = [];
  private readonly maxSize: number;

  constructor(maxSize: number = Infinity) {
    if (maxSize < 0) throw new RangeError('maxSize must be non-negative');
    this.maxSize = maxSize;
  }

  push(item: T): void {
    if (this.items.length >= this.maxSize) {
      throw new RangeError('Stack overflow: maximum size exceeded');
    }
    this.items.push(item);
  }

  pop(): T {
    if (this.items.length === 0) {
      throw new RangeError('Stack underflow: stack is empty');
    }
    return this.items.pop()!;
  }

  peek(): T {
    if (this.items.length === 0) {
      throw new RangeError('Stack underflow: stack is empty');
    }
    return this.items[this.items.length - 1];
  }

  get size(): number {
    return this.items.length;
  }

  get isEmpty(): boolean {
    return this.items.length === 0;
  }

  clear(): void {
    this.items = [];
  }

  toArray(): T[] {
    return [...this.items];
  }
}
```

## Expected test coverage

- Constructor: default maxSize, custom maxSize, negative maxSize throws
- push: single item, multiple items, overflow throws
- pop: returns last item, LIFO order, underflow throws
- peek: returns without removing, underflow throws
- size: tracks correctly after push/pop/clear
- isEmpty: true when empty, false when not
- clear: empties the stack
- toArray: returns copy (not reference), correct order
- Generic types: works with numbers, strings, objects

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| All public methods tested | 25% |
| Edge cases covered (empty, full, single element) | 25% |
| Error conditions tested (overflow, underflow) | 20% |
| Tests are well-organized and named | 15% |
| Tests actually pass against the implementation | 15% |
