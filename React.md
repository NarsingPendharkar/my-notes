# React



---

### What is React

**React** is a JavaScript library for building user interfaces, developed and maintained by **Meta (Facebook)**. It was first released in 2013 and has since become one of the most widely used tools for building modern, interactive web applications.

Unlike a full framework, React focuses primarily on the **view layer** of an application — it helps developers build reusable **UI components** that manage their own state and render efficiently when data changes.

##### Key characteristics:

- **Component-Based Architecture** — UIs are broken down into small, reusable, independent pieces called **components**.
- **Declarative** — You describe *what* the UI should look like for a given state, and React handles updating the DOM to match.
- **Virtual DOM** — React maintains a lightweight in-memory representation of the real DOM, allowing it to calculate the minimal set of changes needed and update the actual DOM efficiently.
- **Unidirectional Data Flow** — Data flows in one direction, from parent components to child components via **props**, making applications easier to debug and reason about.
- **JSX** — React uses **JSX (JavaScript XML)**, a syntax extension that lets you write HTML-like code directly within JavaScript.

----

### Why React

- **Reusable Components** — Build once, use across the application, reducing duplicate code.
- **Fast Rendering** — The **Virtual DOM** minimizes direct DOM manipulation, improving performance.
- **Strong Ecosystem** — Backed by a huge community, with libraries like **React Router**, **Redux**, and **React Query** for routing, state management, and data fetching.
- **Flexibility** — React is **unopinionated**; you can choose your own tools for routing, state management, and styling.
- **Easy Learning Curve** — Since React is a library (not a full framework), it's generally quicker to pick up, especially with JavaScript fundamentals already in place.
- **Backed by Meta** — Strong industry adoption and long-term support.
- **React Native** — Skills transfer directly to mobile app development.

---

### Difference between Angular and React

| Point                  | **React**                                    | **Angular**                            |
| ---------------------- | -------------------------------------------- | -------------------------------------- |
| **What it is**         | A **library** (only UI part)                 | A complete **framework**               |
| **Made by**            | **Facebook (Meta)**                          | **Google**                             |
| **Language**           | **JavaScript** (JSX), TypeScript optional    | **TypeScript** (always)                |
| **UI writing style**   | **JSX** — HTML mixed inside JS               | **HTML templates** with Angular syntax |
| **Data binding**       | **One-way** binding                          | **Two-way** binding                    |
| **Learning curve**     | **Easier**, small core                       | **Harder**, more concepts upfront      |
| **Flexibility**        | **Flexible** — pick your own tools           | **Structured** — fixed pattern         |
| **DOM used**           | **Virtual DOM** (faster updates)             | **Real DOM** with change detection     |
| **State management**   | Needs extra library (**Redux**, Context API) | Built-in via **services**              |
| **Routing**            | External library (**React Router**)          | Built-in **Angular Router**            |
| **Mobile development** | **React Native**                             | **Ionic**                              |
| **Best for**           | Fast, flexible, custom apps                  | Large, structured enterprise apps      |
| **In short**           | **Freedom + Simplicity**                     | **Structure + Built-in tools**         |

---

### Features of React JS

**1. JSX (JavaScript XML)**

- A syntax extension that allows writing HTML-like code within JavaScript.
- Makes component structure easier to read and write.
- Gets compiled (via **Babel**) into regular `React.createElement()` calls.

**2. Component-Based Architecture**

- UI is broken into independent, reusable **components**.
- Two types: **Functional Components** (modern, use Hooks) and **Class Components** (older, use lifecycle methods).
- Encourages modularity and code reuse.

**3. Virtual DOM**

- React maintains a lightweight copy of the actual DOM in memory.
- When state changes, React creates a new Virtual DOM tree, **diffs** it against the previous one, and updates only the changed parts in the real DOM.
- This process is called **Reconciliation**, making updates fast and efficient.

**4. One-Way (Unidirectional) Data Binding**

- Data flows from **parent to child** via **props**.
- Makes the application more predictable and easier to debug, since data has a single source of truth.

**5. Hooks**

- Introduced in **React 16.8**, allowing functional components to use state and lifecycle features.
- Common hooks: `useState`, `useEffect`, `useContext`, `useRef`, `useMemo`, `useCallback`, `useReducer`.
- Removed the need for class components in most cases.

**6. State and Props**

- **State** — internal, mutable data managed within a component.
- **Props** — read-only data passed from parent to child components.
- Changes to state or props trigger **re-rendering**.

**7. Declarative UI**

- Developers describe *what* the UI should look like for each state.
- React handles the *how*, updating the DOM automatically to match the desired state.

**8. React Fiber**

- The **reconciliation engine** (rewritten in React 16) that enables incremental rendering.
- Allows React to pause, prioritize, and resume rendering work, improving responsiveness.

**9. Component Lifecycle**

- Class components have lifecycle methods: `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`.
- Functional components replicate this behavior using `useEffect`.

**10. Conditional Rendering**

- UI can be rendered conditionally using JavaScript expressions (`if`, ternary operators, `&&`).

**11. Rich Ecosystem**

- **React Router** — client-side routing.
- **Redux / Context API / Zustand** — state management.
- **React Query / SWR** — data fetching and caching.
- **Next.js** — server-side rendering (SSR) and static site generation (SSG) framework built on React.

**12. React Native Support**

- Same core concepts and component model extend to **mobile app development** via React Native.

**13. Server-Side Rendering (SSR) Support**

- React can render components on the server (commonly via **Next.js**), improving SEO and initial load performance.

**14. Testing Support**

- Strong tooling ecosystem: **Jest**, **React Testing Library**, **Enzyme** for unit and component testing.

**15. Backward Compatibility**

- Meta maintains strong backward compatibility, making upgrades between versions relatively smooth.

---

### What is Virtual DOM & Real DOM

**DOM (Document Object Model)** is a tree-like structure that represents your webpage in the browser's memory. Every HTML tag becomes a "node" in this tree, and JavaScript can read or change these nodes to update what you see on screen.

#### Real DOM

Imagine the **Real DOM** like a **whiteboard** in a classroom.

- Every time you want to change **one word** on the whiteboard, the teacher **erases the entire board** and **rewrites everything** from scratch.
- This is slow because even a tiny change causes the whole board to be redrawn.
- The **Real DOM** works the same way — even a small update (like changing one line of text) can cause the browser to **recalculate layout, styles, and repaint** the whole page.

**Brief Notes:**

- It's the **actual structure** of the webpage the browser uses to display content.
- Updating it is **slow and expensive** because the browser re-renders large portions of the page.
- Every update triggers **reflow** and **repaint**.

#### Virtual DOM

Now imagine the **Virtual DOM** like a **notebook copy** of that whiteboard.

- Instead of erasing the whole whiteboard, you first write your change in your **notebook** (a lightweight copy).
- You then **compare** your notebook with the whiteboard to see **exactly what changed**.
- You only erase and rewrite **that one word** on the real whiteboard — not the whole thing.
- This process of comparing is called **"diffing"**, and applying only the necessary changes is called **"reconciliation."**

**Brief Notes:**

- It's a **lightweight, in-memory copy** of the Real DOM.
- React creates a **new Virtual DOM tree** whenever state/props change.
- React **compares (diffs)** the new tree with the old tree.
- Only the **actual differences** are updated in the Real DOM — making it **fast and efficient**.

---

### Why Virtual DOM is Faster

- Avoids unnecessary **reflows and repaints**.
- Batches multiple changes together before updating the Real DOM.
- Updates only the **minimal required parts**, not the entire page.

```mermaid
flowchart TD
    A["React Component"] --> B["Virtual DOM"]
    B --> C["Compare with Previous Virtual DOM"]
    C --> D["Find Changes"]
    D --> E["Update Required Parts"]
    E --> F["Real DOM"]
    F --> G["Browser UI"]
```

------

### How Virtual DOM Works

Suppose the UI initially displays:

```text
Count: 0
```

After clicking a button:

```text
Count: 1
```

React doesn't need to recreate the entire page.

It can identify that only the `0` changed to `1`.

```mermaid
flowchart LR
    A["State: Count = 0"] --> B["Virtual DOM"]
    C["State: Count = 1"] --> D["New Virtual DOM"]
    B --> E["Comparison"]
    D --> E
    E --> F["Only Count changed"]
    F --> G["Update Real DOM"]
```

------

### Real DOM vs Virtual DOM

| Real DOM                        | Virtual DOM                        |
| ------------------------------- | ---------------------------------- |
| Browser's actual DOM            | In-memory representation           |
| Managed by browser              | Managed by React                   |
| Directly updates UI             | Helps determine required updates   |
| DOM operations can be expensive | Reduces unnecessary DOM operations |
| Represents the actual page      | Represents desired UI state        |

------

**Example :**

```jsx
function App() {
    const [count, setCount] = useState(0);

    return (
        <>
            <h1>Count: {count}</h1>
            <button onClick={() => setCount(count + 1)}>
                Increment
            </button>
        </>
    );
}
```

When the button is clicked:

```text
Click Button
     ↓
State changes
     ↓
React creates new UI representation
     ↓
React compares old and new representation
     ↓
Determines required DOM changes
     ↓
Browser DOM is updated
```

------

### How React Works ?

Think of React like a **smart artist** repainting a picture.

1. **You describe what you want** — Using JSX, you tell React "this is what the screen should look like right now."
2. **React builds a Virtual DOM** — Instead of painting directly on the real canvas (the browser), it first sketches the picture on **scratch paper** (Virtual DOM).
3. **Something changes** — Say you click a button and a number updates.
4. **React draws a new sketch** — It makes a **new scratch paper** with the updated picture.
5. **React compares old vs new sketch** — This is called **diffing** — spotting exactly what's different.
6. **React updates only the changed part** — Instead of repainting the whole canvas, it only touches the **exact spot** that changed on the real DOM.

**In short:** React always keeps a draft copy, compares it to the last draft, and only updates what's actually different — making it fast and efficient.

---

#### Example — Simple Counter UI Page

Let's take a simple **Counter App** as an example to see React in action.

**The UI:**

A page with a **number**, an **Increment button**, and a **Decrement button**.

**Code Example:**

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Counter: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
    </div>
  );
}

export default Counter;
```

##### How This Works Step by Step

**1. Initial Render**

- `useState(0)` sets the initial **state** — `count = 0`.
- React builds the **Virtual DOM** for this JSX and shows: `Counter: 0`

**2. User clicks "Increment"**

- `setCount(count + 1)` is called — this updates the **state** to `1`.
- This triggers a **re-render**.

**3. New Virtual DOM created**

- React creates a **new Virtual DOM tree** with `count = 1`.

**4. Diffing**

- React **compares** the new tree with the old tree.
- It finds that only the text `Counter: 0` changed to `Counter: 1` — everything else (buttons, div) is the same.

**5. Real DOM update**

- React updates **only that one text node** in the Real DOM — not the whole page.

**In short:** Every click updates the **state**, React re-renders the component in the **Virtual DOM**, diffs it, and updates only the changed part in the **Real DOM**.

---

### How to Create a React Application

**1. Install Node.js** (includes npm)

- Download from [nodejs.org](https://nodejs.org/) and verify installation:

```bash
node -v
npm -v
```

**2. Create a React App using Vite** (recommended, faster than CRA)

```bash
npm create vite@latest my-app
```

- Select **React** as the framework.
- Select **JavaScript** or **TypeScript** as the variant.

**3. Navigate into the project folder**

```bash
cd my-app
```

**4. Install dependencies**

```bash
npm install
```

**5. Run the development server**

```bash
npm run dev
```

- App runs at **http://localhost:5173** by default.

##### Alternative — Using Create React App (older method)

```bash
npx create-react-app my-app
cd my-app
npm start
```

- App runs at **http://localhost:3000** by default.

- **Vite** is preferred over CRA today for **faster builds** and **better performance**.

---

