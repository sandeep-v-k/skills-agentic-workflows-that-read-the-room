---
name: update-github-info
description: Keep the GitHub Info content current with practical, source-backed updates.
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

model: gpt-5-mini

tools:
  github:
    toolsets: [repos]
  web-fetch:
  edit:

network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: true
    max: 1
---

# Update GitHub Info

Maintain the site's GitHub information page with concise, practical updates for developers.

## Sources and repository reading

1. Read `notes/mona-notes.md` with the GitHub repository API tools. Use those notes as editorial guidance.
2. Read the current `site/content/github-info.md` with the GitHub repository API tools before changing it.
3. Web fetch `https://github.blog/latest/`, `https://github.blog/changelog/`, and `https://awesome-copilot.github.com/workflows/` with the `web-fetch` tool.
4. Use relevant, official items from the GitHub Blog, GitHub Changelog, and Awesome Copilot workflows source. Preserve useful existing content and avoid repeating items that are already covered.
5. Do not use terminal, CLI, bash, or other sandboxed commands to read repository guidance or reference files. Use the GitHub repository API tools for those reads.

## Editing and pull request

1. Update only `site/content/github-info.md` using the `edit` tool.
2. Keep summaries short and practical, with an emphasis on helping developers learn GitHub faster.
3. Include the official source link for every Blog or Changelog update.
4. Review the resulting diff for accuracy, clarity, and unnecessary churn.
5. Create one draft pull request with the `create-pull-request` safe output for Mona to review. Use a concise title and explain which official sources informed the update.
6. Do not write directly to `main`, push changes manually, or use any unsafe GitHub write operation.
7. If no meaningful update is available, do not change files and call the configured safe-output completion tool with a brief explanation.
