---
name: coding-style
description: Enforces R and C++ code formatting standards for the RSI project. Use when writing R code, C++ code, formatting functions, or when the user asks about coding style.
---

# Coding Style Rules

**Principle: Break line for each argument and after arithmetic operations.**

## General Rules

- **Break line for each argument** in function definitions and calls; for assignments like `x <- f(...)`, break line after the opening `(` of the function call and before the closing `)` (one line per argument or expression inside the call).
- **Break line after arithmetic operations** (`+`, `-`, `*`, `/`, etc.)
- **Keep comments minimal** (only essential comments)
- **If statements**: break line **after** the opening parenthesis `(`, and **before** the closing parenthesis `)`; when the condition uses `&&` or `||`, also break line after each `&&` or `||`.
- **Parenthesized expressions** (e.g. arithmetic): break line after the opening `(`, break line after binary operators (e.g. `-`, `+`), and break line right before the closing `)` (so the closing `)` is on its own line or starts the next part, e.g. `) / denominator`).

## Function Argument Ordering

**Alphabetical order with required arguments first, then optional arguments:**

1. Required arguments (no default values) first, alphabetical
2. Optional arguments (with default values) after, alphabetical

Ensures R function signatures match C++ function signatures.

## C++ Error Handling

Use `std::numeric_limits<double>::quiet_NaN()` for error handling in C++ catch blocks.

See [examples.md](examples.md) for detailed examples.
