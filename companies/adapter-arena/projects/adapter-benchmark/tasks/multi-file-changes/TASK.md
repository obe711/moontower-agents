---
name: Multi-file Changes
assignee: null
project: adapter-benchmark
---

# Task: Add a Discount System to an E-commerce Module

Add a discount/coupon system to the following e-commerce module. This requires coordinated changes across all 3 files.

## Existing code

### types.ts

```typescript
export interface Product {
  id: string;
  name: string;
  price: number;
}

export interface OrderItem {
  product: Product;
  quantity: number;
}

export interface Order {
  id: string;
  items: OrderItem[];
  total: number;
  createdAt: Date;
}
```

### cart.ts

```typescript
import { Product, OrderItem } from './types';

export class Cart {
  private items: Map<string, OrderItem> = new Map();

  add(product: Product, quantity: number = 1): void {
    const existing = this.items.get(product.id);
    if (existing) {
      existing.quantity += quantity;
    } else {
      this.items.set(product.id, { product, quantity });
    }
  }

  remove(productId: string): void {
    this.items.delete(productId);
  }

  getTotal(): number {
    let total = 0;
    for (const item of this.items.values()) {
      total += item.product.price * item.quantity;
    }
    return total;
  }

  getItems(): OrderItem[] {
    return Array.from(this.items.values());
  }

  clear(): void {
    this.items.clear();
  }
}
```

### order-service.ts

```typescript
import { Order } from './types';
import { Cart } from './cart';
import { randomUUID } from 'crypto';

export class OrderService {
  private orders: Order[] = [];

  createOrder(cart: Cart): Order {
    const items = cart.getItems();
    if (items.length === 0) throw new Error('Cart is empty');
    const order: Order = {
      id: randomUUID(),
      items,
      total: cart.getTotal(),
      createdAt: new Date(),
    };
    this.orders.push(order);
    cart.clear();
    return order;
  }

  getOrder(id: string): Order | undefined {
    return this.orders.find(o => o.id === id);
  }
}
```

## Requirements

1. Add a `Discount` interface to `types.ts` with: `code: string`, `type: 'percentage' | 'fixed'`, `value: number`, `minOrderAmount?: number`
2. Add an `appliedDiscount?: Discount` field to the `Order` interface
3. Modify `Cart` to accept and apply a discount via `applyDiscount(discount: Discount): void` and `removeDiscount(): void`. The discount should affect `getTotal()`.
4. Modify `OrderService.createOrder` to include the applied discount in the created order
5. Handle edge cases: discount doesn't reduce below 0, minOrderAmount is checked

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| All 3 files modified correctly | 25% |
| Discount interface matches spec | 15% |
| Cart discount logic correct (percentage and fixed) | 20% |
| OrderService passes discount through | 15% |
| Edge cases handled (min amount, negative total) | 15% |
| Changes are consistent across files | 10% |
