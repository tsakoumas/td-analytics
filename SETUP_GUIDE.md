# TD Analytics - Complete Setup Guide

## Files Included

| File | Purpose |
|------|---------|
| `index.html` | The complete app (HTML + CSS + JavaScript) |
| `manifest.json` | PWA configuration for iOS home screen |
| `icon-192.png` | App icon (small) |
| `icon-512.png` | App icon (large) |

---

## What This App Does

**Dashboard Features:**
- Sessions, Users, Bounce Rate, Avg. Duration
- Traffic trend chart
- Top pages breakdown
- Device breakdown (mobile/desktop/tablet)

**Geographic Data:**
- Top countries with flags
- Top cities
- Interactive visitor hotspots
- Click any location to filter

**Where Visitors Came From:**
- Full source/medium breakdown (google/organic, facebook/paid, etc.)
- Click any source to filter

**Filters:**
- Filter by Country
- Filter by City
- Filter by Traffic Source
- Clear all filters

**13 AI-Computed Insights:**
1. Traffic Velocity (acceleration/deceleration)
2. Traffic Source Concentration Risk
3. Bounce Rate vs Industry Benchmark
4. Session Duration Quality Score
5. Pages Per Session Efficiency
6. New vs Returning User Ratio
7. Weekend vs Weekday Pattern
8. Page Concentration Analysis
9. Device Performance Gap
10. Traffic Trend Classification
11. Geographic Concentration
12. Top City Clusters
13. Organic vs Paid Traffic Balance

---

## STEP 1: Host the App Files

You need to host these files on a web server with HTTPS. Pick ONE option:

### Option A: GitHub Pages (Free, Recommended)

1. Go to https://github.com and sign in (or create account)

2. Click the **+** button (top right) → **New repository**

3. Name it: `td-analytics`

4. Keep it **Public**, click **Create repository**

5. On the next page, click **"uploading an existing file"**

6. Drag all 4 files into the upload area:
   - index.html
   - manifest.json
   - icon-192.png
   - icon-512.png

7. Click **Commit changes**

8. Go to **Settings** tab → **Pages** (left sidebar)

9. Under "Source", select **main** branch, click **Save**

10. Wait 2-3 minutes, then your app is live at:
    ```
    https://YOUR_GITHUB_USERNAME.github.io/td-analytics/
    ```

### Option B: Netlify (Free, Drag-and-Drop)

1. Go to https://netlify.com and sign up

2. From dashboard, drag and drop the folder containing all 4 files

3. Netlify gives you a URL like:
   ```
   https://random-name-12345.netlify.app
   ```

4. You can customize this URL in Site Settings

---

## STEP 2: Google Cloud Console Setup

This is required to connect to your Google Analytics data.

### 2.1 Create a Google Cloud Project

1. Go to: https://console.cloud.google.com

2. Click **Select a project** (top left) → **New Project**

3. Enter:
   - Project name: `TD Analytics App`
   - Click **Create**

4. Wait for project creation (30 seconds)

5. Make sure your new project is selected in the dropdown

### 2.2 Enable the Analytics API

1. In the search bar at top, type: `Google Analytics Data API`

2. Click on **Google Analytics Data API** in results

3. Click the blue **Enable** button

4. Wait for it to enable (30 seconds)

### 2.3 Configure OAuth Consent Screen

1. In left sidebar, click **APIs & Services** → **OAuth consent screen**

2. Select **External** → Click **Create**

3. Fill in the form:
   - App name: `TD Analytics`
   - User support email: `your@email.com`
   - Scroll down, Developer contact email: `your@email.com`
   - Click **Save and Continue**

4. On "Scopes" page:
   - Click **Add or Remove Scopes**
   - In the filter box, type: `analytics.readonly`
   - Check the box for `../auth/analytics.readonly`
   - Click **Update**
   - Click **Save and Continue**

5. On "Test users" page:
   - Click **Add Users**
   - Enter your email address
   - Click **Add**
   - Click **Save and Continue**

6. Click **Back to Dashboard**

### 2.4 Create OAuth Credentials

1. In left sidebar, click **APIs & Services** → **Credentials**

2. Click **+ Create Credentials** → **OAuth client ID**

3. Select Application type: **Web application**

4. Name: `TD Analytics Web`

5. Under **Authorized JavaScript origins**, click **+ Add URI**:
   - Add your hosted URL, example:
     ```
     https://yourusername.github.io
     ```
   - (Just the base URL, no path)

6. Under **Authorized redirect URIs**, click **+ Add URI**:
   - Add the same URL:
     ```
     https://yourusername.github.io
     ```

7. Click **Create**

8. A popup shows your credentials. **Copy the Client ID** - it looks like:
   ```
   123456789-abcdefg.apps.googleusercontent.com
   ```

9. Click **OK**

### 2.5 Create API Key

1. Still on Credentials page, click **+ Create Credentials** → **API Key**

2. A popup shows your new API key. **Copy it**.

3. Click **Edit API key** (or click the pencil icon)

4. Under "API restrictions":
   - Select **Restrict key**
   - Check **Google Analytics Data API**
   - Click **Save**

---

## STEP 3: Get Your GA4 Property ID

1. Go to: https://analytics.google.com

2. Make sure you're viewing the **tailordigitals.com** property

3. Click the **gear icon** (Admin) in bottom left

4. In the Property column, click **Property Settings**

5. At the top, you'll see **PROPERTY ID** - it's a number like:
   ```
   123456789
   ```

6. Copy this number

---

## STEP 4: Update the App with Your Credentials

1. Open `index.html` in any text editor (TextEdit, Notepad, VS Code)

2. Press **Ctrl+F** (or Cmd+F on Mac) and search for:
   ```
   YOUR_GOOGLE_CLIENT_ID
   ```

3. Find this section (around line 1440):
   ```javascript
   const CONFIG = {
       CLIENT_ID: 'YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com',
       API_KEY: 'YOUR_GOOGLE_API_KEY',
       PROPERTY_ID: 'properties/YOUR_GA4_PROPERTY_ID',
   ```

4. Replace with your actual values:
   ```javascript
   const CONFIG = {
       CLIENT_ID: '123456789-abcdefg.apps.googleusercontent.com',
       API_KEY: 'AIzaSyB-abc123def456',
       PROPERTY_ID: 'properties/123456789',
   ```

5. **Save the file**

6. Re-upload to GitHub/Netlify:
   - **GitHub**: Go to your repo, click index.html, click pencil to edit, paste new content, commit
   - **Netlify**: Just drag the updated file to your site

---

## STEP 5: Add to iPhone Home Screen

1. Open **Safari** on your iPhone (must be Safari, not Chrome)

2. Go to your hosted URL:
   ```
   https://yourusername.github.io/td-analytics/
   ```

3. Tap the **Share button** (square with arrow pointing up)

4. Scroll down and tap **"Add to Home Screen"**

5. Name it: `TD Analytics`

6. Tap **Add**

The app now appears on your home screen and works like a native app!

---

## STEP 6: First Sign In

1. Open the app from your home screen

2. Tap **"Sign in with Google"**

3. Select your Google account (use the one with GA access)

4. If prompted about app verification, click **Advanced** → **Go to TD Analytics (unsafe)**
   - This is normal for apps in test mode

5. Grant permission to view analytics data

6. The dashboard loads with your live data!

---

## Troubleshooting

### "Sign in doesn't work"
- Verify CLIENT_ID ends in `.apps.googleusercontent.com`
- Check your hosted URL is in "Authorized JavaScript origins" (exact match, including https://)
- Make sure you're using HTTPS, not HTTP

### "No data after sign in"
- Verify PROPERTY_ID format is `properties/123456789` (include the word "properties/")
- Make sure your Google account has access to the GA4 property
- Check that Google Analytics Data API is enabled

### "App shows mock data"
- The CONFIG values still have placeholder text
- Update CLIENT_ID, API_KEY, and PROPERTY_ID with real values
- Re-upload the file

### "Can't add to home screen"
- Must use Safari (not Chrome or Firefox)
- Must be HTTPS (not HTTP)

### "Error 403 or permission denied"
- Add your email to "Test users" in OAuth consent screen
- Or publish the app (OAuth consent screen → Publish App)

---

## Updating the App

To update after changes:

**GitHub Pages:**
1. Go to your repository
2. Click the file you want to update
3. Click the pencil icon to edit
4. Make changes
5. Click "Commit changes"
6. Wait 2-3 minutes for update to go live

**Netlify:**
1. Make changes to your local file
2. Drag the updated file to Netlify dashboard
3. Changes go live immediately

---

## Security Notes

- Your Google password is never stored (OAuth 2.0)
- Access tokens are stored locally and cleared on sign out
- API key is restricted to Analytics API only
- All data stays between Google and your browser

---

## Support

If you get stuck, document:
1. What step you're on
2. What you expected to happen
3. What actually happened
4. Any error messages (screenshot helps)
