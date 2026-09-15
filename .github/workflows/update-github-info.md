---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read

tools:
  github:
    toolsets: [repos]
  web-fetch:
  edit:

network:
  allowed: [github.blog, github.com, awesome-copilot.github.com]

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: true
---

# Update GitHub Info

Keep the GitHub Info website content current and useful for Mona.

## Instructions

1. Use the GitHub repository API tools to read `notes/mona-notes.md` and the current `site/content/github-info.md`. Do not use terminal, CLI, or sandboxed shell commands to read repository guidance or reference files.
2. Use web-fetch to read:
   - https://github.blog/latest/
   - https://github.blog/changelog/
  - https://awesome-copilot.github.com/workflows/
3. Identify only recent, useful updates that fit Mona's editorial angle. Keep summaries short and practical, prefer guidance that helps developers learn GitHub faster, and preserve official source links for claims from the GitHub Blog or GitHub Changelog.
4. Use the edit tool to update `site/content/github-info.md` with accurate, concise content based on the repository notes and fetched sources. Preserve the existing structure and do not change unrelated files.
5. Review the resulting diff for accuracy, source links, scope, and clear writing. If there is no meaningful update, do not make a speculative change and do not open a pull request.
6. When a meaningful update is ready, use the `create-pull-request` safe output exactly once. Open a pull request for Mona to review, with a concise title and body summarizing the updates and citing the source URLs. Do not write directly to the default branch and do not push manually.