# How to Identify and Obtain hCaptcha `rqdata`

## Introduction
When dealing with hCaptcha challenges, it's crucial to understand the importance of `rqdata`, especially if you're working on advanced automation or bypass techniques. The `rqdata` parameter is often a required component for successfully solving hCaptcha challenges, particularly in enterprise environments. This guide will walk you through how to identify, extract, and correctly use `rqdata` in your automation scripts.

## Step 1: Determine If `rqdata` is Necessary

The first step is to verify whether the hCaptcha you are trying to solve requires the submission of `rqdata`. Not submitting this data when necessary can lead to invalid tokens or high failure rates. Capsolver's captcha detection feature is a powerful tool that can help you determine if `rqdata` is required for the challenge at hand.

To explore Capsolver's captcha detection feature further, check out [Capsolver's Captcha Detector](https://www.capsolver.com/blog/Extension/identify-any-captcha-and-parameters).

When `rqdata` is necessary, Capsolver’s extension will notify you with a display panel similar to the one below:

![Capsolver extension display panel](https://assets.capsolver.com/prod/images/post/2023-11-21/7a1cf833-e03d-43c9-9519-590dcaad4816.png)

## Step 2: Locate the `rqdata` Value

Once you've identified that `rqdata` is required, the next step is to find and extract this value. Here’s a step-by-step guide:

### 1. Open the Inspect Element Tool
- Press `F12` to open the Developer Tools in your browser.
- Navigate to the **Network** tab.
- Activate the hCaptcha by interacting with it.

### 2. Capture the Request
Look for a request URL that resembles the following:

```
https://api.hcaptcha.com/getcaptcha/9928de2d-2800-4c58-be91-060e5a6aa117
```

The "sitekey" part of the URL (e.g., `9928de2d-2800-4c58-be91-060e5a6aa117`) will be unique to the site you are working with.

### 3. Inspect the Request Payload
- Click on the request to inspect its payload.
- In the payload, search for the `"rqdata"` parameter.

![Inspecting the payload](https://assets.capsolver.com/prod/images/post/2023-11-21/fe716b22-f15a-4ff0-92b4-b78d57d9bcc3.png)

Copy the value associated with `"rqdata"`.

### 4. Search for the `rqdata` Value
In the Developer Tools, press `CTRL + S` to open the search panel. Paste the `rqdata` value into the search field. This will help you locate the exact request that generated this value.

![Searching for rqdata in the network logs](https://assets.capsolver.com/prod/images/post/2023-11-21/c0ffbca2-f8c7-4892-bc1d-961986adcfdc.png)

### 5. Handle Edge Cases
In some cases, the `rqdata` value might be HTML encoded, encrypted, or stored elsewhere in the response. If the above method doesn’t work, you may need to inspect the response body of various requests until you find where the value originates.

## Step 3: Using `rqdata` in Your Requests

Once you’ve obtained the `rqdata` value, you need to include it in your request when attempting to solve the hCaptcha. Make sure to scrape a fresh `rqdata` value for each captcha submission, as this value changes with every challenge and submitting an outdated `rqdata` can lead to invalid tokens.

Here’s an example of how to specify this data in your request payload:

```json
 "enterprisePayload": {
      "rqdata": "[value]" // Optional, required if the site uses hCaptcha Enterprise
    }
```

## Troubleshooting Common Issues

### 1. Invalid `rqdata` Submission
If you’re encountering frequent failures, ensure that:
- You are obtaining a new `rqdata` value before each request.
- The `rqdata` value is correctly included in your request.

### 2. Handling Encryption or Encoding
If the `rqdata` appears encoded or encrypted, you may need to decode it before use. This could involve base64 decoding or JSON parsing, depending on how the value is formatted.

### 3. API Response Issues
If the API response returns errors, ensure:
- The site key and site URL are correctly specified.
- The `rqdata` is up-to-date and correctly formatted.

## Conclusion

Understanding and correctly using `rqdata` is essential for successfully solving hCaptcha challenges, particularly for enterprise-level captchas. By following the steps outlined in this guide, you can confidently identify, extract, and apply `rqdata` in your automation scripts.

**Remember:** Always use these techniques responsibly and in compliance with legal and ethical guidelines.
