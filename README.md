# 🌿 Dev Ayurveda — Invoice Generator Dashboard

> A professional, full-stack-ready Invoice Generator built with **React 18**, **jsPDF**, **SheetJS (xlsx)**, and **Firebase Firestore**. Designed for Ayurvedic businesses to generate GST-compliant PDF invoices, sync data to Firestore, and export accounting spreadsheets — all from one clean dashboard.

---

## ✨ Features

| Feature | Details |
|---|---|
| 📋 Dynamic Product Table | Add/remove rows with searchable product dropdown |
| 🧮 Auto Calculations | Subtotal, GST per line (5 / 12 / 18 %), Grand Total |
| 📄 PDF Invoice | Branded "Dev Ayurveda" PDF with jsPDF + AutoTable |
| 🖨 Print Preview | Opens PDF in browser print dialog |
| 📊 Excel Export | One-click `.xlsx` for accounting (SheetJS) |
| 🔥 Firebase Firestore | Saves full invoice object to `invoices` collection |
| 🧾 Invoice Numbering | Auto-generated unique invoice numbers (`DA-YYYY-XXXXX`) |
| ✅ Form Validation | Inline error states with helpful messages |
| 📈 Session Stats | Live revenue counter for the current session |
| 📱 Responsive | Works on desktop, tablet, and mobile |

---

## 🚀 Quick Start

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/dev-ayurveda-invoice.git
cd dev-ayurveda-invoice
```

### 2. Install dependencies
```bash
npm install
```

### 3. Configure Firebase
Create a `.env` file in the project root:
```env
VITE_FIREBASE_API_KEY=your_api_key_here
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
```
> Get these from [Firebase Console](https://console.firebase.google.com/) → Project Settings → Your Apps → Web App → SDK Config.

### 4. Enable Firestore in the code
In `src/App.jsx`, uncomment the Firebase block at the top (~lines 20–32) and inside `saveToFirestore()` (~line 140).

### 5. Run
```bash
npm run dev
```

---

## 📁 Project Structure

```
dev-ayurveda-invoice/
├── public/
│   └── favicon.ico
├── src/
│   ├── App.jsx          ← Main dashboard (all-in-one component)
│   └── main.jsx         ← React entry point
├── .env                 ← 🔒 Firebase secrets (never commit this)
├── .gitignore
├── index.html
├── package.json
├── vite.config.js
└── README.md
```

---

## 🛠 Tech Stack

| Library | Purpose |
|---|---|
| React 18 | UI & state management |
| jsPDF + jsPDF-AutoTable | PDF generation |
| SheetJS (xlsx) | Excel export |
| Firebase Firestore | Cloud database |
| Google Fonts | Playfair Display + DM Sans |
| Vite | Build tool |

---

## 📦 Dependencies

```json
{
  "dependencies": {
    "react": "^18.0.0",
    "react-dom": "^18.0.0",
    "jspdf": "^2.5.1",
    "jspdf-autotable": "^3.8.2",
    "xlsx": "^0.18.5",
    "firebase": "^10.0.0"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.0.0",
    "vite": "^5.0.0"
  }
}
```

---

## 🔥 Firebase Firestore Schema

Each generated invoice is stored in the `invoices` collection with this structure:

```json
{
  "invoiceNo"  : "DA-2025-73421",
  "clientName" : "Ramesh Sharma",
  "gstin"      : "07AABCD1234E1Z5",
  "mobile"     : "9876543210",
  "address"    : "123, MG Road, New Delhi",
  "datetime"   : "2025-08-15T14:30",
  "items": [
    {
      "product"  : "Ashwagandha Capsules",
      "qty"      : 2,
      "unitPrice": 450,
      "gstPct"   : 12
    }
  ],
  "totals": {
    "subtotal"  : 900,
    "totalGST"  : 108,
    "grandTotal": 1008
  },
  "createdAt": "Firebase ServerTimestamp"
}
```

---

## 🗂 Excel Export Columns

Each row in the exported `.xlsx` maps to one invoice line item:

`Invoice No | Date | Client Name | GSTIN | Mobile | Product | Quantity | Unit Price | GST % | GST Amount | Line Total | Subtotal | Total GST | Grand Total`

---

## 🔒 Security

- Never commit `.env` to Git. It is already listed in `.gitignore`.
- Add [Firebase Security Rules](https://firebase.google.com/docs/firestore/security/get-started) to restrict write access to authenticated operators only.
- Consider adding [Firebase Authentication](https://firebase.google.com/docs/auth) for operator login before deploying to production.

---

## 📝 Customization Checklist

- [ ] Replace `GSTIN: 07AABCD1234E1Z5` with your real GSTIN (search `07AABCD1234E1Z5` in `App.jsx`)
- [ ] Update business address and contact in the PDF header (`generatePDF` function)
- [ ] Add your logo: replace the circular placeholder in `generatePDF` with `doc.addImage(logoBase64, ...)`
- [ ] Expand `PRODUCT_LIST` array with your full product catalog
- [ ] Set up [Firebase Authentication](https://firebase.google.com/docs/auth) for secure operator access

---

## 🌐 Deploying to GitHub Pages / Vercel

### Vercel (recommended)
```bash
npm i -g vercel
vercel
# Follow prompts — add env vars in Vercel dashboard
```

### GitHub Pages
```bash
npm run build
# Deploy the dist/ folder using GitHub Actions or gh-pages package
```

---

## 📄 License

MIT © Dev Ayurveda. Built with 🌿 and ❤️.
