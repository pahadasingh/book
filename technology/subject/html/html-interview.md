Q.  Explain viewport Configuration
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=5.0">
```

The `<meta name="viewport">` tag is used in HTML to control the layout on mobile browsers. It helps ensure that your web page looks good on all devices by controlling the viewport's size and scale. Here’s a breakdown of the attributes used in your example:

1. **width=device-width**: This sets the width of the viewport to the width of the device, which means the web page will match the screen’s width in device-independent pixels.

2. **minimum-scale=1.0**: This sets the minimum zoom level to 1.0, meaning the user cannot zoom out beyond the actual size of the content.

3. **maximum-scale=5.0**: This sets the maximum zoom level to 5.0, allowing the user to zoom in up to five times the actual size of the content.

In summary, the provided meta tag ensures the web page adapts to the width of the user's device while allowing the user to zoom in up to five times but not zoom out beyond the actual size. This is useful for maintaining a good user experience across various devices and screen sizes.

Q.
