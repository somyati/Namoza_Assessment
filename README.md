# Namoza Developer Assignment – OrthoNow (Client Web + Martech)

Candidate: Somya Tiwari
Role: Developer – Position 1 (Client Web + Martech)

## Assignment Overview

This repository contains my submission for the Namoza Developer Assignment for OrthoNow, an orthopaedic clinic chain operating across Bengaluru, Hyderabad, and Chennai.

The assignment consists of three deliverables:

1. GTM Event Schema
2. Landing Page Build
3. Integration Design

---

# Repository Structure

```text
namoza-ortho-assignment/
│
├── README.md
├── task-01/
│   └── gtm-schema.md
├── task-02/
│   └── pagespeed-screenshot.png
|   └── background.png
└── task-03/
|   └── integration-design.md
├── index.html
```

---

# Task 01 – GTM Event Schema

Deliverables:

- Complete GTM event schema for OrthoNow.
- Multi-step booking funnel tracking using custom dataLayer events.
- GA4 Funnel Exploration setup.
- Recommended Google Ads conversion event.

File:

```text
task-01/gtm-schema.md
```

---

# Task 02 – Landing Page Build

Features:

- Built using HTML, CSS, and Vanilla JavaScript.
- Single self-contained HTML file.
- Mobile responsive design.
- Minimal lead capture form (Name + Phone).
- Trust elements and primary CTA.
- `window.dataLayer.push()` fires on successful form submission.
- Thank-you state displayed without page reload.
- Optimized for Core Web Vitals and PageSpeed.

File:

Background Image:

```text
task-02/background.png
```

PageSpeed screenshot:

```text
task-02/pagespeed-screenshot.png
```

---

# Task 03 – Integration Design

Deliverables:

- End-to-end architecture connecting:
  - Landing Page
  - HubSpot CRM
  - Karix WhatsApp API
  - Google Ads Conversion Tracking

- Handling phone number deduplication in HubSpot.
- Failure handling and SLA monitoring strategy.

File:

```text
task-03/integration-design.md
```

# index.html

File:

```text
index.html
```

# Features Implemented

- Built using **HTML, CSS, and Vanilla JavaScript** only.
- Single self-contained file that runs directly in a browser.
- Mobile-responsive consultation landing page for OrthoNow.
- Clear headline and subheadline targeting patients with knee and back pain.
- Minimal lead capture form with only **Name** and **Phone Number** fields.
- Trust elements including:
  1. 4.8/5 patient rating
  2. 9 clinic locations
  3. 25,000+ patients treated

- Interactive hover and focus effects on form elements and CTA button.
- Thank-you state displayed without page reload after form submission.
- Background image and gradient overlay optimized for readability.

# GTM dataLayer Event

On successful form submission, the following event is pushed to the `dataLayer`:

```javascript
window.dataLayer.push({
  event: "consultation_form_submitted",
  patient_name_present: true,
  phone_length: 10,
  page_name: "consultation_landing_page",
  campaign_name: "google_ads_consultation",
});
```

This event can be captured in Google Tag Manager and forwarded to:

1. Google Analytics 4 (GA4)
2. Google Ads Conversion Tracking

---

# Technology Stack

- HTML5
- CSS3
- Vanilla JavaScript
- Google Tag Manager (GTM)
- Google Analytics 4 (GA4)
- HubSpot CRM API
- Karix WhatsApp Business API
- Google Ads Conversion Tracking

---

# Running the Landing Page Locally

1. Clone the repository:

```bash
git clone <repository-url>
```

2. Open:

```text
task-02/index.html
```

in any modern browser.

3. Open Developer Tools (`F12`) and submit the form.

4. Verify the event:

```javascript
window.dataLayer;
```

Expected output:

```javascript
[
  {
    event: "consultation_form_submitted",
    patient_name_present: true,
    phone_length: 10,
    page_name: "consultation_landing_page",
    campaign_name: "google_ads_consultation",
  },
];
```

---

# Loom Walkthrough

The Loom walkthrough covers:

1. GTM schema decisions.
2. Live demonstration of the landing page and `dataLayer.push()`.
3. Integration architecture and failure handling approach.

---

Thank you for reviewing my submission.
