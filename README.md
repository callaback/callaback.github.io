## 🔧 The API builder that lets you see what's happening

**callback** is a Jekyll-based documentation boilerplate for APIs. Build your docs, add API specs, customize the theme.

### Why we built this

- Our APIs send JSON objects, not parameter strings
- Testing live APIs is risky (nobody wants accidental deletes)
- Running a server for static docs felt like overkill

**The real value?** A solid structure for API documentation. Use it as a template.

---

## 🚀 Install

It's Jekyll...

1. Clone this repo
2. [Install Jekyll](https://github.com/mojombo/jekyll/wiki/install)
3. Run `jekyll serve --watch` at the root
4. Open `http://localhost:4000`

---

## 📝 How to...

### Add a new API call

Create a new post in `_posts/`. Jekyll requires dates in filenames (yeah, we know). Use dates to control display order.

**YAML header options:**

| Variable | Required | Description |
|----------|----------|-------------|
| `title` | ✅ | Short description of the call |
| `path` | ❌ | URL path with parameters |
| `type` | ❌ | `GET` `POST` `PUT` `DELETE` or leave blank |

**Example:**
```yaml
---
path: '/stuff/:id'
title: 'Delete a thing'
type: 'DELETE'
---
```

Add request/response details in the post body. Check `_posts` for examples.

### Group calls

Add `category` to group methods in navigation:
```yaml
---
category: Stuff
path: '/stuff/:id'
title: 'Delete a thing'
type: 'DELETE'
---
```

### Customize design

Edit `css/style.css` and jQuery scripts in `/_layouts/default.html`. Make it yours.


