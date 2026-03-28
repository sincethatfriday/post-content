---
title: "How we built the Since That Friday backend"
date: "2025-03-20"
author: "Sam"
tag: "Story"
excerpt: "A Node.js backend with a contact form, AI chatbot, and a GitHub-powered blog. Here's how we built it and why we made the choices we did."
---

## Why we built it ourselves

We could have used Webflow, Squarespace, or any no-code tool. They're great products. But we build things for a living — it felt wrong to not build our own.

So we built the Since That Friday backend from scratch using Node.js. Here's what it does and how it's put together.

## What the backend handles

Three things:

**1. Contact form**
When someone fills the form on our website, the backend validates the input, builds a clean email, and sends it straight to hola@sincethatfriday.in. Simple, no third-party form tools, no monthly fees.

**2. Joy — our AI chatbot**
Joy runs on LLaMA via Groq's free API. The backend handles the conversation history, the system prompt, and the handoff flow that collects leads and emails them to us automatically.

**3. This blog**
Every post you're reading is a markdown file sitting in our GitHub repo. The backend fetches it via the GitHub API, parses the frontmatter, converts it to HTML, and serves it. No CMS, no database, no admin panel. Just files.

## The tech stack

- **Runtime:** Node.js
- **Framework:** Express
- **Email:** Nodemailer with Gmail SMTP
- **Chatbot:** Groq API with LLaMA 3.1
- **Blog:** GitHub API + gray-matter + marked
- **Architecture:** Controllers, services, routes — clean and separated

## The folder structure
```
stf-backend/
├── app.js
├── src/
│   ├── controllers/
│   ├── services/
│   ├── routes/
│   └── knowledge/
```

Every feature has its own controller, service, and route file. Adding something new means adding three files and one line in app.js. Nothing bleeds into anything else.

## What we learned

**Keep it lightweight.** We have four dependencies for the core backend — express, nodemailer, cors, dotenv. That's it. Every package you add is a package you have to maintain.

**Separate your concerns.** The route doesn't know about the database. The controller doesn't know about nodemailer. The service does one thing. When something breaks you know exactly where to look.

**Environment variables for everything sensitive.** API keys, SMTP passwords, GitHub tokens — all in `.env`, never in code, never in GitHub.

## What's next

We're planning to add:

- A filter by tag on the blog
- A newsletter signup that feeds into an email sequence
- A simple admin view to see all chatbot conversations

All of it will be built the same way — lightweight, clean, no unnecessary complexity.

If you want to see how any of this works or want something similar for your business — you know where to find us.

📧 hola@sincethatfriday.in
```

---

Commit to `main` then test:
```
GET http://localhost:3000/api/blog/how-we-built-stf-backend
```

And tags should now return three values:
```
GET http://localhost:3000/api/blog/tags
