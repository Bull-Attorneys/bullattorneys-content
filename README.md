# Bull Attorneys — Content Repository

This repository is for **blog content only**. You submit JSON files with text, metadata, and schema. The development team handles all code, routing, images, and deployment.

---

## How to submit a blog

1. **Create a branch** from `main` — name it after the slug, e.g. `blog/car-accident-checklist-wichita`
2. **Add your JSON file** inside `locales/en/blogs/` — filename must match the slug exactly: `car-accident-checklist-wichita.json`
3. **Open a pull request** against `main` with a short description of the topic
4. The dev team reviews and merges — they will create the page, handle images, and deploy

Spanish (`es`) versions are optional and can be submitted separately in a follow-up PR under `locales/es/blogs/`.

---

## Slug rules

The slug becomes the live URL: `bullattorneys.com/blogs/your-slug-here/`

- Lowercase only
- Words separated by hyphens (`-`), no underscores or spaces
- No special characters (`& / ? # %`)
- Be descriptive — include the primary keyword
- Keep it under 70 characters

**Good:** `how-long-do-i-have-to-file-a-car-accident-claim-kansas`
**Bad:** `Blog_Post_#4`, `new-blog`, `car-accident`

---

## Two content formats

Blogs on this site use one of two structures depending on the content type. Use the template that matches what you're writing.

### Format A — Q&A / FAQ style
Use when the blog answers a series of questions. Each section has a heading (the question) and one or more paragraphs as the answer. See: `templates/blog-qa-format.json`

**Best for:** "What should I do after a car accident?", "How long do I have to file a claim?", guide-style posts.

### Format B — Long-form article style
Use when the blog presents research, data, or an extended argument with subsections. Sections can include bullet lists, nested subheadings, and images. See: `templates/blog-article-format.json`

**Best for:** Statistics posts, deep-dives, trend reports, multi-section analysis.

---

## Fields reference

### Fields common to both formats

| Field | Required | Notes |
|---|---|---|
| `metadata.title` | Yes | Page `<title>` tag — max 60 characters, include primary keyword |
| `metadata.description` | Yes | Meta description — 140–160 characters, written for click-through |
| `metadata.canonical` | Yes | Full URL: `https://bullattorneys.com/blogs/your-slug/` |
| `metadata.datePublished` | Yes | ISO format: `2026-07-15T00:00:00-05:00` |
| `metadata.dateModified` | Yes | Same as datePublished on first submission |
| `hero.date` | Yes | Display date: `JULY 15, 2026` |
| `hero.title` | Yes | The H1 headline shown on the page — can differ from meta title |
| `authorSection` | Yes | Leave as-is from template — dev team fills in |
| `schema.headline` | Yes | Usually same as `hero.title` |
| `schema.description` | Yes | Usually same as `metadata.description` |
| `schema.articleSection` | Yes | Array of topic tags, e.g. `["Car Accidents", "Kansas Law"]` |
| `schema.keywords` | Yes | 5–10 keyword phrases, long-tail preferred |
| `schema.about` | Yes | Array of `{ "@type": "Thing", "name": "Topic Name" }` objects |
| `schema.articleBody` | Yes | 2–4 sentence plain-text summary of the article (no HTML) |
| `legalDisclaimer` | Yes | Leave exactly as shown in template — do not change |

### Format A additional fields

| Field | Required | Notes |
|---|---|---|
| `content.featuredImage.src` | Yes | Dev team fills this in — leave as shown in template |
| `content.practiceAreaButtons` | Yes | Which practice area buttons to show — see template options |
| `content.sections` | Yes | Array of Q&A sections — see format below |

Each section in Format A:
```json
{
  "heading": "The question as a heading",
  "intro": [
    "First paragraph as a string.",
    "Second paragraph — each paragraph is a separate string in the array."
  ],
  "items": []
}
```

### Format B additional fields

| Field | Required | Notes |
|---|---|---|
| `content.sections` | Yes | Array of article sections — see format below |
| `content.images` | If using images | Array of `{ "src": "...", "alt": "..." }` — dev team fills src, you write alt text |
| `schema.alternativeHeadline` | Recommended | A shorter alternative headline for schema |
| `schema.mentions` | Recommended | External sources cited — array of `{ "@type": "WebPage", "name": "...", "url": "..." }` |

---

## HTML in content strings

You may include limited HTML inside content strings for links and emphasis only.

**Allowed:**
```
<a href="/practice-areas/car-accidents/" class="text-green-700 hover:text-green-800 no-underline hover:underline">Car Accident Lawyers</a>
<strong>bold text</strong>
```

**For internal links** — use relative paths starting with `/`
**For external links** — always add `target="_blank" rel="noopener noreferrer"`

**Not allowed:** `<div>`, `<p>`, `<h2>`, `<script>`, `<style>`, or any structural or scripting tags.

---

## What the dev team handles

Do not include or attempt to specify any of the following — they are outside the scope of this repo:

- Image files and image URLs (you write the `alt` text only)
- Page routing and Next.js page components
- Sitemap updates
- Spanish translations (submit separately if available)
- Deployment and caching

---

## Questions

Open a GitHub issue in this repository with your question. Do not contact the dev team directly for content questions — keep all discussion in GitHub so there is a record.
