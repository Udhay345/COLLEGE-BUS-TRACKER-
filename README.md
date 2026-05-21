# 🚌 RIT Bus Tracker

A real-time college bus tracking web application for **Rajalakshmi Institute of Technology (RIT)**. Drivers share their live GPS location via Firebase Realtime Database, and students can track buses and calculate ETAs from the student-facing map.

![App Preview](bus-vector.webp)

---

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Screenshots / Pages](#screenshots--pages)
- [Prerequisites](#prerequisites)
- [Setup & Configuration](#setup--configuration)
- [Firebase Setup](#firebase-setup)
- [Google Maps API Setup](#google-maps-api-setup)
- [Running the App](#running-the-app)
- [Bus Routes](#bus-routes)
- [Security Notes](#security-notes)
- [Contributing](#contributing)
- [License](#license)

---

## ✨ Features

- 🗺️ **Live Driver Tracking** – Drivers share GPS location in real-time via the browser's Geolocation API
- 📍 **Student Map View** – Students can see bus position, select stops, and get distance & ETA
- 🔐 **Driver Login** – Simple Bus ID + password authentication to access the driver dashboard
- 🛑 **Route & Stop Management** – Pre-configured stops per bus route with marker overlays
- 🔔 **Live Updates** – Firebase Realtime Database provides instant location syncing
- 📱 **Responsive Design** – Mobile-first UI works on phones and desktops
- 💫 **Splash Screen** – Animated RIT logo intro screen
- 📞 **Contact Page** – Driver contact numbers for each route

---

## 🛠️ Tech Stack

| Layer        | Technology |
|--------------|------------|
| Frontend     | HTML5, CSS3, Vanilla JavaScript |
| Maps (Driver)| Google Maps JavaScript API |
| Maps (Student)| Leaflet.js + OpenStreetMap |
| Routing      | Leaflet Routing Machine |
| Backend/DB   | Firebase Realtime Database |
| Fonts        | Google Fonts (Poppins, Montserrat) |
| Icons        | Font Awesome 6 |

---

## 📁 Project Structure

```
rit-bus-tracker/
│
├── splash.html          # Animated splash screen (entry point)
├── index1.html          # Home page — Driver / Student role selection
├── driver-login.html    # Driver authentication page
├── driver-map.html      # Driver's live location sharing map (Google Maps)
├── student-map.html     # Student bus tracking map (Leaflet + OSM)
├── contact.html         # Driver contact numbers page
│
├── map.json             # Sample bus data schema (template only)
│
├── rit-logo.png         # RIT college logo
├── bus-vector.jpg       # Bus vector illustration
├── bus-vector.webp      # Bus vector illustration (WebP)
├── bus_stop.png         # Bus stop marker icon
├── bus_stop.jpg         # Bus stop image
├── bus_driver.png       # Bus driver marker icon
│
├── .gitignore           # Git ignore rules
└── README.md            # This file
```

---

## 📸 Screenshots / Pages

| Page | Description |
|------|-------------|
| **splash.html** | Animated logo intro, auto-redirects to Home |
| **index1.html** | Landing page — choose Driver or Student mode |
| **driver-login.html** | Login form for bus drivers |
| **driver-map.html** | Google Maps view; driver starts/stops location sharing |
| **student-map.html** | Leaflet map; students select route & stop to see ETA |
| **contact.html** | Contact numbers for each bus route driver |

---

## ✅ Prerequisites

- A modern web browser (Chrome, Firefox, Edge)
- A **Firebase** project with **Realtime Database** enabled
- A **Google Maps JavaScript API** key (for the driver map)
- A static file server (e.g., VS Code Live Server, `npx serve`, Python `http.server`)

---

## ⚙️ Setup & Configuration

### 1. Clone the Repository

```bash
git clone https://github.com/Udhay345/COLLEGE-BUS-TRACKER-.git
cd COLLEGE-BUS-TRACKER-
```

### 2. Configure Firebase

Open **both** `driver-map.html` and `student-map.html` and replace the placeholder Firebase config with your actual project credentials:

```javascript
// ⚠️ Replace these placeholders with your actual Firebase project config.
// Find your config in Firebase Console > Project Settings > Your Apps.
const firebaseConfig = {
  apiKey: "YOUR_FIREBASE_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT_ID-default-rtdb.asia-southeast1.firebasedatabase.app",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT_ID.appspot.com",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID",
  measurementId: "YOUR_MEASUREMENT_ID"   // driver-map.html only
};
```

### 3. Configure Google Maps API Key

In `driver-map.html`, replace the placeholder in the script tag:

```html
<!-- Replace YOUR_GOOGLE_MAPS_API_KEY with your actual Google Maps API key -->
<script src="https://maps.googleapis.com/maps/api/js?key=YOUR_GOOGLE_MAPS_API_KEY"></script>
```

### 4. Configure Driver Credentials

In `driver-login.html`, replace the placeholder Bus IDs and password:

```javascript
// ⚠️ Replace with your actual Bus IDs and a secure password.
// In production, move authentication to a backend or Firebase Auth.
const validBusIds = ["BUS_ID_1", "BUS_ID_2", "BUS_ID_3", "BUS_ID_4"];
const validPassword = "YOUR_DRIVER_PASSWORD";
```

---

## 🔥 Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/) and create a new project.
2. Navigate to **Build → Realtime Database** and click **Create Database**.
3. Choose your region (e.g., `asia-southeast1`) and start in **test mode** (you can tighten rules later).
4. Set the following Realtime Database rules for basic security:

```json
{
  "rules": {
    "buses": {
      "$busId": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```

> ⚠️ For production, restrict write access to authenticated driver users.

5. Go to **Project Settings → Your Apps → Web App** and copy the `firebaseConfig` object into both map files.

---

## 🗺️ Google Maps API Setup

1. Go to [Google Cloud Console](https://console.cloud.google.com/).
2. Create or select a project.
3. Navigate to **APIs & Services → Library** and enable **Maps JavaScript API**.
4. Go to **APIs & Services → Credentials** and create an **API Key**.
5. **Restrict the key** to your domain for security.
6. Paste the key into `driver-map.html` as described above.

---

## 🚀 Running the App

Since this is a plain HTML/JS app, you need a local HTTP server (not `file://`) for Geolocation and Firebase to work correctly.

**Option 1 — VS Code Live Server** (Recommended)
- Install the [Live Server extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
- Right-click `splash.html` → **Open with Live Server**

**Option 2 — npx serve**
```bash
npx serve .
```
Then open `http://localhost:3000/splash.html`

**Option 3 — Python**
```bash
python -m http.server 8080
```
Then open `http://localhost:8080/splash.html`

---

## 🚌 Bus Routes

The app supports the following configurable routes (update in `student-map.html`):

| Route | Default Stops |
|-------|--------------|
| BUS_ID_1 | Stop A, Stop B |
| BUS_ID_2 | Stop A, Stop B |
| BUS_ID_3 | Stop A, Stop B, Stop C, Stop D |
| BUS_ID_4 | Stop A, Stop B |

> Edit the `busStops` object in `student-map.html` to set real stop coordinates for your institution.

---

## 🔒 Security Notes

> **⚠️ Important before deploying:**

- **Never commit real API keys** to a public repository. All keys in this repo are placeholders.
- Move driver authentication to **Firebase Authentication** for production — the current hardcoded password approach is for development/demo only.
- **Restrict your Google Maps API key** to specific HTTP referrers in the Google Cloud Console.
- **Restrict your Firebase API key** using [Firebase Security Rules](https://firebase.google.com/docs/rules).
- Consider enabling **App Check** in Firebase for additional protection against abuse.

---

## 🤝 Contributing

1. Fork this repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m 'Add my feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 👤 Authors

- **Udhay** — [GitHub](https://github.com/Udhay345)

> Built as a college project for Rajalakshmi Institute of Technology (RIT).
