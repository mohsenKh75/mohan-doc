---
id: stack-vs-heap
title: Stack vs Heap
sidebar_label: Stack vs Heap
---

# Stack and Heap in JavaScript

## Stack

- The **stack** is used for storing short-lived data such as:

  - Function calls
  - Local variables (e.g., strings, numbers)

- When a function is called, it's added (pushed) to the stack. When it finishes, it's removed (popped) from the stack.

- If too many function calls happen without returning (e.g., deep or infinite recursion), we face a **"Maximum call stack size exceeded"** error.

- This happens when the browser or Node.js reaches its **call stack limit**.

- In Chrome or Node.js, the limit is typically between **10,000 to 20,000 calls**, depending on how much RAM is in use.

## Heap

- The **heap** is used for storing complex and long-lived data, such as:

  - Objects
  - Arrays
  - Functions
  - Long or dynamic strings

- Data stored in the heap is managed by **Garbage Collection (GC)**.

- For example:

  - If a function creates an object and returns it, and we assign the result to a variable, the data stays in the heap.
  - If we don’t reference the returned object, it will eventually be garbage collected.

- The heap is **larger** than the stack and suitable for storing **dynamic or complex structures** that need to persist in memory longer.

---

**Summary**:

- **Stack**: Short-lived, simple data; limited size; fast; call stack errors possible.
- **Heap**: Long-lived, complex data; larger; managed by GC.
