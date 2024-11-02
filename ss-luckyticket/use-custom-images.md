# Use Custom Images

#### Using Custom Ticket Images in SS-LuckyTicket with Base64 Encoding

To use custom images for the scratch tickets in _SS-LuckyTicket_, follow these steps to convert your images to Base64 format and update the `imageDataScript.js` file accordingly.

**Step 1: Convert Custom Images to Base64**

1. **Prepare Your Images**: Design or select custom images for each ticket type (e.g., Bronze, Silver, Gold). Save these images in `.png` or `.jpg` format.
2. **Convert to Base64**:
   * Use an online tool, like [base64-image.de](https://www.base64-image.de/) or [Image to Base64](https://www.base64encode.org/), to convert each image.
   * Upload the image to the tool, generate the Base64 code, and copy the resulting string.

**Step 2: Update `imageDataScript.js`**

In `imageDataScript.js`, each ticket type (`luckyticket`, `luckyticket2`, etc.) has its Base64 image data stored as a string.

1. **Locate the Ticket Definitions**:
   * You’ll see entries like `imageData["luckyticket"]`, `imageData["luckyticket2"]`, etc.
   * Each entry holds a Base64 string that represents the image for that specific ticket.
2. **Replace Base64 Strings**:
   * Replace the existing Base64 string with your new custom Base64-encoded image data. Ensure you keep the `data:image/png;base64,` prefix, as shown in the existing structure.

Example for updating the Bronze Ticket (luckyticket):

{% code overflow="wrap" %}
```javascript
imageData["luckyticket"] = 'data:image/png;base64, <Your Custom Base64 Data Here>';
imageData["luckyticket2"] = 'data:image/png;base64, <Your Custom Base64 Data Here>';
imageData["luckyticket3"] = 'data:image/png;base64, <Your Custom Base64 Data Here>';
```
{% endcode %}

Replace `<Your Custom Base64 Data Here>` with the Base64 string from your converted image.

**Step 3: Save and Test**

1. **Save Changes**: After pasting your new Base64 strings, save `imageDataScript.js`.
2. **Restart the Resource**: Restart _SS-LuckyTicket_ or the server to apply changes.
3. **Verify in Game**: Check each ticket type in the game to ensure the custom images display as expected.

***

Following these steps will allow users to replace the default ticket images with their own custom designs in _SS-LuckyTicket_.
