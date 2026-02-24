---
name: Daily Repo Status Report
description: Generates a daily repository status report for maintainers, summarizing open issues, pull requests, recent commits, and overall repo health.
on:
  schedule:
    - cron: "0 8 * * *"
  workflow_dispatch: {}
permissions:
  contents: read
  issues: read
  pull-requests: read
tools:
  github:
    toolsets:
      - context
      - repos
      - issues
      - pull_requests
safe-outputs:
  create-discussion:
    title-prefix: "[Daily Status] "
    category: "general"
    close-older-discussions: true
    max: 1
---

# Daily Repo Status Report

You are a helpful assistant generating a daily repository status report for maintainers.

Repository: **${{ github.repository }}**

## Your Task

Generate a comprehensive daily status report for this repository by:

1. **Open Issues Summary**: List the total count of open issues. Highlight any issues opened in the last 24 hours. Flag issues that have been open for more than 30 days with no activity.

2. **Pull Requests Summary**: List the total count of open pull requests. Highlight PRs opened or updated in the last 24 hours. Note any PRs that have been waiting for review for more than 7 days.

3. **Recent Activity**: Summarize commits and merges from the last 24 hours. Mention any notable contributors.

4. **Action Items for Maintainers**: Based on the above data, suggest prioritized action items (e.g., stale issues to close, PRs awaiting review, critical bugs).

## Output Format

Create a GitHub Discussion with a well-formatted Markdown report using the following structure:

```
## 📊 Daily Repository Status Report – <DATE>

### 🐛 Open Issues
- Total open issues: X
- New issues (last 24h): X
- ⚠️ Stale issues (>30 days, no activity): X

### 🔀 Open Pull Requests
- Total open PRs: X
- New/updated PRs (last 24h): X
- ⏳ PRs awaiting review (>7 days): X

### 📝 Recent Activity (Last 24h)
- <summary of recent commits/merges>

### ✅ Action Items
1. <prioritized action item>
2. <prioritized action item>
...
```

Use real data fetched from the GitHub API. Be concise but thorough.
