---
name: Bug Fixing
assignee: null
project: adapter-benchmark
---

# Task: Fix the Shopping Cart

The following shopping cart module has 3 bugs. Find and fix all of them. Explain each bug.

## Buggy code

```typescript
// shopping-cart.ts
interface CartItem {
  id: string;
  name: string;
  price: number;
  quantity: number;
}

class ShoppingCart {
  private items: CartItem[] = [];

  addItem(item: Omit<CartItem, 'quantity'>, quantity: number = 1): void {
    const existing = this.items.find(i => i.id === item.id);
    if (existing) {
      existing.quantity = quantity; // BUG 1: should += not =
    } else {
      this.items.push({ ...item, quantity });
    }
  }

  removeItem(id: string): void {
    this.items = this.items.filter(i => i.id === id); // BUG 2: should be !==
  }

  getTotal(): number {
    return this.items.reduce((sum, item) => sum + item.price, 0); // BUG 3: should multiply by quantity
  }

  getItems(): CartItem[] {
    return this.items;
  }
}

export { ShoppingCart, CartItem };
```

## Expected output

Provide the corrected code and for each bug explain:
1. What line the bug is on
2. What the bug is
3. What the fix is

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| All 3 bugs identified | 40% |
| All 3 bugs correctly fixed | 30% |
| Clear explanation of each bug | 20% |
| No regressions introduced | 10% |
