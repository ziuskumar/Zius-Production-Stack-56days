# 🧭 Next.js Routing & Navigation

## 📌 What is Routing?

Routing decides **which UI/page should be displayed for a particular URL**.

Next.js App Router uses **file-system based routing**.

```text
Folder Structure → URL
```

---

## 🗂️ Basic Routing

Inside the `app` directory:

```text
app/
├── page.tsx
├── about/
│   └── page.tsx
└── contact/
    └── page.tsx
```

Creates:

```text
/          → Home
/about     → About
/contact   → Contact
```

### Rule

```text
folder = URL segment
page.tsx = actual route
```

---

## 📁 Nested Routes

```text
app/
└── dashboard/
    └── settings/
        └── page.tsx
```

URL:

```text
/dashboard/settings
```

Multiple folders create nested URLs.

---

## 🔗 Navigation with Link

Next.js provides `Link` for internal navigation.

```tsx
import Link from "next/link";

export default function Navbar() {
  return (
    <nav>
      <Link href="/">Home</Link>
      <Link href="/about">About</Link>
      <Link href="/dashboard">Dashboard</Link>
    </nav>
  );
}
```

### Why `Link`?

It provides optimized **client-side navigation** between internal routes.

---

## 🆚 Link vs `<a>`

| `Link` | `<a>` |
|---|---|
| Next.js navigation | Standard HTML navigation |
| Recommended for internal routes | Useful for normal/external links |
| Client-side navigation | Browser navigation |

---

## 🔥 Dynamic Routes

Used when part of the URL changes dynamically.

Example:

```text
/products/101
/products/102
/products/103
```

Create:

```text
app/
└── products/
    └── [id]/
        └── page.tsx
```

`[id]` is a **dynamic route segment**.

```text
/products/[id]
        ↓
/products/101
```

The value can be accessed through `params`.

```tsx
export default async function ProductPage({
  params,
}: {
  params: Promise<{ id: string }>;
}) {
  const { id } = await params;

  return <h1>Product {id}</h1>;
}
```

---

## 🧩 Route Groups

Route groups use parentheses:

```text
app/
├── (auth)/
│   ├── login/
│   │   └── page.tsx
│   └── signup/
│       └── page.tsx
```

URLs:

```text
/login
/signup
```

`(auth)` does **not** appear in the URL.

### Why?

Mainly for **organizing routes** and applying layouts to groups of routes.

---

## 🧱 Layouts

`layout.tsx` contains UI shared between routes.

```text
app/
├── layout.tsx
├── page.tsx
└── dashboard/
    ├── layout.tsx
    ├── page.tsx
    └── settings/
        └── page.tsx
```

Example use:

```text
Root Layout
 ├── Navbar
 ├── Page
 └── Footer
```

Dashboard layout could contain:

```text
Dashboard Layout
 ├── Sidebar
 ├── Dashboard Page
 └── Settings Page
```

---

## ⚡ Programmatic Navigation

When navigation should happen after an action, use `useRouter()`.

```tsx
"use client";

import { useRouter } from "next/navigation";

export default function Login() {
  const router = useRouter();

  function handleLogin() {
    router.push("/dashboard");
  }

  return (
    <button onClick={handleLogin}>
      Login
    </button>
  );
}
```

### Common Methods

```tsx
router.push("/dashboard");
router.replace("/dashboard");
router.back();
router.forward();
router.refresh();
```

| Method | Purpose |
|---|---|
| `push()` | Navigate to a new route |
| `replace()` | Navigate without adding history entry |
| `back()` | Go back |
| `forward()` | Go forward |
| `refresh()` | Refresh current route |

---

## 🔍 Dynamic Route vs Search Params

### Dynamic Route

```text
/products/101
```

Used when `101` identifies a resource.

```text
/products/[id]
```

### Search Params

```text
/products?category=shoes
```

Used for filtering, searching, sorting, etc.

```text
category = shoes
```

### Easy Difference

```text
/products/101
        ↑
   Dynamic Route

/products?category=shoes
        ↑
   Search Parameter
```

---

## 🚨 Common Mistakes

### ❌ Folder without `page.tsx`

```text
app/about/
```

does not create a page by itself.

### ✅ Correct

```text
app/about/page.tsx
```

---

### ❌ Using `useRouter()` in a Server Component

`useRouter()` is a Client Component hook.

```tsx
"use client";
```

is required when using it.

---

## 🎯 Interview Questions

### 1. How does routing work in Next.js?

Next.js uses **file-system based routing** where folders represent URL segments and `page.tsx` defines the route UI.

### 2. How do you create a dynamic route?

Use square brackets:

```text
app/products/[id]/page.tsx
```

### 3. Difference between `Link` and `useRouter()`?

`Link` is mainly for normal declarative navigation.

`useRouter()` is used for programmatic navigation after events/actions.

### 4. What is a route group?

A folder wrapped in parentheses, such as `(auth)`, used for organization without affecting the URL.

---

## 🧠 Quick Revision

```text
app/page.tsx
      ↓
      /

app/about/page.tsx
      ↓
      /about

app/products/[id]/page.tsx
      ↓
      /products/123

(group)
      ↓
Organization only

layout.tsx
      ↓
Shared UI

<Link>
      ↓
Normal navigation

useRouter()
      ↓
Programmatic navigation
```

### 🔥 Remember

> **Folder → URL | page.tsx → Route | `[id]` → Dynamic | `(group)` → Organization | layout.tsx → Shared UI**