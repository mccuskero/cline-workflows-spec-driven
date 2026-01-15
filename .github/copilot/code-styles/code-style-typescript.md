# TypeScript Code Style Guide

## File Header

All TypeScript files must include the standard header template. See `.clinerules/templates/header-typescript.ts`.

## Naming Conventions

### Variables and Functions
- Use `camelCase` for variables, functions, and methods
- Use descriptive names that convey intent
- Prefix boolean variables with `is`, `has`, `can`, `should`

```typescript
// Good
const userName: string = 'John';
const isActive: boolean = true;
function calculateTotal(items: Item[]): number { }
function getUserById(id: string): User | null { }

// Bad
const user_name = 'John';
const active = true;
function calc(i: any) { }
```

### Constants
- Use `UPPER_SNAKE_CASE` for true constants
- Use `camelCase` for const references

```typescript
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = 'https://api.example.com';

const userService = new UserService();
```

### Types and Interfaces
- Use `PascalCase` for types, interfaces, classes, and enums
- Prefix interfaces with `I` only when necessary to distinguish from classes
- Prefer `interface` for object shapes, `type` for unions/intersections

```typescript
// Interfaces
interface User {
  id: string;
  name: string;
  email: string;
}

interface UserRepository {
  findById(id: string): Promise<User | null>;
  save(user: User): Promise<void>;
}

// Types
type UserRole = 'admin' | 'user' | 'guest';
type AsyncResult<T> = Promise<Result<T, Error>>;

// Classes
class UserService { }
class HttpClient { }

// Enums
enum Status {
  Active = 'active',
  Inactive = 'inactive',
  Pending = 'pending',
}
```

### Generics
- Use descriptive names for generics when meaning isn't obvious
- Single letter (`T`, `K`, `V`) acceptable for simple cases

```typescript
// Simple - single letter OK
function identity<T>(value: T): T { }
function mapObject<K extends string, V>(obj: Record<K, V>): void { }

// Complex - use descriptive names
interface Repository<TEntity, TKey> {
  findById(id: TKey): Promise<TEntity | null>;
  save(entity: TEntity): Promise<void>;
}
```

### Files
- Use `kebab-case` for file names
- Match file name to primary export

```
user-service.ts
http-client.ts
user.interface.ts
user.types.ts
```

## Type Annotations

### When to Annotate
- Always annotate function parameters
- Annotate return types for public functions
- Let TypeScript infer for local variables when obvious

```typescript
// Good - explicit where needed
function processUser(user: User): ProcessedUser {
  const result = transform(user); // inference OK here
  return result;
}

// Bad - over-annotated
function processUser(user: User): ProcessedUser {
  const result: ProcessedUser = transform(user);
  return result;
}
```

### Avoid `any`
- Use `unknown` instead of `any` when type is truly unknown
- Use proper generics or union types
- If `any` is necessary, add a comment explaining why

```typescript
// Good
function parseJson(text: string): unknown {
  return JSON.parse(text);
}

function handleResponse<T>(response: Response): Promise<T> {
  return response.json();
}

// Bad
function parseJson(text: string): any {
  return JSON.parse(text);
}
```

### Strict Null Checks
- Always handle `null` and `undefined` explicitly
- Use optional chaining and nullish coalescing

```typescript
// Good
const userName = user?.name ?? 'Anonymous';

function getUser(id: string): User | null {
  return users.get(id) ?? null;
}

// Bad
function getUser(id: string): User {
  return users.get(id)!; // Avoid non-null assertion
}
```

## Interfaces vs Types

### Use Interfaces For
- Object shapes
- Class contracts
- Extendable definitions

```typescript
interface User {
  id: string;
  name: string;
}

interface AdminUser extends User {
  permissions: string[];
}

interface Comparable<T> {
  compareTo(other: T): number;
}
```

### Use Types For
- Union types
- Intersection types
- Mapped types
- Utility types

```typescript
type Status = 'active' | 'inactive' | 'pending';
type Result<T> = Success<T> | Failure;
type ReadonlyUser = Readonly<User>;
type UserKeys = keyof User;
```

## Functions

### Function Signatures
- Use arrow functions for callbacks
- Use regular functions for methods
- Specify return types for public APIs

```typescript
// Public function - explicit return type
function calculateTotal(items: Item[]): number {
  return items.reduce((sum, item) => sum + item.price, 0);
}

// Callback - arrow function
items.filter((item): item is ActiveItem => item.isActive);

// Method
class UserService {
  async findById(id: string): Promise<User | null> {
    return this.repository.findById(id);
  }
}
```

### Overloads
- Use function overloads for multiple signatures
- Order from most specific to least specific

```typescript
function createElement(tag: 'div'): HTMLDivElement;
function createElement(tag: 'span'): HTMLSpanElement;
function createElement(tag: string): HTMLElement;
function createElement(tag: string): HTMLElement {
  return document.createElement(tag);
}
```

## Classes

### Access Modifiers
- Use `private` for internal implementation
- Use `protected` for inheritance
- Use `public` explicitly for clarity (optional)
- Use `readonly` for immutable properties

```typescript
class UserService {
  private readonly repository: UserRepository;
  protected logger: Logger;

  constructor(repository: UserRepository, logger: Logger) {
    this.repository = repository;
    this.logger = logger;
  }

  public async findUser(id: string): Promise<User | null> {
    this.logger.debug(`Finding user: ${id}`);
    return this.repository.findById(id);
  }
}
```

### Parameter Properties
- Use parameter properties for simple constructors

```typescript
// Good - concise
class UserService {
  constructor(
    private readonly repository: UserRepository,
    private readonly logger: Logger,
  ) {}
}

// Equivalent to:
class UserService {
  private readonly repository: UserRepository;
  private readonly logger: Logger;

  constructor(repository: UserRepository, logger: Logger) {
    this.repository = repository;
    this.logger = logger;
  }
}
```

## Enums

### String Enums Preferred
- Use string enums for better debugging and serialization

```typescript
// Good - string enum
enum Status {
  Active = 'active',
  Inactive = 'inactive',
  Pending = 'pending',
}

// Avoid - numeric enum (unless needed)
enum Status {
  Active,
  Inactive,
  Pending,
}
```

### Const Enums
- Use `const enum` for performance when values are inlined

```typescript
const enum Direction {
  Up = 'UP',
  Down = 'DOWN',
  Left = 'LEFT',
  Right = 'RIGHT',
}
```

## Async/Await

### Return Types
- Always specify `Promise<T>` return type for async functions

```typescript
async function fetchUser(id: string): Promise<User> {
  const response = await api.get(`/users/${id}`);
  return response.data;
}
```

### Error Handling
- Use typed errors when possible
- Consider Result types for expected failures

```typescript
type Result<T, E = Error> =
  | { success: true; data: T }
  | { success: false; error: E };

async function fetchUser(id: string): Promise<Result<User>> {
  try {
    const user = await api.get(`/users/${id}`);
    return { success: true, data: user };
  } catch (error) {
    return { success: false, error: error as Error };
  }
}
```

## Modules

### Import Order
1. Node built-ins
2. External packages
3. Internal modules (using path aliases)
4. Relative imports
5. Type-only imports last

```typescript
// Node built-ins
import { readFile } from 'fs/promises';

// External packages
import express from 'express';
import { z } from 'zod';

// Internal modules
import { UserService } from '@/services/user-service';
import { config } from '@/config';

// Relative imports
import { helper } from './helper';

// Type-only imports
import type { User } from '@/types';
```

### Type-Only Imports
- Use `import type` for type-only imports

```typescript
import type { User, UserRole } from './types';
import { createUser } from './user-service';
```

## Documentation

### TSDoc Comments
- Use TSDoc for public APIs

```typescript
/**
 * Retrieves a user by their unique identifier.
 *
 * @param id - The user's unique identifier
 * @returns The user if found, null otherwise
 * @throws {ValidationError} If the id format is invalid
 *
 * @example
 * ```typescript
 * const user = await userService.findById('user-123');
 * if (user) {
 *   console.log(user.name);
 * }
 * ```
 */
async function findById(id: string): Promise<User | null> {
  // ...
}
```

## Testing

### Type Testing
- Test that types work as expected

```typescript
// Type assertions in tests
import { expectType } from 'tsd';

const user: User = createUser({ name: 'John' });
expectType<string>(user.id);
expectType<string>(user.name);
```

### Test File Naming
- `*.test.ts` or `*.spec.ts`

```
user-service.test.ts
user-service.spec.ts
```
