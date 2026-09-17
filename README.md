# Let me ask AI for you

A static, offline “prank” page that looks like the ChatGPT start screen.  
You share a special link; when someone opens it, the page **types a message for them** into the chat box, presses Send, then **opens the real ChatGPT** with that same question already filled in.

**Repo:** [https://github.com/you-in-you/Let-me-ask-AI-for-you](https://github.com/you-in-you/Let-me-ask-AI-for-you)

---

## What it does

1. **Looks like ChatGPT**  
   Dark UI, thin left icon rail, centered “What’s on the agenda today?”, pill-shaped composer with “Ask anything”, Think, and blue send button.

2. **Prank / share flow**
   - You open the page with `#main` (or click **How to use**).
   - You type the message you want the victim to “send”.
   - You get a link like:  
     `index.html#text:BASE64…`
   - When they open that link:
     - The text is typed character-by-character into the box (typing animation).
     - Send is triggered.
     - The browser redirects to the real ChatGPT with the same prompt:  
       `https://chatgpt.com/?q=your+message`  
       so ChatGPT opens with that question ready (or already asked, depending on their session).

3. **Fully static**  
   No backend, no API keys. One HTML file. Works from GitHub Pages, any static host, or `file://`.

---

## How to use

### Build a prank link

1. Open the page with the builder:
   ```
   …/index.html#main
   ```
   Or click **How to use** in the top bar.
2. Enter the text that should be typed and sent.
3. Click **Generate link** → copy the `#text:…` URL (or use **Open preview**).

### What the other person sees

They open the link → typing animation → redirect to:

```
https://chatgpt.com/?q=<encoded message>
```

ChatGPT’s official `?q=` parameter pre-fills the composer with that message.

### Normal chat UI

Without a hash (or after leaving `#main`), the page is just a static lookalike. Typing and pressing Send also redirects to `chatgpt.com/?q=…` with whatever they wrote.

---

## URL fragments

| Hash | Behavior |
|------|----------|
| `#main` | Opens the “How to use” / link builder panel |
| `#text:…` | Decodes the payload, types it into the composer, sends, then redirects to ChatGPT |
| *(none)* | Normal start screen |

Encoding is base64url (UTF-8 safe).

---

## Files

- `index.html` — entire app (UI + logic)
- `README.md` — this file

---

## Notes

- This does **not** send messages to OpenAI by itself. It only mimics the UI and then hands off to the real `chatgpt.com` via `?q=`.
- Favicon is loaded from ChatGPT’s CDN when online; the rest works offline.
- For a cleaner share URL, host `index.html` on GitHub Pages (or any static host) and share that origin + `#text:…`.

---

## License

Use freely for jokes and demos. Don’t use it to phish or mislead people about identity/security.
