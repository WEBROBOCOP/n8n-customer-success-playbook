# n8n Customer Success Playbook

n8n workflows that help a Customer Success Manager (CSM) keep an enterprise portfolio healthy. Every project starts with a one-page plan (problem, one-sentence solution, five questions about the flow) before anything is built. All data in this repo is **sample data**.

---

## Project 1: Customer Health Monitor

![Workflow canvas](workflow-canvas.png)

### 1 · Problem
*What goes wrong today? For whom? How often?*

A CSM managing around 30 enterprise accounts can't watch every usage dashboard every day. Falling usage, silent teams and piling-up tickets get noticed too late, often just before renewal.

### 2 · Solution in one sentence
*When [trigger], then [result] should happen for [whom], so that [benefit].*

> When the weekday schedule runs, then a diagnosis and a draft check-in email should be created for the CSM, so that at-risk accounts get attention early.

### 3 · Sketch: five questions about the flow

| Step | Question | Answer |
|---|---|---|
| **Start** | What triggers the flow? | Schedule trigger (manual trigger in this demo) |
| **In** | What data arrives? Which fields? | Company, executions (last 30 days vs the previous 30), active users, days since last login, open tickets |
| **Do** | What happens to the data? | Each account gets a score out of 100. Healthy accounts are filtered out. Claude writes a diagnosis and a check-in email for the rest |
| **Out** | What comes out at the end? | One alert email per at-risk account with diagnosis, subject line and draft email |
| **Human** | Who looks at it before anything goes out? | The CSM reviews and decides. Nothing is sent to the customer automatically |

### How the health score works
Each account starts at 100 points and loses points for four signals:

| Signal | Why it matters |
|---|---|
| Usage change vs the previous 30 days | A big drop often means the product is losing its place in daily work |
| Days since last login | Long silence suggests the champion left or priorities shifted |
| Active users | Few users means the account depends on one or two people |
| Open support tickets | Unresolved friction is a leading churn signal |

**Healthy** is 75 or above, **Watch** is 50 to 74, **At risk** is below 50. Only accounts that are not Healthy go to Claude.

### Example output
![Sample alert email](sample-alert-email.png)

### How I'd explain this to a customer
"We look at how your team uses n8n each month. If activity drops or tickets stay open, we notice early and reach out to help before it becomes a problem. You get proactive support instead of waiting for something to break."

### Setup
1. Import `Customer Health Monitor.json` into n8n (menu, **Import from file**).
2. Connect your own Anthropic and Gmail credentials.
3. Set the recipient in the Gmail node (it is `csm@example.com` here).
4. Click **Execute workflow**.

### Next steps
- Connect real product usage data instead of sample accounts
- Tune the thresholds with CSM feedback
- Log outcomes to measure which alerts led to saved accounts

---

## Roadmap
- 02 Customer onboarding kit 
- 03 QBR and ROI report generator
- 04 Renewal and expansion radar
