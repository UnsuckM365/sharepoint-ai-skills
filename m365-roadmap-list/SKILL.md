---
name: m365-roadmap-list
description: |-
  Generate Microsoft 365 Roadmap items for the current month and save each roadmap item as a row in a SharePoint list instead of a Markdown report.

  Use when the user says:
    - "save this month’s M365 roadmap to a list"
    - "create a Microsoft 365 roadmap list"
    - "show this month’s Microsoft 365 releases in a SharePoint list"
    - "generate the M365 roadmap items as list rows"
---
# Microsoft 365 Roadmap list

## When to use
Use this skill when the user asks for current-month Microsoft 365 Roadmap items to be captured in a SharePoint list, including previews, targeted releases, general availability, rollout starts, rollout completions, or other roadmap activity during the month.

## Inputs
- Current date/month: determine automatically at run time. Do not hardcode dates.
- Source: official Microsoft 365 Roadmap.
- Scope: include every Microsoft 365 roadmap item with Current, Preview, Targeted Release, General Availability, rollout start, rollout completion, rescheduled, delayed, renamed, or other milestone activity during the current month.
- Destination list: if the user specifies a SharePoint list, use it. Otherwise create or update a list named `M365 Roadmap - <Month YYYY>` in the current site.

## Steps
1. Determine the current month and year automatically.
2. Search the official Microsoft 365 Roadmap for all Microsoft 365 items with any roadmap activity during the current month, including:
   - 👀 Current
   - 🧪 Preview
   - 🎯 Targeted Release
   - ✅ General Availability
   - 🚀 Rollout Start
   - 🏁 Rollout Completion
3. Do not limit results to items that begin releasing this month. Include rollout completion, rescheduled, delayed, renamed, or other milestone activity during the month.
4. Exclude duplicate roadmap entries. If the same roadmap ID has multiple milestones during the month, include each milestone as a separate list row and explain the milestone in `Milestone Notes`.
5. For each item, capture:
   - Category
   - Feature name
   - Roadmap ID
   - Product / app
   - Release phase
   - Release date
   - Plain-English summary of what it does
   - Who it affects
   - Official Microsoft 365 Roadmap URL
   - Milestone notes
   - Importance marker for the five most significant items
6. Group items into logical categories. Use these categories when applicable:
   - Microsoft Teams
   - SharePoint
   - OneDrive
   - Outlook
   - Microsoft 365 Copilot
   - Power Platform
   - Admin, Security, Compliance & Governance
   - Microsoft 365 Apps
   - Other Microsoft 365 Services
7. Identify the five most significant announcements and mark `Top Highlight` as Yes for those rows.
8. If a release date is estimated, delayed, missing, or unclear, label it clearly in `Date Status`. Do not guess.
9. Do not invent dates, categories, release phases, audiences, licensing details, descriptions, or roadmap links.
10. Create or update the destination SharePoint list using `create_or_update_list` with these columns:
    - Title: single line text; use the feature name.
    - Category: choice.
    - Roadmap ID: single line text.
    - Product / App: single line text.
    - Release Phase: choice.
    - Release Date: date/time when a valid date exists; leave blank if missing or unclear.
    - Date Status: choice; values: Confirmed, Estimated, Delayed, Missing, Unclear.
    - What It Does: multiple lines text.
    - Who It Affects: multiple lines text.
    - Roadmap URL: hyperlink.
    - Milestone Notes: multiple lines text.
    - Top Highlight: yes/no.
    - Report Month: single line text using `<Month YYYY>`.
11. Add one list item per roadmap item or milestone using `create_list_items_v2`.
12. If updating an existing list, avoid duplicate rows by checking existing items first. Treat `Roadmap ID` + `Release Phase` + `Release Date` + `Milestone Notes` as the duplicate key.
13. Return a brief confirmation with:
    - List name
    - Number of rows created
    - Number of duplicates skipped, if any
    - Any caveats about source access, unclear dates, or estimated release timing
14. If search, source access, list creation, or item creation fails, say so plainly and do not invent roadmap content or claim rows were saved.

## Output format
Return a concise confirmation, not a Markdown executive report.

Use this format:

Saved Microsoft 365 Roadmap items to SharePoint list: `<list name>`

- Rows created: `<count>`
- Duplicates skipped: `<count>`
- Top highlights marked: `5` or fewer if fewer than five items were found
- Caveats: `<source/date/save caveats>`

## Quality checks
Before responding, verify:
- The current month was determined dynamically.
- Every saved row has an official roadmap link.
- Duplicate roadmap entries were removed unless separate milestones occurred during the month.
- No dates, phases, audiences, licensing details, or descriptions were guessed.
- The SharePoint list exists before creating items.
- List rows were created successfully before saying they were saved.
