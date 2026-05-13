
---

## 📄 `docs/setup-guide.md`

```markdown
# 🛠️ Complete Setup Guide

Follow these steps to deploy the **Slack → PRD → Jira Automator** in under 10 minutes. All tools used have generous free tiers.

---

## ✅ Prerequisites Checklist
- [ ] [Slack Workspace](https://slack.com) (Free)
- [ ] [Jira Cloud Site](https://www.atlassian.com/software/jira/free) (Free, up to 10 users)
- [ ] [Groq API Key](https://console.groq.com) (Free, ~30 RPM)
- [ ] [Pipedream Account](https://pipedream.com) (Free, 1,000 runs/mo)
- [ ] Basic familiarity with Slack apps & REST APIs

---

## 🟦 Step 1: Create & Configure Slack App

1. Go to [api.slack.com/apps](https://api.slack.com/apps) → **Create New App** → **From scratch**
2. Name: `PRD Automator` → Select your workspace
3. **Event Subscriptions**:
   - Toggle **Enable Events** → ON
   - Request URL: Leave blank for now (Pipedream handles this via OAuth)
   - Subscribe to bot events → Add: `reaction_added`
4. **OAuth & Permissions** → Add these **Bot Token Scopes**:
   - `reactions:read`
   - `channels:history`
   - `groups:history`
   - `chat:write`
5. Click **Install to Workspace** → **Allow**
6. Copy the **Bot User OAuth Token** (`xoxb-...`) for later

![Slack App Setup](../demo/slack-app-setup.png)

---

## 🟪 Step 2: Set Up Jira Cloud

1. Create a free site at [jira.atlassian.com](https://www.atlassian.com/software/jira/free)
2. Create a project: **Projects → Create project → Kanban**
3. Note your **Project Key** (e.g., `KAN`, `PROJ`)
4. Generate API Token:
   - Go to [id.atlassian.com/manage-profile/security/api-tokens](https://id.atlassian.com/manage-profile/security/api-tokens)
   - Click **Create API token** → Label: `Pipedream` → Copy token
5. Create Basic Auth string:
   ```bash
   echo -n "your-email@domain.com:your-api-token" | base64