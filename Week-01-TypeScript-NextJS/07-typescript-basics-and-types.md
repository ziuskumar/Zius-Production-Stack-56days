# TypeScript Basics and Basic Types

## Introduction

TypeScript is a superset of JavaScript that adds static typing and helps catch many errors during development.

```text
TypeScript
    │
    ├── JavaScript
    │
    └── Type System
          │
          ├── Type Checking
          ├── Better Autocomplete
          └── Error Detection
```

## Definition

TypeScript is a programming language built on JavaScript that adds a static type system.

```typescript
let username: string = "Zius";
let age: number = 21;
let isStudent: boolean = true;
```

## Why TypeScript?

* Catches many errors during development
* Provides better autocomplete
* Makes code easier to understand
* Improves maintainability
* Helps with large applications
* Makes refactoring safer

## Basic Types

### String

```typescript
let name: string = "Zius";
```

Used for text.

### Number

```typescript
let age: number = 21;
let salary: number = 50000;
```

Used for numeric values.

### Boolean

```typescript
let isStudent: boolean = true;
```

Used for `true` or `false`.

### Array

```typescript
let numbers: number[] = [10, 20, 30];

let skills: string[] = [
    "JavaScript",
    "TypeScript",
    "React"
];
```

### Object

```typescript
let user: {
    name: string;
    age: number;
} = {
    name: "Zius",
    age: 21
};
```

Visual structure:

```text
user
 │
 ├── name → string
 │
 └── age  → number
```

## Type Annotation

A type annotation explicitly tells TypeScript what type a variable should have.

```typescript
let name: string = "Zius";
let age: number = 21;
let active: boolean = true;
```

### Structure

```text
let age: number = 21;
    │     │       │
    │     │       └── Value
    │     └────────── Type
    └──────────────── Variable
```

## Type Inference

TypeScript can automatically determine the type.

```typescript
let name = "Zius";
let age = 21;
let isStudent = true;
```

TypeScript understands:

```text
name      → string
age       → number
isStudent → boolean
```

Explicit typing is therefore not always necessary.

## Type Safety

TypeScript prevents incompatible values from being assigned to typed variables.

```typescript
let age: number = 21;

age = "twenty one";
```

❌ Error because `age` expects a `number`.

Correct:

```typescript
age = 22;
```

## TypeScript Compilation Flow

```text
TypeScript Code
      │
      ↓
TypeScript Compiler
      │
      ├── Type Checking
      │
      ↓
JavaScript Code
      │
      ↓
Browser / Node.js
```

## Practical Example

```typescript
let username: string = "Zius";
let age: number = 21;
let isStudent: boolean = true;

let skills: string[] = [
    "JavaScript",
    "TypeScript",
    "React"
];

console.log(username);
console.log(age);
console.log(isStudent);
console.log(skills);
```

### Output

```text
Zius
21
true
[ "JavaScript", "TypeScript", "React" ]
```

## Common Mistakes 🚨

### Wrong Type

```typescript
let age: number = "21";
```

❌ `"21"` is a string.

```typescript
let age: number = 21;
```

✅ Correct.

### Mixed Array Types

```typescript
let numbers: number[] = [1, 2, "3"];
```

❌ Incorrect.

```typescript
let numbers: number[] = [1, 2, 3];
```

✅ Correct.

## Interview Keywords 🎯

* TypeScript
* Static typing
* Type safety
* Type annotation
* Type inference
* Type checking
* TypeScript compiler
* JavaScript superset
* `.ts`
* `.tsx`

## Interview Questions

### What is TypeScript?

TypeScript is a superset of JavaScript that adds static typing and other development features.

### What is type annotation?

Explicitly specifying the expected type.

```typescript
let age: number = 21;
```

### What is type inference?

When TypeScript automatically determines the type.

```typescript
let age = 21;
```

### Does TypeScript run directly in the browser?

Generally, no. TypeScript is compiled/transpiled into JavaScript before execution.

### Is explicit typing always required?

No. TypeScript can infer many types automatically.

## Interview Traps 🔥

* TypeScript is a **superset of JavaScript**.
* TypeScript types are primarily used for **development and compile-time checking**.
* TypeScript supports **type inference**, so explicit types are not always required.

## Quick Revision 🧠

```text
string  → text
number  → numbers
boolean → true / false
array   → multiple values
object  → related properties
```

### Type Annotation

```typescript
let age: number = 21;
```

### Type Inference

```typescript
let age = 21;
```

### Core Idea

```text
JavaScript
    +
Static Type System
    ↓
TypeScript
    ↓
Type Checking
    ↓
JavaScript
```

## Today's Progress

✅ TypeScript basics
✅ Basic types
✅ Type annotations
✅ Type inference
✅ Basic type safety

🟨 **Next:** Continue TypeScript essentials
