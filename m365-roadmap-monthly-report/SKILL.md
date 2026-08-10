---
name: m365-roadmap-monthly-report
description: |-
  Generate and automatically save a polished monthly Microsoft 365 Roadmap release report as Markdown for all items with activity during the current month.

  Use when the user says:
    - "create this month’s M365 roadmap report"
    - "show this month’s Microsoft 365 releases"
    - "generate the Microsoft 365 Roadmap highlights for this month"
    - "make a monthly M365 roadmap executive report"
---
# Microsoft 365 Roadmap monthly report

## When to use
Use this skill when the user asks for a current-month Microsoft 365 Roadmap release report, monthly Microsoft 365 roadmap highlights, or an executive summary of Microsoft 365 releases, previews, targeted releases, rollout starts, or rollout completions.

## Inputs
- Current date/month: determine automatically at run time. Do not hardcode dates.
- Source: official Microsoft 365 Roadmap.
- Scope: include every Microsoft 365 roadmap item with Current, Preview, Targeted Release, General Availability, rollout start, or rollout completion dates during the current month.
- Save location: if the user specifies a SharePoint library/folder, use it. Otherwise save the report as a Markdown file in the current site’s Documents library root.

## Steps
1. Determine the current month and year automatically.
2. Search the official Microsoft 365 Roadmap for all Microsoft 365 items with any roadmap activity during the current month, including:
   - 👀 Current
   - 🧪 Preview
   - 🎯 Targeted Release
   - ✅ General Availability
   - 🚀 Rollout Start
   - 🏁 Rollout Completion
3. Do not limit results to items that begin releasing this month. Include items with rollout completion, rescheduled, delayed, renamed, or other milestone activity during the month.
4. Exclude duplicate roadmap entries. If the same roadmap ID has multiple milestones during the month, include each milestone as a separate row and explain what changed.
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
6. Group items into logical categories. Use these categories when applicable, and omit categories with no results:
   - 💬 Microsoft Teams
   - 📄 SharePoint
   - ☁️ OneDrive
   - 📧 Outlook
   - 🤖 Microsoft 365 Copilot
   - 🧩 Power Platform
   - 🛡️ Admin, Security, Compliance & Governance
   - 📱 Microsoft 365 Apps
   - 📊 Other Microsoft 365 Services
7. Add an appropriate emoji to each category and product/app.
8. Sort the full table by category, then release date.
9. Identify the five most significant announcements. Mark them with ⭐ in both the highlights section and the Feature column.
10. If a release date is estimated, delayed, missing, or unclear, label it clearly. Do not guess.
11. Do not invent dates, categories, release phases, audiences, licensing details, descriptions, or roadmap links.
12. Build the final report in Markdown using the Output format below.
13. Automatically save the Markdown report using `create_file`:
    - File name: `M365 Roadmap Monthly Report - <Month YYYY>.md`
    - File content: the complete Markdown report.
    - Destination: user-specified SharePoint library/folder, or the current site’s Documents library root if unspecified.
14. Return a brief confirmation with the created file link. If useful, also include the report body in chat.
15. If search, source access, or file creation fails, say so plainly and do not invent roadmap content or claim the file was saved.

## Output format
Return clean Markdown suitable for a live executive demonstration and save the same Markdown as a `.md` file.

Begin the report exactly with:

# 🚀 This Month’s Microsoft 365 Highlights

Then include the five most significant Microsoft 365 announcements. Mark each with ⭐ and briefly explain why it matters in plain English.

Then present the full results in this table:

| Category | Feature | Roadmap ID | Product / App | Release Phase | Release Date | What It Does | Who It Affects | Roadmap Link |
|----------|---------|------------|---------------|---------------|--------------|--------------|----------------|--------------|

Use concise, plain-English summaries. Highlight the five most important features with a ⭐ in the Feature column.

After the table, include:

## 👀 What Admins Should Watch

Summarize practical takeaways for:
- Microsoft 365 administrators
- Adoption and change-management teams
- Governance and compliance leads
- Help desk and support teams
- Business owners preparing communications or training

Focus on:
- 🔑 Licensing implications
- ⚙️ Required configuration
- 📅 Rollout timing
- 👥 End-user impact
- 🛡️ Governance and compliance considerations
- 📚 Documentation updates
- ✅ Readiness recommendations

Finish with:

## 📌 Roadmap Snapshot

Include these bullets:
- 📦 Total Microsoft 365 roadmap items found
- 🧪 Preview items
- 🎯 Targeted Release items
- ✅ General Availability items
- 🚀 Rollout Start items
- 🏁 Rollout Completion items
- ⚠️ Items with estimated, delayed, missing, or unclear dates

After saving, respond with:
- Saved report: `[file name](file URL)`
- Any caveats about source access, unclear dates, or estimated release timing.

## Quality checks
Before responding, verify:
- The current month was determined dynamically.
- Every row has an official roadmap link.
- Duplicate roadmap entries were removed unless separate milestones occurred during the month.
- Categories with no results were omitted.
- No dates, phases, audiences, licensing details, or descriptions were guessed.
- Snapshot counts match the table.
- The Markdown file was created successfully before saying it was saved.
