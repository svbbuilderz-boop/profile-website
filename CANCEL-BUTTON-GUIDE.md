# SVB Builders Website - Updated with Cancel Button

## What's Changed

Your website now has a **smarter popup form system** with these behaviors:

### 1. **Initial Page Load (Optional) ✅**
- Popup appears when someone first visits the website
- **"Maybe Later" button** is visible
- Users can close the form and browse the website freely
- No data is collected if they click "Maybe Later"

### 2. **Project Card Clicks (Mandatory) ✅**
- When users click on ANY project card (Farmland, Residential, or Apartment)
- The popup appears again
- **"Maybe Later" button is HIDDEN** - form becomes mandatory
- Users MUST enter their details to access project pages
- Each project card triggers the form separately

## How It Works

### Scenario 1: First-Time Visitor Skips Initial Form
```
1. User visits website
2. Popup appears with "Maybe Later" button
3. User clicks "Maybe Later"
4. Popup closes, user browses freely
5. User clicks "Farmland Projects" card
6. Popup appears again (no cancel button this time)
7. User MUST submit to see project page
8. After submission, redirected to farmland coming soon page
```

### Scenario 2: First-Time Visitor Submits Initial Form
```
1. User visits website
2. Popup appears with "Maybe Later" button
3. User fills form and submits
4. Data stored in Google Sheets
5. User clicks any project card
6. Popup appears again (mandatory)
7. User submits details
8. Redirected to project page
```

### Scenario 3: Returning Visitor
```
1. User has already submitted form once
2. No popup on page load
3. User clicks project card
4. Popup appears (mandatory)
5. User submits
6. Redirected to project page
```

## Key Features

### ✅ Cancel Button Behavior
- **Visible**: On initial page load popup
- **Hidden**: When user clicks project cards
- **Function**: Closes modal and allows browsing

### ✅ Smart Tracking
The system tracks:
- If user submitted the initial popup form
- Which projects they've clicked on
- Ensures form appears for each project card click

### ✅ Data Collection
Each submission stores:
- Name
- Phone Number
- Timestamp
- Source (Homepage or specific project name)

## Technical Details

### LocalStorage Keys Used
```javascript
'svb_initial_submitted'              // Tracks if initial form was submitted
'svb_project_farmland_submitted'     // Tracks farmland project form
'svb_project_residential_submitted'  // Tracks residential project form
'svb_project_apartment_submitted'    // Tracks apartment project form
```

### JavaScript Variables
```javascript
isProjectClick          // Tracks if modal is from project card click
hasSubmittedInitial    // Tracks if user submitted initial form
window.pendingProjectRedirect  // Stores where to redirect after submission
```

## Button Styling

### Submit Button
- Gold background (#C9A84E)
- Full width when no cancel button
- Half width when cancel button is visible

### Cancel Button ("Maybe Later")
- Transparent background with border
- Grey text color
- Appears on left side
- Only shows for initial popup

## Testing the Changes

### Test 1: Initial Popup Cancel
1. Open website in browser
2. Popup appears with "Maybe Later" button
3. Click "Maybe Later"
4. Popup closes
5. You can browse the website

### Test 2: Project Card Mandatory Form
1. Click any project card (without submitting initial form)
2. Popup appears WITHOUT "Maybe Later" button
3. Try clicking outside - modal stays open
4. Must fill form and submit
5. Redirects to project page

### Test 3: Multiple Project Clicks
1. Click "Farmland Projects" → Submit form → Redirected
2. Go back to homepage
3. Click "Residential Projects" → Form appears again → Submit → Redirected
4. Each project card triggers the form

## Customization Options

### Change Button Text

**Cancel Button** (line ~811):
```html
<button type="button" class="cancel-btn" id="cancelBtn">Maybe Later</button>
```
Change "Maybe Later" to your preferred text like:
- "Skip for now"
- "Browse website"
- "Not now"

**Submit Button** (line ~812):
```html
<button type="submit" class="submit-btn" id="submitBtn">Submit & Continue</button>
```

### Change Button Colors

Find the CSS section (around line 165-210):

**Cancel Button Color**:
```css
.cancel-btn {
    background: transparent;
    color: var(--text-light);  /* Change this */
    border: 2px solid var(--light-grey);  /* And this */
}
```

**Submit Button Color**:
```css
.submit-btn {
    background: var(--primary-gold);  /* Change this */
    color: var(--dark-navy);  /* And this */
}
```

### Make Modal Non-Dismissible

If you want users to NEVER be able to close the modal (even on initial load), remove the cancel button logic:

In JavaScript (line ~1054):
```javascript
// Cancel button handler
cancelBtn.addEventListener('click', () => {
    // Delete this entire function to make modal always mandatory
});
```

## File Structure

```
your-website-folder/
├── svb-builders-website-updated.html    (Main file with cancel button)
├── project-coming-soon.html             (Project pages)
├── SETUP-INSTRUCTIONS.md                (Google Sheets guide)
└── images/                              (Your project images)
    ├── farmland.jpg
    ├── residential.jpg
    └── apartment.jpg
```

## Google Sheets Integration

The form still works with Google Sheets as before. Each submission includes:

```
Name | Phone | Timestamp | Source
-----|-------|-----------|--------
John | 9876543210 | 2025-01-01 10:30 | Homepage
Jane | 9123456789 | 2025-01-01 11:15 | FARMLAND PROJECT
Mike | 9988776655 | 2025-01-01 12:00 | RESIDENTIAL PROJECT
```

## Browser Compatibility

Works on:
- ✅ Chrome, Edge, Firefox, Safari (desktop)
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)
- ✅ Tablets

## Troubleshooting

### Cancel button not showing on initial popup
- Clear browser cache
- Clear localStorage (F12 > Application > Local Storage > Delete All)
- Refresh page

### Cancel button showing on project clicks
- Check the JavaScript code around line 1129
- Ensure `cancelBtn.classList.add('hidden');` is present

### Modal not closing when cancel is clicked
- Check browser console for JavaScript errors (F12 > Console)
- Verify the cancel button has `id="cancelBtn"`

### Form appears every time on page load
- Check if localStorage is enabled in browser
- Clear localStorage and try again
- Check that the key `'svb_initial_submitted'` is being set

## Summary

The key difference in behavior:

| Scenario | Cancel Button | Form Required |
|----------|---------------|---------------|
| Initial page load | ✅ Visible | ❌ Optional |
| Project card click | ❌ Hidden | ✅ Mandatory |

This gives you the best of both worlds:
- **Non-intrusive** initial experience (users can skip)
- **Lead capture** when users show real interest (clicking projects)

---

**Need More Help?** All the code is commented and organized. Look for comments starting with `//` in the JavaScript section to understand each part.
