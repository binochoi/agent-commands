---
description: Research a topic across the web and this codebase
allowed-tools: WebSearch, WebFetch, Read, Grep, Glob
---

Topic: $ARGUMENTS

Investigate the topic using both web sources and this codebase.

Rules:
- Do not ask clarifying questions. State any assumption inline and proceed.
- Prefer primary sources: official documentation, specifications,
  source repositories. Treat blog posts as secondary.
- Search the codebase for existing usage before recommending anything new.
- Output in this order: conclusion first, then supporting findings as
  bullets, then open questions, then a source list with URLs.
- Mark anything you could not verify as unverified.
- Keep the whole response under 400 words unless the topic demands more.
