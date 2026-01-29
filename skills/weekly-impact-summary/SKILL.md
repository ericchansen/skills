---
name: weekly-impact-summary
description: Generate evidence-based weekly impact summaries focused on measurable business outcomes. Use when the user asks to create, generate, or write their weekly summary, weekly update, weekly report, impact summary, or accomplishments for their manager/boss. Also use when the user mentions preparing status updates or reviewing their week's work.
---

# Weekly Impact Summary

Generate factual, evidence-based weekly impact summaries that focus on measurable business outcomes rather than activity lists or meeting attendance.

## Process

### 1. Gather Evidence via WorkIQ

Query WorkIQ to collect factual information about the user's week:

**Query 1 - Overall Accomplishments:**
"What are my key accomplishments, contributions, and impact this week? Include projects I've worked on, meetings I've participated in, deliverables I've completed, and significant communications or decisions I've been involved with."

**Query 2 - Specific Evidence:**
"What specific customer or technical blockers did I help resolve this week? What revenue, deals, or consumption metrics was I involved with? What concrete deliverables did I create or contribute to?"

**Query 3 - Verification (as needed):**
"For [specific claim], provide specific Teams message links and clarify my actual role or contribution. Provide links to referenced documents or spreadsheets."

### 2. Apply Impact Framework

Transform activities into impact statements using this hierarchy:

**Primary Impact (highest priority):**
- Revenue/Consumption: ACR growth, deal acceleration, MACC/ACO progress, capacity unblocked
- Customer Blockers Removed: What was blocked → What you did → What outcome was enabled
- Product Improvements: Feedback that drove feature changes or prioritization

**Secondary Impact:**
- Team Enablement: Reusable artifacts, patterns, or knowledge that unblocks others
- Risk Mitigation: Prevented escalations or technical failures

**Exclude (not impact):**
- Meeting attendance without outcome
- Being "included on threads" without contribution
- Passive participation

### 3. Verify Every Claim

**Critical Rule: Only include claims with evidence.**

For each impact statement, verify:
- ✅ Have a link? (Teams message, email, document, recording)
- ✅ Can describe YOUR specific contribution? (not just awareness)
- ✅ Measurable outcome or concrete deliverable?

If any answer is NO:
1. Query WorkIQ again to find evidence, OR
2. Downgrade the claim (e.g., "Contributed to discussion" instead of "Led initiative"), OR
3. Remove it entirely

### 4. Format Output

Structure the summary as follows:

```markdown
**Weekly Impact Summary – Week of [dates]**

**[Category 1: e.g., "IBM Account Growth"]**
- [Specific contribution with measurable outcome] [Link]
- [Your actual role - be honest about participation level]
- _Impact: [What this enabled/prevented/accelerated]_

**[Category 2: e.g., "Customer Problem-Solving"]**
- [Blocker description] → [What you did] [Link]
- _Impact: [Outcome enabled]_

**[Category 3: e.g., "Team Enablement"]**
- [Deliverable created] - [How it helps others] [Link]
- _Impact: [Efficiency/quality improvement]_

**Professional Development**
- [Learning activities relevant to current work]

**Next Week Priorities**
- [3-5 forward-looking items]
```

Keep output to one page or less. All links should be clickable for manager follow-up.

## Core Principles

**Evidence-Based**
- Never claim credit without verifiable links
- If WorkIQ can't find evidence, don't include it
- Be explicit about your role: "attended," "contributed," "led," "created"

**Impact-Focused**
- Lead with outcomes, not activities
- Meetings only count if they produced decisions or outcomes
- Transform "Participated in 3 meetings" → "Unblocked capacity issue enabling $X deployment"

**Conservative**
- Understate rather than overstate
- Credit others appropriately for team contributions
- Clarify your actual role in ambiguous situations, or omit

**Honest About Ramping**
- Acknowledge when you're learning or new to something
- "Contributed to discussions" is honest and valuable
- Building relationships and context IS impact during onboarding

## What to Avoid

❌ **Vague claims:** "Advanced IBM execution" (What specifically?)
❌ **Meeting lists:** "Attended 5 meetings totaling 8 hours" (List outcomes, not attendance)
❌ **False credit:** "Tracked 3 new opportunities" (when you were just cc'd)
❌ **Unverifiable metrics:** "Influenced $2M in pipeline" (without documented evidence)

## Example

**Before (Activity-Focused):**
```
- Attended 3 IBM meetings this week (5 hours)
- Participated in PTEP review covering GitHub, marketplace, migrations
- Was included on email about new opportunities
```

**After (Impact-Focused):**
```
**IBM Account Execution**
- Participated in 2-hour PTEP review that defined H2 execution plan with
  specific ownership for GitHub adoption, marketplace tactics, and migration
  priorities [Link: Teams meeting]
- _My role: Attended and contributed to alignment discussions_
- _Impact: Clarity on H2 priorities and ownership_
```

## Usage Notes

- Run weekly, ideally Thursday or Friday
- Save output to session files/ for historical tracking
- Use WorkIQ skill to query Microsoft 365 data
