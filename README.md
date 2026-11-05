# Cloud Digest

A twice-weekly briefing on cloud computing industry news and research in cloud architecture and design patterns. Issues are written by a Claude scheduled task (Mondays and Thursdays, 7:35 AM US Eastern), committed here as Markdown, built with [Hugo](https://gohugo.io/) and deployed to Firebase Hosting by GitHub Actions.

- Site: latest issue on the home page, archive at `/digests/`, topics at `/tags/`
- Feeds: `/feed.xml` (all issues, full text), `/tags/<tag>/feed.xml` (one topic)

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

Each issue is one file at `content/digests/YYYY-MM-DD.md`:

```markdown
---
title: "Cloud Digest: Monday, November 9, 2026"
date: 2026-11-09T07:35:00-05:00
tags: ["aws", "kubernetes", "finops"]
summary: "One sentence naming the issue's main theme."
---

## Industry news

**Headline in one line.** What happened and why it matters. [Source](https://example.com)

## Architecture & design patterns

### Title of paper or post
*Source* — plain-language summary. **When to use it:** one line.

## Takeaway

One short paragraph.

## Sources

- [Title](https://example.com)
```

Tags are lowercase and hyphenated. Prefer this set so tag pages stay useful: `aws`, `azure`, `google-cloud`, `oracle`, `ibm`, `alibaba`, `gpu-cloud`, `ai-infrastructure`, `kubernetes`, `cloud-native`, `serverless`, `event-driven`, `microservices`, `distributed-systems`, `multi-cloud`, `platform-engineering`, `resilience`, `finops`, `security`, `outages`, `regulation`, `earnings`, `m-and-a`, `data-centers`, `research`.

## Local preview

```sh
hugo server
```

Then open http://localhost:1313/.
