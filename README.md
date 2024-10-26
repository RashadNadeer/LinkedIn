# Linkedin-

How It Works
Identify Overflow Menus:

The script first selects all elements with the data-test-icon="overflow-web-ios-medium" attribute, which typically corresponds to the three-dot overflow menu icons on LinkedIn.
Iterative Unsave Process:

For each icon, the script:
Removes the inert attribute if present, making it interactable.
Clicks on the icon’s parent element (usually a <button> or <div> that holds the SVG) to open the options menu.
Unsave Action:

After a short delay to allow the menu to load, the script searches for a span containing the text "Unsave."
If the "Unsave" option is found, it clicks the option to remove the post from the saved list.
Timing Considerations:

Each iteration includes a unique delay to ensure each menu opens and closes without interference. This approach avoids overlap in actions.
Usage Instructions
Open LinkedIn Saved Posts:

Navigate to your saved posts on LinkedIn to ensure the posts you want to unsave are visible on the screen.
Open Developer Console:

Open your browser’s Developer Console (usually by pressing F12 or Ctrl+Shift+J).
Paste and Run the Script:

Copy and paste the code above into the console and press Enter.
Note: Adjust the delays if the LinkedIn interface takes longer to load each menu. LinkedIn’s layout may also change, requiring adjustments to element selectors.

Limitations
Dynamic Elements: LinkedIn may update its structure or attributes, which may break the script.
Rate Limiting: If LinkedIn detects too many interactions in a short time, it may temporarily restrict actions.
Troubleshooting
If you encounter issues, verify:

Selector Validity: Ensure the data-test-icon="overflow-web-ios-medium" selector still applies.
Timing Delays: Increase delays if menus load slowly.
Console Messages: Check console output for logs about each action.
