# 📸 Photo Print Order Portal

A lightweight, secure, single-file web application for photo printing businesses. It allows customers to select photos, adjust print sizes, customize cropping interactively, view real-time estimates, and submit print orders that sync directly with a Google Apps Script backend.

---

## 🌟 Features

- **📱 Mobile & Desktop Friendly:** Responsive design engineered to work smoothly on mobile browsers (includes a 16px font-size lock to prevent iPhone auto-zoom).
- **✂️ Interactive Crop Editor:** 
  - Drag, pinch, zoom, or slider-adjust crop windows per photo.
  - Supports switching between Portrait and Landscape orientations.
  - Generates live canvas thumbnails that reflect exact crop bounds.
- **⚠️ Low-Resolution Detection:** Automatically calculates photo DPI based on target print dimensions and alerts users if a photo may print soft ($<150\text{ DPI}$).
- **💰 Real-Time Pricing & Order Minimums:** Dynamic subtotal and tax calculation with automated order-minimum ($15.00) enforcement.
- **🛡️ Built-in Security:**
  - Includes a strict Content Security Policy (CSP).
  - Honeypot form field to trap simple automated bots.
  - Integrated Cloudflare Turnstile CAPTCHA option.
- **🚀 Google Apps Script Integration:** Uploads photo blobs and order metadata directly to a Google Sheets/Drive backend without needing an intermediate node server.

---

## 🛠️ Tech Stack & Dependencies

- **Frontend:** Plain HTML5, CSS3, JavaScript (ES6, zero external UI framework dependencies).
- **Backend:** Google Apps Script (`Code.gs`) bound to Google Drive & Google Sheets.
- **Protection (Optional):** Cloudflare Turnstile.

---

## 🚀 Setup & Installation

### 1. Google Apps Script Setup (Backend)

1. Create a new Google Sheet or Google Drive folder to store submitted orders.
2. Open **Extensions > Apps Script** in Google Sheets (or create a stand-alone Apps Script).
3. Implement a `doPost(e)` function in `Code.gs` that accepts JSON payloads containing:
   - Order metadata (`customerName`, `phoneNumber`, `deliveryAddress`, `deliveryInstructions`).
   - Encoded photo blobs and selected crop coordinates (`size`, `qty`, `orient`, `nx`, `ny`, `zoom`).
4. Deploy as a Web App:
   - **Execute as:** *Me*
   - **Who has access:** *Anyone*
5. Copy the generated Web App URL ending in `/exec`.

### 2. Frontend Configuration

Open `index.html` and update the configuration variables inside the `<script>` tag:

```javascript
// Paste your Google Apps Script Web App URL here:
const API_URL = '[https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec](https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec)';

// (Optional) Add your Cloudflare Turnstile Site Key:
const TURNSTILE_SITE_KEY = '0x4AAAAAA...';
