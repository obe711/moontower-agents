---
name: Debugging
assignee: null
project: adapter-benchmark
---

# Task: Diagnose a Production Error

Given the following error log and source code, identify the root cause and provide a fix.

## Error log

```
2026-04-07T14:32:15.003Z ERROR [RequestHandler] Unhandled exception in /api/users/search
TypeError: Cannot read properties of undefined (reading 'toLowerCase')
    at UserService.searchUsers (/app/src/user-service.ts:42:38)
    at RequestHandler.handle (/app/src/handler.ts:18:29)
    at process.processTicksAndRejections (node:internal/process/task_queues:95:5)

Request context:
  Method: GET
  Path: /api/users/search
  Query: { q: "john", fields: "name,email,department" }

2026-04-07T14:32:15.005Z WARN [RequestHandler] Response: 500 Internal Server Error
2026-04-07T14:32:16.201Z ERROR [RequestHandler] Unhandled exception in /api/users/search
TypeError: Cannot read properties of undefined (reading 'toLowerCase')
    at UserService.searchUsers (/app/src/user-service.ts:42:38)
    at RequestHandler.handle (/app/src/handler.ts:18:29)

Request context:
  Method: GET
  Path: /api/users/search
  Query: { q: "doe", fields: "name,email,phone" }
```

## Source code

```typescript
// user-service.ts
interface User {
  id: string;
  name: string;
  email: string;
  department: string;
  phone?: string;
  bio?: string;
}

const SEARCHABLE_FIELDS = ['name', 'email', 'department', 'bio'] as const;
type SearchableField = typeof SEARCHABLE_FIELDS[number];

export class UserService {
  private users: User[] = [
    { id: '1', name: 'John Doe', email: 'john@example.com', department: 'Engineering' },
    { id: '2', name: 'Jane Smith', email: 'jane@example.com', department: 'Marketing', bio: 'Marketing lead' },
    { id: '3', name: 'Bob Wilson', email: 'bob@example.com', department: 'Engineering', phone: '+1234567890' },
  ];

  searchUsers(query: string, fields: string[]): User[] {
    const searchFields = fields.length > 0 ? fields : [...SEARCHABLE_FIELDS];
    const lowerQuery = query.toLowerCase();

    return this.users.filter(user => {
      return searchFields.some(field => {
        const value = user[field as keyof User];      // line 40
        return value.toLowerCase().includes(lowerQuery); // line 42
      });
    });
  }
}
```

## Expected analysis

1. **Root cause**: The `fields` parameter includes fields like `phone` which are optional on the `User` interface. When a user doesn't have that field, `user['phone']` returns `undefined`, and calling `.toLowerCase()` on `undefined` throws.
2. **Contributing factor**: The code doesn't validate that requested fields are in `SEARCHABLE_FIELDS`, so arbitrary fields like `phone` are allowed even though they may be undefined.
3. **Fix**: Add a null/undefined check before calling `.toLowerCase()` and/or validate fields against `SEARCHABLE_FIELDS`.

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| Root cause correctly identified | 35% |
| Error trace correctly interpreted | 15% |
| Fix is correct and complete | 25% |
| Contributing factors identified | 15% |
| Explanation is clear and logical | 10% |
