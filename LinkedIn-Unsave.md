
# LinkedIn Saved Posts Management Script

This JavaScript script allows you to automatically manage saved posts on LinkedIn by either "unsaving" or "removing" all visible posts through the overflow menu options.

## How It Works

### 1. Identify Overflow Menus
The script selects all elements with the attribute `data-test-icon="overflow-web-ios-medium"`, which usually corresponds to the three-dot overflow menu icons on LinkedIn posts.

### 2. Iterative Process for Unsave or Remove
For each overflow icon found, the script performs these actions:
- **Remove the `inert` Attribute (if present):** The script removes this attribute to allow interaction.
- **Click the Overflow Icon:** It then clicks the parent element (often an anchor or `<div>` holding the SVG) to open the options menu.

### 3. Action (Unsave or Remove)
After a brief delay to ensure the menu is fully loaded, the script will locate either the "Unsave" or "Remove" option based on your choice.
- If the "Unsave" option is found, it clicks to remove the post from the saved list.
- If the "Remove" option is found, it clicks to delete the post.

### 4. Timing Considerations
Each iteration includes a delay to ensure each menu interaction completes without interference, preventing action overlap.

## Usage Instructions

1. **Open LinkedIn Saved Posts:** 
   Go to your LinkedIn saved posts page so that the posts you want to manage are visible on the screen.

2. **Open Developer Console:** 
   Open your browser’s Developer Console by pressing `F12` or `Ctrl+Shift+J` (Windows/Linux) or `Cmd+Option+J` (Mac).

3. **Paste and Run the Desired Script:**
   Copy and paste either the "Unsave" or "Remove" code below into the console and press **Enter** to execute.

   > **Note:** Adjust delay values if LinkedIn’s interface takes longer to load each menu.

---

## Code Example for Unsave

This script unsaves each visible post on the page.

```javascript
// Select all visible overflow menu icons in the view
let overflowMenus = Array.from(document.querySelectorAll('svg[data-test-icon="overflow-web-ios-medium"]'));

overflowMenus.forEach((icon, index) => {
    setTimeout(() => {
        // Step 1: Remove the 'inert' attribute if present and open the overflow menu
        if (icon.hasAttribute('inert')) {
            icon.removeAttribute('inert');
        }
        icon.parentElement.click(); // Open the overflow menu
        console.log(`Overflow menu ${index + 1} clicked.`);
        
        // Step 2: Wait briefly to allow the menu to open, then locate and click "Unsave"
        setTimeout(() => {
            let unsaveOption = Array.from(document.querySelectorAll('span'))
                .find(span => span.textContent.includes('Unsave'));

            if (unsaveOption) {
                unsaveOption.click();
                console.log(`Post ${index + 1} unsaved!`);
            } else {
                console.log(`Unsave option not found for post ${index + 1}.`);
            }
        }, 500); // Adjust delay as needed
    }, index * 1000); // Delay each iteration to avoid overlapping clicks
});
```

---

## Code Example for Remove

This script removes each visible post on the page.

```javascript
// Select all visible overflow menu icons in the view
let overflowMenus = Array.from(document.querySelectorAll('svg[data-test-icon="overflow-web-ios-medium"]'));

overflowMenus.forEach((icon, index) => {
    setTimeout(() => {
        // Step 1: Remove the 'inert' attribute if present and open the overflow menu
        if (icon.hasAttribute('inert')) {
            icon.removeAttribute('inert');
        }
        icon.parentElement.click(); // Open the overflow menu
        console.log(`Overflow menu ${index + 1} clicked.`);
        
        // Step 2: Wait briefly to allow the menu to open, then locate and click "Remove"
        setTimeout(() => {
            let removeOption = Array.from(document.querySelectorAll('span'))
                .find(span => span.textContent.includes('Remove'));

            if (removeOption) {
                removeOption.click();
                console.log(`Post ${index + 1} removed!`);
            } else {
                console.log(`Remove option not found for post ${index + 1}.`);
            }
        }, 500); // Adjust delay as needed
    }, index * 1000); // Delay each iteration to avoid overlapping clicks
});
```

---

## Limitations

- **Dynamic Elements:** LinkedIn may update its structure or attributes, which could break this script. Check for updated selectors if this occurs.
- **Rate Limiting:** LinkedIn may temporarily restrict actions if it detects too many interactions in a short period.

## Troubleshooting

If you encounter issues, verify the following:
- **Selector Validity:** Ensure the `data-test-icon="overflow-web-ios-medium"` selector still applies to the overflow menu.
- **Timing Delays:** Increase delays if LinkedIn’s menus load slowly.
- **Console Messages:** Check the console output for logs on each action to help diagnose where the script may be failing.
