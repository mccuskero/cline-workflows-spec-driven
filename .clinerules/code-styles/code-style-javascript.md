# JavaScript Code Style Guide

## File Header

All JavaScript files must include the standard header template. See `.clinerules/templates/header-javascript.js`.

## Naming Conventions

### Variables and Functions
- Use `camelCase` for variables and functions
- Use descriptive names that convey intent
- Prefix boolean variables with `is`, `has`, `can`, `should`

```javascript
// Good
const userName = 'John';
const isActive = true;
const hasPermission = false;
function calculateTotal(items) { }
function getUserById(id) { }

// Bad
const user_name = 'John';
const active = true;
function calc(i) { }
```

### Constants
- Use `UPPER_SNAKE_CASE` for true constants
- Use `camelCase` for const references that could conceptually change

```javascript
// True constants
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = 'https://api.example.com';

// Const references
const userService = new UserService();
const config = loadConfig();
```

### Classes and Constructors
- Use `PascalCase` for classes and constructor functions

```javascript
class UserAccount { }
class HttpRequestHandler { }
function DataProcessor() { }
```

### Files and Modules
- Use `kebab-case` for file names
- One class/component per file

```
user-service.js
http-client.js
data-processor.js
```

## Formatting

### Indentation
- Use 2 spaces for indentation
- No tabs

### Line Length
- Maximum 100 characters per line
- Break long lines at logical points

### Braces
- Opening brace on same line
- Always use braces for control structures

```javascript
// Good
if (condition) {
  doSomething();
}

function example() {
  return value;
}

// Bad
if (condition)
  doSomething();

function example()
{
  return value;
}
```

### Semicolons
- Always use semicolons

### Quotes
- Prefer single quotes for strings
- Use template literals for interpolation

```javascript
const name = 'John';
const greeting = `Hello, ${name}!`;
```

## Functions

### Arrow Functions
- Prefer arrow functions for callbacks and short functions
- Use regular functions for methods and constructors

```javascript
// Callbacks
items.map(item => item.value);
items.filter(item => item.isActive);

// Methods
const service = {
  getData() {
    return this.data;
  }
};
```

### Parameters
- Maximum 3-4 parameters; use options object for more
- Use default parameters instead of conditionals

```javascript
// Good
function createUser({ name, email, role = 'user', active = true }) {
  // ...
}

// Bad
function createUser(name, email, role, active, department, manager) {
  // ...
}
```

### Return Early
- Return early to avoid deep nesting

```javascript
// Good
function processUser(user) {
  if (!user) {
    return null;
  }

  if (!user.isActive) {
    return { error: 'User inactive' };
  }

  return processActiveUser(user);
}

// Bad
function processUser(user) {
  if (user) {
    if (user.isActive) {
      return processActiveUser(user);
    } else {
      return { error: 'User inactive' };
    }
  } else {
    return null;
  }
}
```

## Objects and Arrays

### Object Shorthand
- Use property shorthand when possible

```javascript
const name = 'John';
const age = 30;

// Good
const user = { name, age };

// Bad
const user = { name: name, age: age };
```

### Destructuring
- Use destructuring for object and array access

```javascript
// Good
const { name, email } = user;
const [first, second] = items;

// Bad
const name = user.name;
const email = user.email;
```

### Spread Operator
- Use spread for copying and merging

```javascript
const newArray = [...oldArray, newItem];
const newObject = { ...oldObject, newProp: value };
```

## Async/Await

### Prefer async/await over Promises
```javascript
// Good
async function fetchData() {
  try {
    const response = await api.get('/data');
    return response.data;
  } catch (error) {
    handleError(error);
  }
}

// Avoid
function fetchData() {
  return api.get('/data')
    .then(response => response.data)
    .catch(error => handleError(error));
}
```

### Error Handling
- Always handle errors in async functions
- Use try/catch blocks

## Modules

### Import Order
1. External libraries
2. Internal modules
3. Relative imports
4. Styles/assets

```javascript
// External
import express from 'express';
import lodash from 'lodash';

// Internal
import { UserService } from '@/services/user-service';
import { config } from '@/config';

// Relative
import { helper } from './helper';
import { constants } from '../constants';
```

### Export Style
- Prefer named exports over default exports
- Export at declaration when possible

```javascript
// Good
export function processData() { }
export const CONFIG = { };

// Acceptable for main module export
export default class UserService { }
```

## Comments

### When to Comment
- Explain "why", not "what"
- Document complex algorithms
- Note workarounds and their reasons

```javascript
// Good - explains why
// Using setTimeout to allow DOM to update before measuring
setTimeout(() => measureElement(), 0);

// Bad - explains what (obvious from code)
// Loop through users
users.forEach(user => { });
```

### JSDoc
- Use JSDoc for public APIs and complex functions

```javascript
/**
 * Calculates the total price including tax.
 * @param {number} subtotal - The pre-tax amount
 * @param {number} taxRate - Tax rate as decimal (e.g., 0.08 for 8%)
 * @returns {number} The total price with tax
 */
function calculateTotal(subtotal, taxRate) {
  return subtotal * (1 + taxRate);
}
```

## Error Handling

### Custom Errors
- Create custom error classes for specific error types

```javascript
class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.name = 'ValidationError';
    this.field = field;
  }
}
```

### Never Swallow Errors
```javascript
// Bad
try {
  riskyOperation();
} catch (e) {
  // silent fail
}

// Good
try {
  riskyOperation();
} catch (error) {
  logger.error('Operation failed:', error);
  throw error; // or handle appropriately
}
```

## Testing

### Test File Naming
- `*.test.js` or `*.spec.js`
- Place next to source file or in `__tests__` directory

### Test Structure
```javascript
describe('UserService', () => {
  describe('createUser', () => {
    it('should create a user with valid data', () => {
      // Arrange
      const userData = { name: 'John', email: 'john@example.com' };

      // Act
      const result = userService.createUser(userData);

      // Assert
      expect(result.name).toBe('John');
    });

    it('should throw ValidationError for invalid email', () => {
      // ...
    });
  });
});
```
