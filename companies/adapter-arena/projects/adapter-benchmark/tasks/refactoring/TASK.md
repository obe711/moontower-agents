---
name: Refactoring
assignee: null
project: adapter-benchmark
---

# Task: Refactor Utility Functions

Refactor the following utility module to improve structure, reduce duplication, and follow best practices. Do not change the public API (same exported function signatures and behavior).

## Code to refactor

```typescript
// utils.ts
export function formatDate(d: any): string {
  if (d === null || d === undefined) return '';
  let date: Date;
  if (typeof d === 'string') {
    date = new Date(d);
  } else if (typeof d === 'number') {
    date = new Date(d);
  } else {
    date = d;
  }
  const month = date.getMonth() + 1;
  const day = date.getDate();
  const year = date.getFullYear();
  return (month < 10 ? '0' + month : '' + month) + '/' + (day < 10 ? '0' + day : '' + day) + '/' + year;
}

export function formatCurrency(amount: any, currency: string): string {
  if (amount === null || amount === undefined) return '';
  if (currency === 'USD') {
    return '$' + (Math.round(amount * 100) / 100).toFixed(2);
  } else if (currency === 'EUR') {
    return '€' + (Math.round(amount * 100) / 100).toFixed(2);
  } else if (currency === 'GBP') {
    return '£' + (Math.round(amount * 100) / 100).toFixed(2);
  } else {
    return (Math.round(amount * 100) / 100).toFixed(2) + ' ' + currency;
  }
}

export function validateEmail(email: any): boolean {
  if (email === null || email === undefined) return false;
  if (typeof email !== 'string') return false;
  if (email.length === 0) return false;
  const parts = email.split('@');
  if (parts.length !== 2) return false;
  if (parts[0].length === 0) return false;
  if (parts[1].length === 0) return false;
  if (parts[1].indexOf('.') === -1) return false;
  return true;
}

export function slugify(text: any): string {
  if (text === null || text === undefined) return '';
  if (typeof text !== 'string') return '';
  let result = text.toLowerCase();
  result = result.replace(/[^a-z0-9\s-]/g, '');
  result = result.replace(/\s+/g, '-');
  result = result.replace(/-+/g, '-');
  result = result.replace(/^-|-$/g, '');
  return result;
}
```

## Expected improvements

- Extract common null/undefined guard pattern
- Use proper TypeScript types instead of `any`
- Use template literals or padStart instead of manual padding
- Use a currency symbol map instead of if/else chain
- Simplify and modernize syntax where possible

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| Public API preserved (same exports, same behavior) | 25% |
| Duplication reduced | 25% |
| Proper TypeScript types | 20% |
| Modern JS/TS idioms used | 15% |
| Readability improved | 15% |
