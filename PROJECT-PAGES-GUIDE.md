# SVB Builders Website - Project Pages Update

## What's New

I've created a **single "Coming Soon" page** that dynamically displays content for all three project types:
- Farmland Projects
- Residential Projects  
- Apartment Projects

This is more efficient than creating three separate HTML files!

## Files You Have

1. **svb-builders-website-updated.html** - Your main website (now updated with clickable project cards)
2. **project-coming-soon.html** - The dynamic "Coming Soon" page for all projects
3. **SETUP-INSTRUCTIONS.md** - Google Sheets integration guide

## How It Works

### Project Cards Are Now Clickable ✅

When visitors click on any project card:

1. **First-time visitors** (haven't filled the form):
   - The popup form appears
   - They must enter their details
   - After submission, they're automatically redirected to the project page

2. **Returning visitors** (already submitted form):
   - They're immediately redirected to the project page
   - No form interruption

### Dynamic Coming Soon Page

The `project-coming-soon.html` page automatically shows different content based on which project was clicked:

- **Farmland Project** → Shows 🌾 icon and farmland-specific text
- **Residential Project** → Shows 🏘️ icon and residential-specific text
- **Apartment Project** → Shows 🏢 icon and apartment-specific text

## File Structure

```
your-website-folder/
├── svb-builders-website-updated.html    (Main homepage)
├── project-coming-soon.html             (Coming soon page for all projects)
└── SETUP-INSTRUCTIONS.md                (Google Sheets setup guide)
```

**Important:** Both files must be in the **same folder** for the links to work correctly.

## How to Use

### Step 1: Place Files Together
Put both HTML files in the same directory on your web server or local folder.

### Step 2: Test Locally
1. Open `svb-builders-website-updated.html` in your browser
2. Scroll to the "Our Projects" section
3. Click on any project card (Farmland, Residential, or Apartment)
4. If first visit: Fill out the form
5. You'll be redirected to the "Coming Soon" page

### Step 3: Navigate Back
The coming soon page has:
- A "Back to All Projects" button
- Full navigation menu in the header
- Contact information to reach you

## Customizing the Coming Soon Page

### Change the Icons
Find this section in `project-coming-soon.html` (around line 360):

```javascript
const projectConfigs = {
    farmland: {
        icon: '🌾',
        name: 'Farmland Projects',
        description: 'farmland'
    },
    residential: {
        icon: '🏘️',
        name: 'Residential Projects',
        description: 'residential plot'
    },
    apartment: {
        icon: '🏢',
        name: 'Apartment Projects',
        description: 'apartment'
    }
};
```

You can change the emojis or text as needed.

### Change the Message
Edit the description text around line 248:

```html
<p class="description">
    We are working on bringing you exceptional <span id="projectName">farmland</span> opportunities 
    that reflect our commitment to quality, transparency, and customer satisfaction. 
    Stay tuned for detailed information about locations, amenities, and booking details.
</p>
```

### Update Contact Information
The coming soon page displays your contact info (around line 254):

```html
<div class="contact-item">
    📧 <a href="mailto:info@svbbuilders.in">info@svbbuilders.in</a>
</div>
<div class="contact-item">
    📱 <a href="tel:+916363307062">+91 63633 07062</a>
</div>
```

Update these with your actual contact details.

## When Projects Are Ready

When you're ready to launch actual project pages, you have two options:

### Option 1: Replace the Coming Soon Page
Create individual pages:
- `farmland-project.html`
- `residential-project.html`
- `apartment-project.html`

Then update the main website's JavaScript (line 1120):

```javascript
} else {
    // Navigate to specific project pages
    window.location.href = `${projectType}-project.html`;
}
```

### Option 2: Update the Coming Soon Page
Transform `project-coming-soon.html` into a full project details page by:
1. Replacing the "Coming Soon" text with actual project details
2. Adding image galleries
3. Including pricing and availability information
4. Adding booking forms

## Design Features

The coming soon page includes:
- ✅ Om Namo Venkatesaya header (matching your brand)
- ✅ Animated background pattern (consistent with main site)
- ✅ Bouncing project icon
- ✅ Professional gradient background
- ✅ Contact information section
- ✅ "Get Notified" call-to-action
- ✅ Fully responsive design
- ✅ Back navigation button
- ✅ Complete header navigation

## Testing Checklist

- [ ] Both files are in the same folder
- [ ] Click on "Farmland Projects" card → redirects to coming soon page with farmland icon
- [ ] Click on "Residential Projects" card → redirects to coming soon page with residential icon
- [ ] Click on "Apartment Projects" card → redirects to coming soon page with apartment icon
- [ ] "Back to All Projects" button returns to homepage
- [ ] Header navigation links work correctly
- [ ] Form submission (if first time) works before redirection
- [ ] Mobile responsive design looks good
- [ ] Contact links (email/phone) work properly

## Troubleshooting

### Project cards not clickable
- Make sure you're using the updated `svb-builders-website-updated.html` file
- Check browser console for JavaScript errors (F12 > Console)

### Coming soon page shows wrong project
- Verify the URL has the correct parameter: `?type=farmland`, `?type=residential`, or `?type=apartment`
- Check that the file names match exactly (case-sensitive)

### Navigation back to homepage doesn't work
- Ensure both HTML files are in the same directory
- If files are in different folders, update the file paths in the links

### Form not triggering before navigation
- Clear your browser's localStorage (F12 > Application > Local Storage)
- Delete the `svb_initial_submitted` key
- Refresh the page and try again

## Next Steps

1. ✅ Complete Google Sheets setup (see SETUP-INSTRUCTIONS.md)
2. ✅ Upload both HTML files to your web server
3. ✅ Test all navigation flows
4. ✅ Customize contact information
5. ✅ When ready, create detailed project pages to replace the coming soon page

---

**Pro Tip:** The coming soon page is a great way to build anticipation and collect interested customer data before your projects officially launch!
