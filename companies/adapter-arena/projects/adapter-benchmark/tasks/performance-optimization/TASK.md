---
name: Performance Optimization
assignee: null
project: adapter-benchmark
---

# Task: Optimize a Slow Search Function

The following search function is too slow for large datasets. Optimize it without changing its public API or return values.

## Slow code

```typescript
// search.ts
interface Product {
  id: string;
  name: string;
  category: string;
  price: number;
  tags: string[];
}

export function searchProducts(
  products: Product[],
  filters: {
    query?: string;
    category?: string;
    minPrice?: number;
    maxPrice?: number;
    tags?: string[];
  },
  sortBy: 'price' | 'name' = 'name',
  page: number = 1,
  pageSize: number = 20
): { results: Product[]; total: number } {
  // Filter
  let filtered = products;

  if (filters.query) {
    filtered = filtered.filter(p =>
      p.name.toLowerCase().includes(filters.query!.toLowerCase()) ||
      p.tags.some(t => t.toLowerCase().includes(filters.query!.toLowerCase()))
    );
  }

  if (filters.category) {
    filtered = filtered.filter(p => p.category === filters.category);
  }

  if (filters.minPrice !== undefined) {
    filtered = filtered.filter(p => p.price >= filters.minPrice!);
  }

  if (filters.maxPrice !== undefined) {
    filtered = filtered.filter(p => p.price <= filters.maxPrice!);
  }

  if (filters.tags && filters.tags.length > 0) {
    filtered = filtered.filter(p =>
      filters.tags!.every(tag =>
        p.tags.some(pt => pt.toLowerCase() === tag.toLowerCase())
      )
    );
  }

  // Sort
  const sorted = [...filtered].sort((a, b) => {
    if (sortBy === 'price') return a.price - b.price;
    return a.name.localeCompare(b.name);
  });

  // Paginate
  const start = (page - 1) * pageSize;
  const results = sorted.slice(start, start + pageSize);

  return { results, total: filtered.length };
}
```

## Performance issues to address

- Multiple separate filter passes over the array (should be single pass)
- `toLowerCase()` called repeatedly on the same query/tags (should precompute)
- Full sort even though only one page is needed
- No early termination

## Expected optimizations

1. Precompute lowercased query and filter tags once
2. Single-pass filtering (combine all filter conditions)
3. Avoid full sort when possible (partial sort or only sort the needed page)
4. Consider building index structures for repeated searches on the same dataset

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| Precomputation of repeated operations | 25% |
| Single-pass filtering implemented | 25% |
| Sort optimization (partial sort or equivalent) | 20% |
| Public API preserved (same inputs/outputs) | 15% |
| Code remains readable after optimization | 15% |
