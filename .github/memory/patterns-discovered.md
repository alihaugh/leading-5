# Patterns Discovered - Code Pattern Library

## Purpose

This file documents recurring code patterns discovered during development. These patterns help AI assistants provide context-aware suggestions that align with your project's specific approaches and conventions.

**Git Status**: COMMITTED - Accumulates knowledge over time.

---

## Pattern Template

```markdown
### [Pattern Name]

**Context**: [When/where this pattern applies]

**Problem**: [What issue this pattern solves]

**Solution**: [The approach that works]

**Example**:
```javascript
// Code example showing the pattern
```

**Related Files**:
- [file1.js] - [description]
- [file2.js] - [description]

**Discovered**: [Date or Session]

---
```

---

## Example Pattern

### Service Initialization - Array vs Null

**Context**: When initializing in-memory data stores or collections at module level in Node.js services

**Problem**: If you initialize a collection variable without a value or as `null`, attempts to use array methods (`.push()`, `.find()`, `.filter()`) will throw errors:
```
TypeError: Cannot read property 'push' of undefined
```

**Solution**: Always initialize collections as empty arrays at the module level, not as `undefined` or `null`:

```javascript
// ✅ GOOD: Initialize as empty array
let todos = [];
let nextId = 1;

// ❌ BAD: Uninitialized or null
let todos; // undefined
let todos = null; // null
```

**Benefits**:
- Array methods work immediately without null checks
- Clearer intent - it's a collection, not a nullable reference
- Fewer runtime errors during development
- Consistent with JavaScript best practices

**Example**:
```javascript
// app.js - Backend service initialization

// ✅ Correct initialization
let todos = []; // Empty array, ready for operations
let nextId = 1; // Counter starts at 1

// Now array methods work immediately
app.post('/api/todos', (req, res) => {
  const todo = {
    id: nextId++,
    title: req.body.title,
    completed: false,
    createdAt: new Date().toISOString()
  };
  todos.push(todo); // No null check needed
  res.status(201).json(todo);
});

app.get('/api/todos', (req, res) => {
  res.json(todos); // Returns [] if empty, never null
});
```

**Related Files**:
- [packages/backend/src/app.js](../../packages/backend/src/app.js) - Main service initialization

**Discovered**: Session 5.1 - Backend Test Suite Fixes

---

## Pattern Library

<!-- Add your discovered patterns below -->

<!-- Example:

### Error Response Format

**Context**: Returning errors from Express API endpoints

**Problem**: Need consistent error response format across all endpoints for frontend error handling

**Solution**: Always return errors with this structure:
```javascript
res.status(statusCode).json({ error: "Error message" });
```

**Example**:
```javascript
// Validation error
if (!title || title.trim() === '') {
  return res.status(400).json({ error: 'Title is required' });
}

// Not found error
if (!todo) {
  return res.status(404).json({ error: 'Todo not found' });
}
```

**Related Files**:
- packages/backend/src/app.js - All endpoints use this format

**Discovered**: Session 5.1

---

### ID Generation Pattern

**Context**: Generating unique IDs for in-memory data stores

**Problem**: Need simple, predictable IDs for learning exercise (not production)

**Solution**: Use incrementing counter starting at 1:
```javascript
let nextId = 1;

function createTodo(title) {
  return {
    id: nextId++,
    // ...other fields
  };
}
```

**Benefits**:
- Simple to understand and debug
- Predictable for testing
- Sufficient for learning exercises

**Related Files**:
- packages/backend/src/app.js

**Discovered**: Session 5.1

---

-->

---

## Pattern Categories

As your pattern library grows, consider organizing patterns by category:

- **Initialization Patterns**: Module setup, configuration
- **Data Manipulation**: Array operations, state updates
- **Error Handling**: Response formats, validation
- **API Design**: Endpoint structure, status codes
- **Testing Patterns**: Test organization, mocking strategies
- **UI Patterns**: Component structure, state management

---

## Notes

- Focus on **non-trivial patterns** - skip obvious JavaScript conventions
- Include **context** so AI understands when to apply the pattern
- Provide **code examples** that can be directly referenced
- Keep examples **concise** but complete enough to understand
- Update patterns if you discover better approaches
- Cross-reference related files for deeper context
