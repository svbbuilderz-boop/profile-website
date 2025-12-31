# SVB Builders Website - Google Sheets Integration Guide

## Overview
Your updated website now includes:
1. A popup form that appears on page load with "Om Namo Venkatesaya" in the header
2. Clickable project cards that trigger the same form before navigation
3. Integration with Google Sheets to store visitor details

## Setup Instructions for Google Sheets Integration

### Step 1: Create a Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new spreadsheet
3. Name it "SVB Builders - Contact Details"
4. In the first row, add these column headers:
   - Column A: **Name**
   - Column B: **Phone**
   - Column C: **Timestamp**
   - Column D: **Source**

### Step 2: Create Google Apps Script

1. In your Google Sheet, click **Extensions** > **Apps Script**
2. Delete any existing code
3. Paste the following code:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var data = JSON.parse(e.postData.contents);
    
    // Add the data to the sheet
    sheet.appendRow([
      data.name,
      data.phone,
      data.timestamp,
      data.source
    ]);
    
    return ContentService.createTextOutput(JSON.stringify({
      'result': 'success'
    })).setMimeType(ContentService.MimeType.JSON);
    
  } catch(error) {
    return ContentService.createTextOutput(JSON.stringify({
      'result': 'error',
      'error': error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet(e) {
  return ContentService.createTextOutput("Service is running");
}
```

4. Click the **Save** icon (disk icon)
5. Name your project (e.g., "SVB Contact Form Handler")

### Step 3: Deploy the Web App

1. Click **Deploy** > **New deployment**
2. Click the gear icon ⚙️ next to "Select type"
3. Choose **Web app**
4. Configure the deployment:
   - **Description**: SVB Contact Form
   - **Execute as**: Me (your email)
   - **Who has access**: Anyone
5. Click **Deploy**
6. You may need to authorize the script:
   - Click **Authorize access**
   - Choose your Google account
   - Click **Advanced** > **Go to [Project Name] (unsafe)**
   - Click **Allow**
7. **IMPORTANT**: Copy the **Web app URL** that appears (it looks like: `https://script.google.com/macros/s/AKfycby.../exec`)

### Step 4: Update Your Website

1. Open the `svb-builders-website-updated.html` file
2. Find this line (around line 1044):
   ```javascript
   const GOOGLE_SHEETS_URL = 'YOUR_GOOGLE_SHEETS_WEB_APP_URL_HERE';
   ```
3. Replace `'YOUR_GOOGLE_SHEETS_WEB_APP_URL_HERE'` with your actual Web App URL:
   ```javascript
   const GOOGLE_SHEETS_URL = 'https://script.google.com/macros/s/AKfycby.../exec';
   ```
4. Save the file

### Step 5: Test Your Setup

1. Open your updated HTML file in a web browser
2. The popup form should appear automatically
3. Fill in:
   - Name: Test User
   - Phone: 1234567890
4. Click "Submit & Continue"
5. Check your Google Sheet - you should see the new entry

## Features Implemented

### 1. Initial Page Load Form
- Appears automatically when someone first visits the website
- Shows "Om Namo Venkatesaya" in the header
- Collects name and phone number
- Stores data in Google Sheets
- Uses localStorage to remember if user has already submitted

### 2. Project Card Forms
- All three project cards (Farmland, Residential, Apartment) are now clickable
- When clicked WITHOUT prior form submission:
  - Shows the same popup form
  - Records which project they're interested in
  - Prevents navigation until form is submitted
- When clicked WITH prior form submission:
  - Allows immediate navigation (you can customize where they go)

### 3. Data Storage
Each submission stores:
- **Name**: Visitor's full name
- **Phone**: 10-digit mobile number
- **Timestamp**: Exact date and time of submission
- **Source**: Either "Homepage" or the specific project name

### 4. Form Validation
- Name: Required field, cannot be empty
- Phone: Must be exactly 10 digits, numbers only
- Real-time error messages for invalid inputs

## Customization Options

### Change Where Project Cards Navigate

Currently, project cards show an alert. To navigate to actual pages, find this code (around line 1120):

```javascript
} else {
    // User has already submitted, allow navigation
    alert(`Navigating to ${projectType.toUpperCase()} project details...`);
    // window.location.href = `${projectType}-details.html`;
}
```

Uncomment and modify the last line to navigate to your project pages:
```javascript
window.location.href = `projects/${projectType}.html`;
```

### Modify Form Fields

To add more fields (like email), edit the HTML form section and update the Google Sheets script to handle additional data.

### Style Customization

All colors and styles are defined in CSS variables at the top of the file:
```css
:root {
    --primary-gold: #C9A84E;
    --dark-navy: #1A2332;
    --soft-cream: #F8F6F1;
    --accent-teal: #3A5F5F;
    --light-grey: #E8E6E1;
    --text-dark: #2C2C2C;
    --text-light: #6B6B6B;
}
```

## Troubleshooting

### Form not submitting to Google Sheets
1. Check that you've replaced the URL with your actual Web App URL
2. Verify the Web App is deployed with "Anyone" access
3. Check your browser console for error messages (F12 > Console)

### Form not appearing on page load
- Clear your browser's localStorage
- Open Developer Tools (F12)
- Go to Application > Local Storage
- Delete the `svb_initial_submitted` key

### Phone number validation issues
- Ensure users enter exactly 10 digits
- No spaces, hyphens, or country codes
- Only numbers 0-9

## Security Notes

- The form uses `mode: 'no-cors'` which means you won't see responses but the data will be submitted
- All submissions are logged with timestamps for audit purposes
- Consider adding CAPTCHA if you experience spam submissions
- The Google Apps Script runs with your permissions, so keep the URL secure

## Support

If you need to modify the functionality or add features, the main JavaScript code is at the bottom of the HTML file (starting around line 1043).

Key sections:
- Lines 1044-1050: Configuration and setup
- Lines 1052-1058: Page load modal trigger
- Lines 1060-1114: Form submission logic
- Lines 1116-1133: Project card click handlers

---

**Need Help?** Keep the Google Sheets URL private and secure. Anyone with this URL can submit data to your sheet.
