# LDS Youth Activities System

A digital flier + SMS reminder system for weekly youth activities.

## Components

| Component | Purpose |
|-----------|---------|
| **Google Sheet** | Data entry for activities |
| **GitHub Pages** | Public-facing digital flier |
| **n8n Workflow** | Sends SMS reminders via RingCentral every Tuesday at 5 PM |

---

## Setup Instructions

### 1. Create Google Sheet

Create a new Google Sheet with a tab named **"Activities"** and these columns:

| Column | Description | Example |
|--------|-------------|---------|
| Date | Activity date (YYYY-MM-DD) | 2026-02-11 |
| Activity | Name of the activity | Basketball Night |
| Description | What we'll be doing | Come play basketball and have fun! |
| Location | Where to meet | Church Gym |
| Time | Start time | 7:00 PM |
| Contact | Who to contact with questions | Bishop Johnson |
| What to Bring | Items needed | Athletic clothes, water bottle |
| Theme | Optional theme for the night | Sports Night |

**Sheet Layout:**
```
| Date       | Activity        | Description                  | Location    | Time    | Contact        | What to Bring         | Theme       |
|------------|-----------------|------------------------------|-------------|---------|----------------|----------------------|-------------|
| 2026-02-11 | Basketball Night| Come play basketball!        | Church Gym  | 7:00 PM | Bishop Johnson | Athletic clothes      | Sports Night|
| 2026-02-18 | Service Project | Help clean up the park       | City Park   | 7:00 PM | Bro. Smith     | Work gloves          |             |
```

### 2. Publish Google Sheet

1. Open your Google Sheet
2. Go to **File → Share → Publish to web**
3. Select "Entire Document" and "Web page"
4. Click **Publish**
5. Copy your Sheet ID from the URL:
   ```
   https://docs.google.com/spreadsheets/d/[THIS-IS-YOUR-SHEET-ID]/edit
   ```

### 3. Update the HTML File

Edit `index.html` and replace `YOUR_GOOGLE_SHEET_ID_HERE` with your actual Sheet ID:

```javascript
const SHEET_ID = 'your-actual-sheet-id-here';
```

### 4. Deploy to GitHub Pages

1. Create a new repo on GitHub (e.g., `youth-activities`)
2. Push this code:
   ```bash
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/YOUR-USERNAME/youth-activities.git
   git push -u origin main
   ```
3. Go to repo Settings → Pages
4. Set Source to "Deploy from a branch" → main → / (root)
5. Your site will be live at: `https://YOUR-USERNAME.github.io/youth-activities/`

### 5. Set Up n8n Workflow

Import the workflow from `n8n-workflow.json` into your n8n instance.

**Configure:**
1. Update the Google Sheets node with your sheet credentials
2. Update the RingCentral node with recipient phone numbers
3. Workflow runs every Tuesday at 5 PM (Arizona time)

---

## Adding New Activities

1. Open your Google Sheet
2. Add a new row with the activity details
3. The website updates automatically
4. SMS will go out the Tuesday before at 5 PM

---

## Phone Number List

Create a second tab in your Google Sheet called **"Contacts"** with:

| Name | Phone |
|------|-------|
| John Smith | +14805551234 |
| Jane Doe | +14805555678 |

The n8n workflow will read from this tab to send SMS to all contacts.

---

## Customization

### Change Colors
Edit the Tailwind classes in `index.html`:
- Header: `bg-white`
- Background: `bg-gradient-to-br from-blue-50 to-indigo-100`
- Featured card: `border-green-400`

### Change Header Text
Find and edit in `index.html`:
```html
<h1>Youth Activities</h1>
<p>Wednesdays at 7:00 PM</p>
```
