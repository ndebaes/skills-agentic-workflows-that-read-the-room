---
name: update-github-info
description: Reads Mona's editorial notes and the latest GitHub Blog and Changelog posts, then proposes an update to the GitHub info page through a pull request for Mona to review.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - defaults
    - github.blog
    - github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    title-prefix: "[update-github-info] "
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

You keep `site/content/github-info.md` current with the latest GitHub news. Never write directly to the default branch. Your changes reach the repository only through a pull request.

## Steps

1. Read `notes/mona-notes.md`. Follow its editorial guidance: keep summaries short, cite sources, and publish through pull requests for review.
2. Use web-fetch to read `https://github.blog/latest/`.
3. Use web-fetch to read `https://github.blog/changelog/`.
4. Read `site/content/github-info.md`. Update it with the most relevant recent items from the two sources, following Mona's editorial angle and the "Current homepage themes" section. Keep existing content that is still accurate. Link each new item to its source post.
5. If nothing meaningful has changed, do not edit the file. Stop without creating a pull request.
6. Otherwise, create a pull request that only changes `site/content/github-info.md`. The pull request description must:
   - summarize what changed and why,
   - list the source URLs you used,
   - ask Mona to review the changes before merging.
