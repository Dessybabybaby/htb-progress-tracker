# HTB Progress Tracker - Setup Guide

## Quick Setup (5 minutes)

### Step 1: Find Your HTB User ID

1. Go to your HTB profile: https://app.hackthebox.com/profile
2. Copy the number from URL
3. Example: `https://app.hackthebox.com/profile/123456` → ID = `123456`

---

### Step 2: Import Workflow

1. Download: [htb-tracker-workflow.json](../workflows/htb-tracker-workflow.json)
2. n8n → Import from File

---

### Step 3: Configure User ID

1. Open "Load HTB Profile URL" node
2. Update line:
```javascript
   const htbUserId = '123456';  // YOUR ID HERE
```
3. Save

---

### Step 4: Test Execution

1. Click "Execute Workflow"
2. Check dashboard: `htb-dashboard.html`
3. Verify stats match your profile

---

### Step 5: Schedule Weekly Tracking

1. Replace "Manual Trigger" with "Schedule Trigger"
2. Configure:
   - Interval: Weeks
   - Day: Sunday
   - Time: 23:59
3. Activate workflow

---

## Automated Notifications

### Slack Setup

1. Add Slack node after "Detect New Achievements"
2. Connect workspace
3. Select channel: #achievements
4. Test notification

### Discord Setup

1. Create webhook in Discord channel settings
2. Add HTTP Request node:
   - Method: POST
   - URL: Your Discord webhook URL
   - Body: See workflow for template

### Gmail Setup

1. Configure Email Credentials
   - Click on "Send Email Alert" node
   - Click "Select Credential" → "Create New" → "Gmail OAuth2"
   - Click "Connect my account"
   - Authorize Google account

---

## Troubleshooting

**Profile not loading:**
- Verify user ID is correct
- Check profile is set to public
- HTB API may have changed (check for errors)

**No dashboard generated:**
- Check file permissions
- Verify Chart.js CDN is accessible
- Review execution logs or
- Ensure the Save HTML Dashboard node has permission to convert the file

**Achievements not detecting:**
- First run won't show achievements
- Manually complete a machine and re-run

---

## Customization

### Change Dashboard Colors

Edit "Generate HTML Dashboard" node, modify CSS:
```css
background: linear-gradient(90deg, #YOUR_COLOR 0%, #YOUR_COLOR2 100%);
```

### Add More Stats

Add to stats-grid section:
```html
<div class="stat-card">
  <div class="number">{{ NEW_STAT }}</div>
  <div class="label">Label</div>
</div>
```

### Export Data

Add "Write to File" node:
- Format: CSV
- Data: Progress history
