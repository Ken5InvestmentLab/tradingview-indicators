# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Dev Server

```bash
npx serve . --listen 3000
```

Launch via the configured preview: `preview_start "Static Site (cyberpunk-trade-os)"` (defined in `.claude/launch.json`).

## Site Structure

Pure static HTML/CSS site deployed to GitHub Pages at `https://ken5investmentlab.github.io/cyberpunk-trade-os/`.

```
index.html          ← LP本体（メインランディングページ）
blog/
  index.html        ← 記事一覧
  [slug]/
    index.html      ← 各記事
sitemap.xml
google8b4f3b8ed9a7759a.html   ← 削除禁止（Google Search Console認証）
```

## Link Paths — Critical Rule

All internal links must use **relative paths with explicit `index.html`** (e.g. `blog/index.html`, `../index.html`). Do NOT use:
- Directory-only links like `./blog/` or `/blog/` — causes directory listing locally
- Absolute paths like `/cyberpunk-trade-os/...` — breaks local dev

| From | To root | To blog list | To article |
|------|---------|--------------|------------|
| `index.html` | — | `blog/index.html` | `blog/[slug]/index.html` |
| `blog/index.html` | `../index.html` | — | `[slug]/index.html` |
| `blog/[slug]/index.html` | `../../index.html` | `../index.html` | — |

## Design System

All pages share inline CSS with these variables (no external stylesheet):

```css
--primary: #00f3ff      /* cyan — headings, accents */
--membership: #bd00ff   /* purple — membership CTAs */
--discord: #5865F2      /* blurple — Discord CTAs */
--bg-dark: #050505
--bg-panel: rgba(20, 25, 40, 0.7)
--font-head: 'Orbitron'
--font-body: 'Inter'
```

Background: animated perspective grid via `body::before` + `@keyframes gridMove`. Scroll animations use `.reveal` / `.active` via `IntersectionObserver` — include `pageshow` listener to handle bfcache (browser back button).

## Adding a Blog Article

1. Copy `blog/how-to-stop-hesitating-when-trading/index.html` as the template
2. Required head tags: `<title>`, `<meta name="description">` (≤150 chars), `og:title`, `og:description`, `og:url`, `<link rel="canonical">`
3. Use relative paths for all internal links (see table above)
4. Timestamps: `<time datetime="YYYY-MM-DDTHH:MM:SSZ">YYYY-MM-DD HH:MM UTC</time>`

After adding an article, update these three files:
- `blog/index.html` — add card at top (newest first)
- `index.html` — keep "Latest from the Lab" section showing the 3 newest articles
- `sitemap.xml` — add `<url>` entry

## Brand / Content Rules

- Tone: minimal, confident, no hype (Notion/Linear aesthetic)
- Pain points to address: 迷い (hesitation), ノイズ (noise), 構造のなさ (lack of structure)
- Positioning: Cyberpunk Trade OS = a thinking framework, not just tools
- Forbidden terms: 稼げる, 爆益, 必勝, NISA, 日本株, 仮想通貨
- Target audience: English-speaking TradingView users
- CTA always links to Discord: `https://discord.gg/JNQEbP5gKE`

## SEO Checklist (per article)

- H1 contains main keyword
- Keyword appears naturally in first 100 words
- `<link rel="canonical">` matches the GitHub Pages URL
