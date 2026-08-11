# Server vs Client Components in Next.js

## 📌 Introduction

Next.js App Router introduces **React Server Components (RSC)** by default.

Understanding **Server Components vs Client Components** is one of the **most important Next.js interview topics**.

This concept directly affects:

- ⚡ Performance
- 📦 Bundle size
- 🔒 Security
- 🚀 SEO
- 🔄 Interactivity

---

# 🧠 Definition

## Server Component

A component that runs **on the server** and sends **HTML/UI to the browser**.

- Default in App Router
- No JavaScript sent for that component
- Can access databases, APIs, environment variables

## Client Component

A component that runs **in the browser**.

- Must start with `'use client'`
- JavaScript is sent to the browser
- Supports state, effects, and event handlers

---

# 🤔 Why This Exists

Before React Server Components:

- Every component became browser JavaScript
- Larger bundle size
- Slower loading

With Server Components:

- Less JS shipped
- Faster initial render
- Better SEO
- Better security

---

# ⚙️ Working

## Flow

```text
Request
   │
   ▼
Server Component executes
   │
   ▼
Fetches data / DB
   │
   ▼
Generates HTML
   │
   ▼
Browser receives HTML
```

Client Components are hydrated later.

---

# 🖥️ Server Component Example

## app/page.tsx

```tsx
async function getUsers() {
  const res = await fetch('https://jsonplaceholder.typicode.com/users');
  return res.json();
}

export default async function Page() {
  const users = await getUsers();

  return (
    <div>
      <h1>Users</h1>
      {users.map((u: any) => (
        <p key={u.id}>{u.name}</p>
      ))}
    </div>
  );
}
```

---

# 📤 Output

```text
Users
Leanne Graham
Ervin Howell
...
```

---

# 💡 Explanation

- Runs only on the server
- Browser receives ready HTML
- No state or click handlers
- Great for data fetching

---

# 💻 Client Component Example

## app/components/counter.tsx

```tsx
'use client';

import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

---

# 📤 Output

```text
Count: 0
(click)
Count: 1
```

---

# 💡 Explanation

- Runs in the browser
- Supports interactivity
- JavaScript is downloaded
- Uses React hooks

---

# 🔄 Combining Both

## Server Parent + Client Child

```tsx
// page.tsx (Server)
import Counter from './components/counter';

export default function Page() {
  return (
    <div>
      <h1>Dashboard</h1>
      <Counter />
    </div>
  );
}
```

This is the **recommended pattern**.

---

# 📊 Comparison Table

| Feature | Server Component | Client Component |
|---|---|---|
| Default | ✅ Yes | ❌ No |
| Runs on server | ✅ | ❌ |
| Runs in browser | ❌ | ✅ |
| useState | ❌ | ✅ |
| useEffect | ❌ | ✅ |
| onClick | ❌ | ✅ |
| Fetch data | ✅ Excellent | ⚠️ Possible |
| Access DB | ✅ | ❌ |
| Access env vars | ✅ | ❌ |
| SEO | ✅ | ⚠️ Depends |
| Bundle size | ✅ Smaller | ❌ Larger |

---

# 🧠 Memory Trick

```text
Server = DATA
Client = INTERACTION
```

- Fetch → Server
- Click → Client
- State → Client
- Database → Server

---

# 📈 Performance Impact

## ❌ Everything Client

```text
HTML + Large JS
```

- Slow load
- More hydration
- Bigger bundle

## ✅ Server First

```text
HTML + Minimal JS
```

- Fast load
- Better Core Web Vitals
- Better SEO

---

# 🔒 Security Advantage

## Server Component

```tsx
const users = await db.user.findMany();
```

- DB credentials stay on server
- Never exposed

## Client Component

```tsx
fetch('/api/users')
```

Cannot directly access DB credentials.

---

# 🎯 When to Use Server Components

Use for:

- Dashboard data
- Product lists
- Blog posts
- SEO pages
- Database queries
- Server-side fetching
- Environment variables

---

# 🎯 When to Use Client Components

Use for:

- Forms
- Buttons
- Modals
- Dropdowns
- Tabs
- Animations
- useState
- useEffect
- Browser APIs

---

# 🏗️ Real-World Architecture

```text
page.tsx (Server)
 ├── UserInfo (Server)
 ├── RecentTasks (Server)
 ├── Stats (Server)
 └── TaskForm (Client)
      └── SubmitButton (Client)
```

👉 Keep most of the tree on the **server**.

---

# ⚠️ Common Mistakes

## ❌ Forgetting 'use client'

```tsx
import { useState } from 'react';
```

Error: Hooks can only be used in Client Components.

---

## ❌ Making entire page client

```tsx
'use client';
```

at the top of a large page.

🚨 This sends unnecessary JS.

---

## ❌ Fetching data in client unnecessarily

```tsx
useEffect(() => {
  fetch('/api/data');
}, []);
```

Prefer server fetching when possible.

---

# 🔥 Interview Traps

### Q1. Are all Next.js components server components?

✅ **In the App Router, yes by default.**

---

### Q2. Can a Server Component import a Client Component?

✅ **Yes.**

---

### Q3. Can a Client Component import a Server Component?

❌ **No.**

---

### Q4. Does 'use client' affect child components?

✅ **Yes. All imported children become part of the client bundle.**

---

### Q5. Where should data fetching happen?

✅ **Prefer Server Components unless the data depends on browser interaction.**

---

# 🧩 Diagram

```text
                ┌─────────────────┐
                │  Server Component│
                └────────┬────────┘
                         │
                fetch DB/API
                         │
                         ▼
                    HTML sent
                         │
                         ▼
                ┌─────────────────┐
                │ Browser renders │
                └────────┬────────┘
                         │
                    hydrate only
                         │
                         ▼
                ┌─────────────────┐
                │ Client Component│
                └─────────────────┘
```

---

# 🏢 Real-World Example

## E-commerce Product Page

### Server

- Product details
- Price
- Reviews
- Related products

### Client

- Add to cart
- Quantity selector
- Wishlist button
- Image zoom

This minimizes JavaScript while keeping the page interactive.

---

# ⚡ Quick Revision

## 30-Second Revision

- **Default = Server Component**
- **'use client' = Browser component**
- **Server → data, SEO, security**
- **Client → state, effects, events**
- **Server can import Client**
- **Client cannot import Server**
- **Keep client components as small as possible**

---

# 🎤 Placement One-Liner

> In Next.js App Router, I use Server Components for data fetching and SEO, and Client Components only for interactivity such as state, effects, and event handlers, which keeps the application faster, more secure, and smaller in bundle size.