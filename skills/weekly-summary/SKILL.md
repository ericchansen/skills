---
name: weekly-summary
description: Generate a concise weekly work summary for sharing with your manager. Combines Microsoft 365 data (meetings, emails, chats) with Copilot CLI session logs to show how technical work supports customer accounts. Use when asked for a "weekly summary", "status update", "what I worked on", or "update for my boss".
---

# Weekly Summary Skill

Generate a boss-ready weekly summary that connects customer activity with technical contributions.

## What This Skill Does

1. **Pulls M365 activity** via WorkIQ (meetings, emails, chats, files)
2. **Scans Copilot CLI session logs** to find what you've been building
3. **Connects the dots** between technical work and customer accounts
4. **Produces a concise summary** suitable for sharing with leadership

## Output Format

The summary should be **SHORT** (fits in one screen) and **actionable**:

```markdown
# Weekly Summary – [Name]
**[Date Range]**

## [Account 1]
- What you did / facilitated / moved forward
- Technical work that supports this account (if any)
- What's coming up

## [Account 2]
...

## Internal / Enablement
- Key meetings attended and takeaways
- Skills/tools built that support multiple accounts

## Next Week
- Upcoming meetings/opportunities
- Planned work
```

## Key Principles

1. **Customer-centric**: Organize by account, not by activity type
2. **Integrated**: Technical building goes WITH the account it supports, not separate
3. **Honest**: If you didn't contribute much to an account, highlight what's coming up instead
4. **Concise**: Your boss doesn't need 5 pages - they need the highlights
5. **Forward-looking**: Always include what's next, especially for accounts with less activity

## Data Sources

### 1. Microsoft 365 (via WorkIQ)
Query for the past 7 days:
- Meetings attended and key outcomes
- Email threads and decisions
- Teams chats and discussions
- Scheduled upcoming meetings

### 2. Copilot CLI Session Logs
Location: `~/.copilot/session-state/`

Scan for:
- `plan.md` files in session directories (show what was being built)
- `events.jsonl` files for intent/activity (what actions were taken)
- `workspace.yaml` for project context

### 3. Session Log Parsing

For each session directory:
1. Check if `plan.md` exists → read the problem statement and current status
2. Look at modification dates to find recent sessions
3. Extract key project names and technologies
4. Match projects to accounts based on context clues

## How to Generate the Summary

### Step 1: Gather M365 Data
```
ask_work_iq: "Summarize my work activity for the past 7 days - meetings attended, key email threads, Teams discussions, and any decisions made. Group by customer/account where possible."
```

### Step 2: Gather Session Logs
```powershell
# Find recent session plan files
Get-ChildItem -Path "$env:USERPROFILE\.copilot\session-state" -Recurse -Filter "plan.md" | 
  Where-Object { $_.LastWriteTime -gt (Get-Date).AddDays(-7) }
```

### Step 3: Connect Technical Work to Accounts

Look for these patterns in session logs:
- Project names that match account names (e.g., "TIBCO", "Citrix")  
- Technologies being discussed in customer meetings
- Demo/POC work that relates to customer asks

### Step 4: Identify Gaps and Upcoming Work
```
ask_work_iq: "What meetings do I have scheduled for next week? What upcoming customer engagements should I prepare for?"
```

### Step 5: Draft Summary

Organize by account. For each:
- **Active work**: What you actually did (facilitated, built, fixed, advised)
- **Technical connection**: Any coding/building that supports this account
- **Coming up**: Scheduled meetings, planned work, opportunities

## Example Output

```markdown
# Weekly Summary – Eric Hansen
**Jan 24-30, 2026**

## Citrix
- Facilitated Azure SRE Agent evaluation sessions
- Assisted with HTTP/2 backend & App Gateway configuration questions
- Helped debug agent behavior with PagerDuty integration
- **Coming up**: Follow-up on feature requests for alert handling

## TIBCO
- Building XML workflow authoring demo (AI agent pipeline for BPEL/BPMN generation)
- Supports Spotfire Copilot conversations with ASML
- **Coming up**: Complete working demo for customer presentation

## NCR
- Scheduled 1:1 with SSP to increase involvement
- **Coming up**: BNZ migration planning sessions

## IBM
- Attended territory cadence calls
- **Coming up**: AI accelerated dev opportunities from morning meeting

## Internal
- Skills Matrix work with Brandon/Jordan - finalizing structure
- Copilot CLI Office Hours - plan mode, skills roadmap
- AI Thirsty Thursday - PostgreSQL for AI apps

## Next Week Priorities
1. Complete TIBCO XML demo
2. NCR SSP 1:1 - scope involvement
3. Follow up on AI accelerated dev opportunities
```

## Tips for Accuracy

- **Don't assume** - if you didn't code something, don't say you did
- **Facilitation counts** - helping customers and unblocking them is valuable work
- **Be specific** - "fixed HTTP/2 config" is better than "helped with technical issues"
- **Highlight momentum** - what moved forward this week?
- **Acknowledge gaps** - "scheduled 1:1 to increase involvement" is honest and forward-looking

---

## PowerPoint Generation

After creating the markdown summary, generate a **single-slide PowerPoint** for sharing with leadership.

### Setup (one-time)
```bash
npm install pptxgenjs
```

### Slide Layout
Single slide with:
- **Dark header bar** with gradient accent strip
- **Title**: "Weekly Summary • [Name] • [Date Range]" in cyan/blue
- **3-column layout**: Internal (left) | Accounts (middle) | Accounts (right)
  - Internal has equal prominence - not hidden at bottom
- **UPCOMING** section at bottom with key meetings and priorities

### Template Script
Use `scripts/create-slides-template.js` as a starting point. Customize the content based on the weekly summary data:

```javascript
const pptxgen = require("pptxgenjs");

const pres = new pptxgen();
pres.layout = "LAYOUT_16x9";

let slide = pres.addSlide();

// Dark header bar
slide.addShape("rect", {
  x: 0, y: 0, w: "100%", h: 1.1,
  fill: { type: "solid", color: "0F1419" }
});

// Accent strip
slide.addShape("rect", {
  x: 0, y: 1.1, w: "100%", h: 0.08,
  fill: { type: "solid", color: "0078D4" }
});

// Title with gradient-style colors
slide.addText([
  { text: "Weekly Summary", options: { color: "00B4D8", bold: true } },
  { text: "  •  [Name]  •  [Date Range]", options: { color: "888888" } }
], {
  x: 0.4, y: 0.35, w: 9.5, h: 0.5,
  fontSize: 24, fontFace: "Segoe UI Light"
});

// 3-column layout:
// col1X = 0.4 (INTERNAL - equal prominence)
// col2X = 3.6 (Accounts: Citrix, TIBCO)
// col3X = 6.8 (Accounts: NCR, IBM)
// startY = 1.4

// INTERNAL column includes:
// - Technical building (e.g., "Built demo web app")
// - Enablement sessions attended

// UPCOMING section at bottom after divider

pres.writeFile({ fileName: "weekly-summary-YYYY-MM-DD.pptx" });
```

### Generation Steps

1. Gather data (Work IQ + session logs)
2. Create markdown summary
3. Generate PowerPoint by:
   - Creating a new JS file with customized content from the template
   - Running `node create-slides.js "weekly-summary-YYYY-MM-DD.pptx"`
4. Output file ready to share

### Design Guidelines
- **Keep it scannable** - one slide means tight, impactful content
- **Account names** in blue headers, bullets in gray
- **"Coming up"** items show forward momentum
- **No fluff** - every word should earn its place
