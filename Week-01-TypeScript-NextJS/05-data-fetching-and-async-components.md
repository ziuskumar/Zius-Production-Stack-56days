# Data Fetching and Async Components in Next.js

## 📌 Introduction

One of the biggest advantages of **Next.js App Router** is that components can be **async**.

This means you can fetch data directly inside a Server Component without using `useEffect`.

This is a **very important placement and interview topic** because it improves:

- ⚡ Performance
- 🔍 SEO
- 📦 Bundle size
- 🧠 Simplicity

---

# 🧠 Definition

## Async Component

A component declared with the `async` keyword.

```tsx
export default async function Page() {}
```

It can use `await` directly inside the component.

---

# 🤔 Why It Exists

In traditional React:

```tsx
useEffect(() => {
  fetch('/api/data');
}, []);
```

Problems:

- Extra loading state
- Runs after render
- Worse SEO
- More client JavaScript

Next.js App Router solves this by fetching on the **server before sending HTML**.

---

# ⚙️ Working

## Flow

```text
Browser Request
      │
      ▼
Server Component
      │
      ▼
Fetch Data
      │
      ▼
Generate HTML
      │
      ▼
Send HTML to Browser
```

---

# 💻 Basic Example

## app/page.tsx

```tsx
async function getPosts() {
  const res = await fetch('https://jsonplaceholder.typicode.com/posts');

  return res.json();
}

export default async function Page() {
  const posts = await getPosts();

  return (
    <div>
      <h1>Posts</h1>

      {posts.slice(0, 5).map((post: any) => (
        <div key={post.id}>
          <h2>{post.title}</h2>
        </div>
      ))}
    </div>
  );
}
```

---

# 📤 Output

```text
Posts

sunt aut facere...
qui est esse...
ea molestias quasi...
...
```

---

# 💡 Explanation

- `Page` is a Server Component
- It waits for data before rendering
- Browser receives ready HTML
- No `useEffect`
- No client-side fetching

---

# 🔄 Fetching Directly in Component

You can also fetch directly:

```tsx
export default async function Page() {
  const res = await fetch('https://jsonplaceholder.typicode.com/users');
  const users = await res.json();

  return (
    <ul>
      {users.map((u: any) => (
        <li key={u.id}>{u.name}</li>
      ))}
    </ul>
  );
}
```

---

# 📦 Caching in Next.js

By default, Next.js **caches fetch requests** in Server Components.

```tsx
await fetch(url);
```

This behaves like static caching when possible.

---

# 🔁 Force Dynamic Fetching

Use:

```tsx
await fetch(url, {
  cache: 'no-store',
});
```

### Use when:

- User-specific data
- Dashboard
- Real-time data
- Frequently changing data

---

# ⏱️ Revalidation (ISR)

Fetch fresh data every 60 seconds.

```tsx
await fetch(url, {
  next: { revalidate: 60 },
});
```

---

# 📊 Caching Comparison

| Option | Behavior |
|---|---|
| Default | Cached |
| `cache: 'no-store'` | Always fresh |
| `revalidate: 60` | Fresh every 60s |

---

# 🧠 Memory Trick

```text
Default      → Cached
no-store     → Dynamic
revalidate   → Periodic refresh
```

---

# ⚡ Parallel Data Fetching

## ❌ Sequential

```tsx
const users = await fetchUsers();
const posts = await fetchPosts();
```

Time = **Users + Posts**

---

## ✅ Parallel

```tsx
const [users, posts] = await Promise.all([
  fetchUsers(),
  fetchPosts(),
]);
```

Time = **Max(Users, Posts)**

---

# 📈 Performance Benefit

```text
Sequential
──────────
Users  2s
Posts  2s
Total  4s

Parallel
────────
Users  2s
Posts  2s
Total  2s
```

---

# 🎯 Interview Tip

Always mention **Promise.all for independent requests**.

---

# 🧩 Loading UI

Create `loading.tsx`.

## app/loading.tsx

```tsx
export default function Loading() {
  return <p>Loading...</p>;
}
```

Next.js automatically shows it while the async page is loading.

---

# 🖼️ Error Handling

Create `error.tsx`.

## app/error.tsx

```tsx
'use client';

export default function Error({
  error,
}: {
  error: Error;
}) {
  return <p>Something went wrong</p>;
}
```

---

# 🏗️ Real Project Structure

```text
app/
├── page.tsx
├── loading.tsx
├── error.tsx
└── components/
    ├── post-list.tsx
    └── post-card.tsx
```

---

# 🔒 Why Server Fetching Is Better

## Client Fetch

```text
HTML
  ↓
JS Download
  ↓
Render
  ↓
Fetch
  ↓
Render Again
```

---

## Server Fetch

```text
Fetch
  ↓
Render
  ↓
Send Ready HTML
```

Fewer steps = better performance.

---

# 🌍 Real-World Example

## E-commerce

### Server Fetch

- Products
- Categories
- Reviews
- Prices

### Client Fetch

- Cart updates
- Search suggestions
- Filters
- Live notifications

---

# ⚠️ Common Mistakes

## ❌ Using useEffect for initial page data

```tsx
useEffect(() => {
  fetchData();
}, []);
```

Prefer Server Components.

---

## ❌ Forgetting `await`

```tsx
const data = fetch(url);
```

Returns a Promise, not data.

---

## ❌ Sequential independent requests

Use `Promise.all`.

---

# 🔥 Interview Traps

### Q1. Can Server Components use async/await?

✅ Yes.

---

### Q2. Does async make it a Client Component?

❌ No.

---

### Q3. Where is fetch executed?

✅ On the server (for Server Components).

---

### Q4. How do you disable caching?

✅ `cache: 'no-store'`

---

### Q5. How do you revalidate periodically?

✅ `next: { revalidate: 60 }`

---

# 📊 Quick Comparison

| Feature | Server Fetch | Client Fetch |
|---|---|---|
| SEO | ✅ | ⚠️ |
| Initial Speed | ✅ | ❌ |
| Bundle Size | ✅ | ❌ |
| Real-time | ⚠️ | ✅ |
| Browser APIs | ❌ | ✅ |

---

# 🧠 Best Practice

## Recommended Pattern

```text
Page (Server)
   │
   ├── Fetch data
   ├── Render content
   │
   └── Interactive parts
         ↓
      Client Components
```

---

# ⚡ Quick Revision

- `async function Page()`
- Use `await fetch()`
- Default = cached
- `no-store` = always fresh
- `revalidate` = periodic refresh
- `Promise.all` for parallel requests
- `loading.tsx` for loading UI
- `error.tsx` for error UI

---

# 🎤 Placement One-Liner

> In Next.js App Router, I prefer server-side data fetching using async Server Components because it improves SEO, reduces client-side JavaScript, enables caching and revalidation, and allows parallel data fetching with Promise.all for better performance.