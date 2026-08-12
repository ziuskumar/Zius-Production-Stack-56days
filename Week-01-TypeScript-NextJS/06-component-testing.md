# 🧪 Component Testing with Vitest + React Testing Library

## Introduction

Component testing verifies that individual React components behave correctly.

In a Next.js application, component testing helps ensure that UI components render correctly and respond properly to user interactions.

Common tools:

- Vitest ⚡
- React Testing Library 🧪
- @testing-library/jest-dom

---

## Definition

### Component Testing

Component testing means testing a React component in isolation to verify:

- What it renders
- How it behaves
- How it responds to user actions
- How it handles different states

Example:

```text
Component
    │
    ├── Render correctly?
    ├── Button works?
    ├── Text appears?
    └── State changes correctly?

    Why Testing Exists

Without tests, changes to one component can accidentally break another part of the application.

Testing provides:

✅ Confidence
🐛 Early bug detection
🔄 Safer refactoring
📦 Better component design
🚀 Faster development
Vitest

Vitest is a modern JavaScript/TypeScript testing framework.

It provides:

Test runner
Assertions
Mocking
Watch mode
Fast execution

Example:

import { describe, it, expect } from "vitest";

describe("Math", () => {
  it("adds two numbers", () => {
    expect(2 + 3).toBe(5);
  });
});
Output
✓ adds two numbers
React Testing Library

React Testing Library allows us to test React components from the user's perspective.

Instead of testing internal implementation details, we test what the user can actually see and interact with.

Example:

❌ Test internal state directly

✅ Test what appears on the screen
✅ Click buttons
✅ Find text
✅ Fill inputs
Basic Testing Flow
Write Component
      │
      ▼
Render Component
      │
      ▼
Find UI Element
      │
      ▼
Perform User Action
      │
      ▼
Check Expected Result
Example Component
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>

      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
Test
import { render, screen } from "@testing-library/react";
import { fireEvent } from "@testing-library/react";
import { describe, it, expect } from "vitest";

import Counter from "./Counter";

describe("Counter", () => {
  it("renders the initial count", () => {
    render(<Counter />);

    expect(screen.getByText("Count: 0")).toBeInTheDocument();
  });

  it("increments the count", () => {
    render(<Counter />);

    const button = screen.getByRole("button", {
      name: "Increment",
    });

    fireEvent.click(button);

    expect(screen.getByText("Count: 1")).toBeInTheDocument();
  });
});
Input
Initial count = 0
User clicks Increment
Output
Count: 1
Explanation
render() renders the component.
screen.getByText() searches for visible text.
getByRole() finds an element using its accessible role.
fireEvent.click() simulates a click.
expect() verifies the expected result.
User-Centered Testing

Prefer accessible queries.

Good
screen.getByRole("button", {
  name: "Submit",
});
Good
screen.getByText("Welcome");
Good
screen.getByLabelText("Email");

Avoid relying heavily on implementation details.

Less Preferred
screen.getByTestId("submit-button");

Use data-testid when there isn't a better accessible query.

Testing Forms

Example:

<input
  aria-label="Username"
  placeholder="Enter username"
/>

Test:

const input = screen.getByLabelText("Username");

Then interact with it and verify the expected result.

Testing Different States

A component may have multiple states:

Loading
   ↓
Success
   ↓
Error

Tests should verify important states.

Example:

Loading → "Loading..."

Success → "Data loaded"

Error → "Something went wrong"
Testing Props

Example component:

function Greeting({ name }: { name: string }) {
  return <h1>Hello {name}</h1>;
}

Test:

render(<Greeting name="Zius" />);

expect(
  screen.getByText("Hello Zius")
).toBeInTheDocument();
Testing Best Practice

Test behavior rather than implementation.

Component
   │
   ▼
User Interaction
   │
   ▼
Expected UI

The goal is to answer:

"Does the component behave correctly for the user?"

Real-World Example

For a Task Manager:

Add Task
   │
   ▼
User enters "Learn React"
   │
   ▼
Clicks Add
   │
   ▼
Task appears

Test:

Input → "Learn React"

Click → Add Task

Expected → "Learn React" appears

This catches regressions if the component changes later.

Component Testing vs Unit Testing
Component Testing	Unit Testing
Focuses on UI components	Focuses on small units
Tests rendering	Tests functions/logic
Tests user interaction	Tests calculations/logic
React Testing Library	Vitest
Often uses Vitest too	Vitest

They can be used together.

Common Mistakes 🚨
1. Testing Implementation Details

Don't test exactly how state is implemented.

Test the resulting behavior.

2. Testing Only Happy Paths

Also test:

Loading
Error
Empty
Invalid input
3. Overusing Test IDs

Prefer accessible queries when possible.

4. Writing Tests That Depend on Each Other

Each test should be independent.

5. Testing Everything

Focus on important user-facing behavior.

Interview Keywords 🎯
Component Testing
Vitest
React Testing Library
Render
Assertions
User Interaction
Accessibility
Test Isolation
Mocking
Regression Testing
Behavioral Testing
Interview Traps 🔥
Q: Why React Testing Library?

Because it encourages testing components from the user's perspective instead of depending on implementation details.

Q: Why use getByRole()?

It encourages accessible, user-oriented queries and closely represents how users interact with the application.

Q: Should every component have tests?

Not necessarily. Prioritize important behavior, business logic, critical components, and areas likely to regress.

Q: Vitest vs React Testing Library?

Vitest provides the testing framework and runner, while React Testing Library provides utilities for rendering and interacting with React components.

Quick Revision 🧠
Vitest
  ↓
Test Runner + Assertions

React Testing Library
  ↓
Render + Interact with React UI

Testing Flow
  ↓
Render
  ↓
Find Element
  ↓
Interact
  ↓
Assert Result
One-Line Interview Answer

Component testing verifies that React components render correctly and behave as expected when users interact with them.