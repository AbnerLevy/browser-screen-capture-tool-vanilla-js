# 📸 Helpdesk Screen Capture & Ticket Attachment Tool

> Streamlining tech support by allowing users to capture and attach screenshots directly from their browser.

[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen)](https://abnerlevy.github.io/browser-screen-capture-tool-vanilla-js/)

Non-technical or elderly users often struggle to take manual screenshots, save them, and upload them correctly. This lightweight, vanilla JavaScript utility is a tool to solves that friction by leveraging the browser's native Web API (`navigator.mediaDevices.getDisplayMedia`) to let users capture, preview, and attach screenshots directly to their active support tickets with just a few clicks—no external software or extensions required.

---

## 🚨 The Problem

In any support or helpdesk workflow, getting clear visual context from users is a major bottleneck because many clients:
- Do not know how to take a screenshot on their operating system.
- Do not know how to save or find the image file on their local machine.
- Send incomplete, blurry photos taken with their mobile phones.
- Face a slow, non-standardized attachment process.

This friction leads to back-and-forth emails, misunderstandings, and significantly increases the **Ticket Resolution Time (MTTR)**.

---

## 💡 The Solution

This utility introduces an integrated web feature that allows users to:
- Capture their screen or specific app window directly inside the web app.
- Bypass the need to save files locally on their device.
- Review and preview the screenshot inside a modal before attaching it.
- Seamlessly bind the image to the active support ticket payload.

Everything is handled natively, without depending on heavy third-party libraries or browser extensions.

---

## ⚙️ How it Works

1. The user clicks the screenshot/capture button.
2. The browser prompts the user to select which tab, window, or entire screen to capture.
3. The system takes a snapshot of the selected target.
4. A modal instantly displays a live preview of the captured image.
5. The user confirms and attaches the image.
6. The screenshot data is converted and prepared for server-side upload.

---

## 🖼️ Demo

<img width="1260" height="639" alt="Tool Demo Animation" src="https://github.com/user-attachments/assets/3ceb3862-569b-4974-a1b3-de43170a8e24" />

> ⚠️ **Important Project Notes:**
> - The provided `index.html` file is strictly a **live demonstration**. The core purpose of this repository is for you to extract the JavaScript logic and implement it into your own custom layout or ticketing system.
> - The final submission button is a mock representation. You must hook your own API or backend upload logic into it.
---

## 🚀 Features

- **Built for Helpdesks:** Streamlines the customer support workflow by making bug reporting foolproof for non-tech-savvy clients.
- **Zero Dependencies:** Light, pure vanilla JavaScript utilizing native modern browser Web APIs.
- **Interactive Preview Modal:** Users can see exactly what they captured before confirming the attachment.
- **Base64 String Pipeline:** Converts the screen capture directly into an `image/png` Data URL, making it incredibly easy to pipe into your current ticket creation payload.
- **Seamless Form Integration:** Appends the captured image to the DOM as a visible attachment and unlocks final form submission.

---

## 🛠️ How to Integrate This Tool Into Your Own System

The `index.html` and `script.js` files provided in this repository are **boilerplate templates**. You don't need to use them as-is. Instead, you can easily map their structure to adapt this feature directly into your existing contact forms, helpdesks, or ticketing layouts.

To make the code work seamlessly with your platform, you only need to link your existing UI components to the specific IDs expected by our JavaScript engine.

### 1. Map Your HTML Form Elements
Ensure your current ticketing page includes or maps to these core interactive elements:

*   **The Trigger:** A button on your form to initiate the flow (corresponds to `#openModalBtn`).
*   **The Modal UI:** An overlay modal containing controls to start the capture (`#startCaptureBtn`), confirm the attachment (`#sendImageBtn`), cancel the operation (`#closeModalBtn`), and an image tag (`#previewImage`) to visually render the captured frame.
*   **The Attachment Zone:** A `div` wrapper where thumbnails of confirmed screenshots will dynamically render (`#anexos`).
*   **The Submit Hook:** Your platform's native ticket submission button (`#finalSendBtn`), which unlocks as soon as an active attachment is captured.

---

### 2. Adaptation Blueprint

Here is how you bridge your current setup with the repository logic:

#### Step A: Keep or Re-assign IDs
If you already have a stylized modal or custom buttons in your system, you can either change your HTML attributes to match the IDs used in `script.js` or update the query selectors at the top of `script.js` to point to your existing element classes/IDs:

```javascript
// Change these strings if your helpdesk uses different IDs
const openModalBtn = document.getElementById('YOUR_CUSTOM_TRIGGER_ID');
const captureModal = document.getElementById('YOUR_CUSTOM_MODAL_ID');
// ... bind the remaining elements accordingly
```

#### Step B: Capture and Pipeline Payload (Base64 Data)

When a non-technical user successfully triggers the capture, the script saves the frame into a global string variable called `capturedImageData` formatted as an **encoded Base64 PNG Data URL** (`data:image/png;base64,...`).

To actually save this in your database or link it to a real support ticket, customize the simulated submission handler inside `script.js`:
```javascript
function enviarParaServidor() {
  if (capturedImageData) {
    console.log('Sending Base64 payload data to your Helpdesk Ticket API...');
    
    // 👇 IMPLEMENT YOUR REAL BACKEND API POST HERE 👇
    fetch('/api/v1/support/tickets', {
       method: 'POST',
       headers: { 'Content-Type': 'application/json' },
       body: JSON.stringify({ 
         user_email: document.getElementById('userEmailField').value,
         ticket_description: document.getElementById('ticketDescriptionField').value,
         screenshot: capturedImageData // Your backend can process this string back into an image file
       })
    })
    .then(response => response.json())
    .then(data => alert('Ticket and screenshot successfully transmitted!'))
    .catch(err => console.error('Upload failed:', err));
  }
}
