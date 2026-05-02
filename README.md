# n8n-notes

Your n8n session notes 📃    
**All in One Place** 

# 📘 n8n Expressions Guide

## 🔹 What are Expressions?
```js
{{ ... }}
```
➡️ Tells n8n that this is a **dynamic expression** (JavaScript-based)

---

## 🔹 Working with Multiple Items

### A. Handle each item individually (current item in loop)
```js
{{ $('Source Node').item.json.key }}
```

- n8n automatically processes items in a loop  
- `.item` refers to the **current item**

#### 📌 If value is an array:
```js
{{ $('Source Node').item.json.key[0] }}
```

#### 📌 If value is a JSON object:
```js
{{ $('Source Node').item.json.key.inner_key }}
```

#### 📌 Get all keys of a JSON object:
```js
{{ Object.keys($('Source Node').item.json.key) }}
```

---

### B. Always use first item (static reference)
```js
{{ $('Source Node').first().json.key }}
```

---

### C. Always use last item (static reference)
```js
{{ $('Source Node').last().json.key }}
```

---

### D. Access all items (returns array)
```js
{{ $('Source Node').all() }}
```

#### 📌 Access a specific item:
```js
{{ $('Source Node').all()[0].json.key }}
```

#### 📌 Extract a field from all items:
```js
{{ $('Source Node').all().map(item => item.json.key) }}
```

---

## 🔹 Applying Functions

Since expressions use JavaScript, you can apply functions:

```js
{{ $('Source Node').item.json.name.toUpperCase() }}
```

```js
{{ Math.round($('Source Node').item.json.age / 7) }}
```

```js
{{ typeof $('Source Node').item.json.scores }}
```

---

## 🔹 Converting JSON Object to String

```js
{{ JSON.stringify($('Source Node').item.json.key, null, 2) }}
```

- `null, 2` → formats output (pretty print)

---

## ⚠️ Important Notes

- `.item` → current item (used in loops)
- `.first()` / `.last()` → **do NOT loop**, always return fixed items
- `.all()` → returns **all items as an array** (use carefully with large data)
- Expressions use **JavaScript syntax**, not Python





