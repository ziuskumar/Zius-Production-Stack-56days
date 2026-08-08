# 📂 File and Folder Structure

## 📌 Core Structure

```text
src/
app/
public/
```

---

## 🧭 app/ Folder

```text
app/
├── layout.tsx
├── page.tsx
└── globals.css
```

### 🎯 Purpose

| File | Purpose |
|------|---------|
| `layout.tsx` | Shared UI for all pages |
| `page.tsx` | Route page |
| `globals.css` | Global styles |

---

## 🖼️ public/ Folder

Used for **images, icons, and static files**.

```text
public/
└── logo.png
```

### ✅ Access

```tsx
<img src="/logo.png" alt="Logo" />
```

---

## 🧠 Mental Model

```text
app/        → Routing
layout.tsx  → Shared UI
page.tsx    → Page content
public/     → Static assets
```

---

## ⚡ Quick Revision

- 📂 `app/` = routes
- 🧩 `layout.tsx` = common layout
- 📄 `page.tsx` = actual page
- 🖼️ `public/` = static files

---

## 🎤 Interview Keywords

`App Directory • Layout • Route • Static Assets • Shared UI`

---

## 🔥 10-Second Revision

👉 **app = routing | layout = shared UI | page = page | public = images**
