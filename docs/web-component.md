# Web Components

**Web Components** are a way of creating custom HTML elements that are browser- and framework-agnostic.  
They are built using technologies like the **Shadow DOM**, which allows components to be **encapsulated** from the main DOM and prevents them from affecting other elements and styles in the project.

---

## 🔻 Downsides

- They use some unusual or low-level APIs, such as `Shadow DOM` and `window.customElements.define`.
- They do not support **state management natively**, so more boilerplate code is often required to manage dynamic behavior.
