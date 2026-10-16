# Scope Docs

Source for [docs.canvascope.org](https://docs.canvascope.org), the help site for every
Scope app: the Chrome extension, Lectra for iPad, and Polya. Built with
[Mintlify](https://mintlify.com).

## Preview locally

You need Node.js 20 or later.

```bash
npx mint dev
```

The site opens at `http://localhost:3000` and reloads when you save a file.

Before you push, run the checks:

```bash
npx mint validate       # build errors and warnings
npx mint broken-links   # internal links that point nowhere
```

## Layout

| Path | What it holds |
|---|---|
| `docs.json` | Site settings, theme, colors, and the sidebar navigation |
| `index.mdx` | Home page |
| `get-started/` | What Scope is, quickstart, accounts, privacy |
| `chrome/` | The Scope extension for Chrome |
| `lectra/` | Lectra for iPad, plus Lectra for Mac and Lectra Receiver |
| `polya/` | Polya, the course tutor at askpolya.com |
| `resources/` | Help, troubleshooting, FAQ, glossary, release notes, legal |
| `images/` | Screenshots, one folder per section |
| `logo/`, `favicon.svg` | Brand marks for light and dark mode |

A page appears in the sidebar only when its path is listed under `navigation` in
`docs.json`.

## Writing rules

- Write in the style of Google's developer documentation: lead with the point, use
  "you", active voice, short sentences, and sentence-case headings.
- Don't write "simply", "just", "easily", "please", or exclamation marks.
- Bold the exact on-screen label for anything the reader taps or clicks. Chain menu
  paths with `>`: **Settings** > **Account**.
- Describe what a feature does for the reader, not how it's built. Leave out
  infrastructure, vendors, and internal names.
- Document only what ships in the released apps. If a feature has a limit, say so
  in a `<Note>`.
- In MDX, a bare `<` or `{` in prose breaks the build. Use `&lt;` or code font.

## Deploy

Mintlify deploys from the `main` branch of `hqscope/docs`.

1. In the [Mintlify dashboard](https://dashboard.mintlify.com), connect the
   `hqscope/docs` GitHub repository.
2. In **Settings** > **Custom domain**, add `docs.canvascope.org`.
3. At the DNS host for `canvascope.org`, add the two TXT records the dashboard
   shows (`_acme-challenge` and `_cf-custom-hostname`). Wait until both show as
   verified.
4. Add a `CNAME` record: name `docs`, value `cname.mintlify.builders`.

Don't add the CNAME before the TXT records verify, or HTTPS can fail.
