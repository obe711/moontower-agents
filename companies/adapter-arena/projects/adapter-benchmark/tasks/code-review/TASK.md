---
name: Code Review
assignee: null
project: adapter-benchmark
---

# Task: Review an Authentication Module

Review the following code and provide actionable feedback. Identify bugs, security issues, performance problems, and style issues. Prioritize findings by severity.

## Code to review

```typescript
// auth.ts
import crypto from 'crypto';

const users: Map<string, { passwordHash: string; salt: string; role: string }> = new Map();
const sessions: Map<string, { userId: string; createdAt: number }> = new Map();

export function register(username: string, password: string, role: string = 'user') {
  if (users.has(username)) throw new Error('User exists');
  const salt = crypto.randomBytes(16).toString('hex');
  const hash = crypto.createHash('md5').update(password + salt).digest('hex');
  users.set(username, { passwordHash: hash, salt, role });
}

export function login(username: string, password: string): string {
  const user = users.get(username);
  if (!user) throw new Error('Invalid credentials');
  const hash = crypto.createHash('md5').update(password + user.salt).digest('hex');
  if (hash !== user.passwordHash) throw new Error('Invalid credentials');
  const sessionId = crypto.randomBytes(32).toString('hex');
  sessions.set(sessionId, { userId: username, createdAt: Date.now() });
  return sessionId;
}

export function authorize(sessionId: string, requiredRole: string): boolean {
  const session = sessions.get(sessionId);
  if (!session) return false;
  const user = users.get(session.userId);
  if (!user) return false;
  return user.role === requiredRole || user.role === 'admin';
}

export function logout(sessionId: string): void {
  sessions.delete(sessionId);
}
```

## Expected findings (minimum)

The reviewer should catch at least these issues:
1. **Critical**: MD5 is cryptographically broken -- should use bcrypt/scrypt/argon2
2. **High**: No session expiration -- sessions live forever
3. **High**: In-memory storage -- no persistence, lost on restart
4. **Medium**: No password complexity validation
5. **Medium**: No rate limiting on login attempts
6. **Low**: Role comparison is simplistic (no role hierarchy)

## Evaluation criteria

| Criterion | Weight |
|-----------|--------|
| Security issues identified (MD5, sessions) | 30% |
| Findings correctly prioritized by severity | 20% |
| Actionable fix suggestions provided | 20% |
| Non-security issues caught (persistence, validation) | 15% |
| Review is well-organized and professional | 15% |
