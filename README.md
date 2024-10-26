
# LinkedIn Saved Posts Removal Script

This JavaScript script helps you automatically remove all visible saved posts on LinkedIn by interacting with each post's overflow menu.

## How It Works

### 1. Identify Overflow Menus
The script first selects all elements with the attribute `data-test-icon="overflow-web-ios-medium"`, typically corresponding to the three-dot overflow menu icons on LinkedIn posts.

### 2. Iterative Removal Process
For each overflow icon found, the script performs the following actions:
- **Remove the `inert` Attribute:** If present, this attribute prevents interaction. The script removes it to enable interaction.
- **Click the Overflow Icon:** The script clicks the icon’s parent element (often an anchor or `<div>` that contains the SVG) to open the options menu.

### 3. Remove Action
After a brief delay to ensure the menu is fully loaded, the script searches for a `<span>` element containing the text "Remove."
- If the "Remove" option is found, it clicks this option to remove the post from the saved list.

### 4. Timing Considerations
Each iteration includes a unique delay, ensuring that each menu opens and closes without interfering with other interactions. This approach avoids overlap between actions.

## Usage Instructions

1. **Open LinkedIn Saved Posts:** 
   Navigate to your LinkedIn saved posts page to ensure that the posts you want to remove are visible on the screen.

2. **Open Developer Console:** 
   Open your browser’s Developer Console by pressing `F12` or `Ctrl+Shift+J` (Windows/Linux) or `Cmd+Option+J` (Mac).

3. **Paste and Run the Script:** 
   Copy and paste the code into the console and press **Enter** to execute.

   > **Note:** Adjust the delay values in the code if the LinkedIn interface requires longer loading times for each menu.

## Code Example

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

## Limitations

- **Dynamic Elements:** LinkedIn may update its structure or attributes, which could break this script. Check for updated selectors if this occurs.
- **Rate Limiting:** LinkedIn may temporarily restrict actions if it detects too many interactions in a short period.

## Troubleshooting

If you encounter issues, verify the following:
- **Selector Validity:** Ensure the `data-test-icon="overflow-web-ios-medium"` selector still applies to the overflow menu.
- **Timing Delays:** Increase delays if LinkedIn’s menus load slowly.
- **Console Messages:** Check the console output for logs on each action to help diagnose where the script may be failing.
