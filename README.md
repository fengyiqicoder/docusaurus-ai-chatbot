# How to add an AI chatbot to a Docusaurus site

A plain Docusaurus site (the classic template, nothing else changed) with an **Ask AI** box that answers from the docs and links to the pages it used. No backend, no plugin to install.

Live site: https://fengyiqicoder.github.io/docusaurus-ai-chatbot/

## How it was added

Two small changes.

**1. `docusaurus.config.js`: load the script**

```js
scripts: [
  {
    src: 'https://onetagai.com/ask-docs.js',
    async: true,
    'data-key': 'YOUR_ONETAG_KEY',
  },
],
```

**2. `package.json`: build a search index after the site**

```json
"build": "docusaurus build && npx -y pagefind --site build"
```

[Pagefind](https://pagefind.app) writes a static full-text index into `build/pagefind/`. When a reader asks a question, the script searches that index in the browser, picks the passages that match, and sends them with the question to [OneTag AI](https://onetagai.com). Nothing is crawled and nothing runs on a server of yours.

Then build and deploy the way you already do (`npm run build`, then GitHub Pages, Netlify, Vercel, anything static).

## The key

A OneTag AI key is free: enter your email on [onetagai.com](https://onetagai.com), no card. It comes with 1,000,000 free tokens. The key is public by design, so it is safe to commit. This repo uses a shared demo key; use your own on a real site.

Guide: https://onetagai.com/guides/ask-the-docs
