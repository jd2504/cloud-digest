# eventually consistent

Briefings for cloud and AI architects and engineers, in two topics:

| Topic | Schedule (US Eastern, mornings) | Content folder | Archive | Feed |
|---|---|---|---|---|
| Cloud Digest | Mondays and Thursdays | `content/cloud/` | `/cloud/` | `/cloud/feed.xml` |
| AI Digest | Tuesdays and Fridays | `content/ai/` | `/ai/` | `/ai/feed.xml` |

Issues are written by Claude scheduled tasks, one per topic, committed here as Markdown, built with [Hugo](https://gohugo.io/) and deployed to Firebase Hosting by GitHub Actions.

- Site: the newest issue from either topic on the home page, with a card for each topic's latest issue; topic archives at `/cloud/` and `/ai/`; tags at `/tags/`
- Feeds: `/feed.xml` (both topics, full text), `/cloud/feed.xml` and `/ai/feed.xml` (one topic), `/tags/<tag>/feed.xml` (one tag, both topics)
- Old `/digests/` URLs, including `/digests/feed.xml`, redirect to `/cloud/` (see `firebase.json`)

## One-time setup

1. **Firebase project.** In the [Firebase console](https://console.firebase.google.com/), add Firebase to your GCP project (or create one). Hosting is enabled on first deploy.
2. **Service account key.** In GCP IAM, create a service account with the *Firebase Hosting Admin* role (plus *API Keys Viewer* if the deploy asks for it), create a JSON key, and add the whole JSON as a repository secret named `FIREBASE_SERVICE_ACCOUNT` (Settings → Secrets and variables → Actions → Secrets).
   Running `firebase init hosting:github` locally does this step for you.
3. **Repository variables** (Settings → Secrets and variables → Actions → Variables):
   - `FIREBASE_PROJECT_ID`: your project ID, e.g. `my-project-123`
   - `SITE_URL`: the public URL with a trailing slash, e.g. `https://my-project-123.web.app/` or your custom domain
4. **Claude write access.** Install the [Claude GitHub App](https://github.com/apps/claude/installations/select_target) on this repo so the scheduled task can push new issues.
5. Push to `main` or run the workflow manually (Actions → *Build and deploy* → Run workflow).

Custom domain: Firebase console → Hosting → Add custom domain, then update `SITE_URL`.

## Issue format

Each issue is one file in its topic's folder, named by date: `content/cloud/YYYY-MM-DD.md` or `content/ai/YYYY-MM-DD.md`. The folder decides the topic; no extra front matter is needed.

```markdown
---
title: "Cloud Digest: Monday, November 16, 2026"   # or "AI Digest: Tuesday, November 17, 2026"
date: 2026-11-16T07:35:00-05:00
tags: [aws, kubernetes, finops]
summary: "One sentence naming the issue's main theme."
---

## Provider announcements

### AWS

**Headline naming the product.** Status, availability and pricing, and why it matters. ([AWS](https://example.com))

## Industry news

**Headline in one line.** What happened and why it matters. ([Outlet](https://example.com))

## Architecture & design patterns

### Title of paper or post
*Source*: plain-language summary. **When to use it:** one line.

## Takeaway

One short paragraph.

## Sources

- [Title — Outlet](https://example.com)
```

Each topic's sections, sources and tag set are defined in its brief (kept in the Claude project, and copied into its scheduled task). Tags are lowercase and hyphenated and shared across topics, so a tag such as `ai-infrastructure` or `regulation` lists issues from both.

## Adding a topic

1. Create `content/<slug>/_index.md` with `title`, `label` (the short topic label shown on issues), `schedule` and `description`.
2. Add the slug to `mainSections` in `hugo.toml` and a menu entry.
3. Add a scheduled task that writes issues to `content/<slug>/`.

## Local preview

```sh
hugo server
```

Then open http://localhost:1313/.
