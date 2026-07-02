# Task 01 – GTM Event Schema for OrthoNow

## Website Interactions to Track

- Appointment Booking Form (3-step)
- Call Now buttons
- WhatsApp Chat Widget
- Download Patient Guide
- Clinic Location Page Views
- Blog Article Engagement

---

# 1. GTM Event Schema

| Event Name                  | Trigger Type             | Key Parameters                                  | GA4 Report / Audience                   |
| --------------------------- | ------------------------ | ----------------------------------------------- | --------------------------------------- |
| page_view                   | Page View Trigger        | page_location, page_title, page_referrer        | Standard GA4 Reports                    |
| clinic_page_view            | Page View Trigger        | clinic_name, city, page_url                     | Audience: Interested in Specific Clinic |
| booking_form_started        | Custom Event             | clinic_location, specialty, page_name           | Booking Funnel Analysis                 |
| booking_step_complete       | Custom Event (dataLayer) | step_number, step_name, clinic_location         | GA4 Funnel Exploration                  |
| booking_completed           | Custom Event (dataLayer) | booking_id, clinic_location, specialty          | Primary Conversion Report               |
| call_now_click              | Click Trigger            | phone_number, page_name, button_location        | Lead Attribution Report                 |
| whatsapp_click              | Click Trigger            | page_name, clinic_name, destination_url         | Audience: WhatsApp Engaged Users        |
| patient_guide_form_submit   | Form Submission          | patient_name_present, phone_present, guide_name | Lead Generation Report                  |
| patient_guide_download      | Link Click Trigger       | guide_name, file_name, page_name                | Download Performance Report             |
| blog_scroll_25              | Scroll Trigger           | article_title, category, scroll_percent         | Content Engagement                      |
| blog_scroll_50              | Scroll Trigger           | article_title, category, scroll_percent         | Content Engagement                      |
| blog_scroll_75              | Scroll Trigger           | article_title, category, scroll_percent         | Engaged Reader Audience                 |
| blog_scroll_90              | Scroll Trigger           | article_title, category, scroll_percent         | Highly Engaged Reader Audience          |
| consultation_form_submitted | Custom Event             | page_name, campaign_name, form_type             | Google Ads Conversion                   |

---

# 2. Booking Form Funnel Tracking

The booking journey consists of:

1. Select Clinic Location + Specialty
2. Enter Patient Details
3. Confirm Booking

Since this is a multi-step form, the front-end developer should push events into the `dataLayer` whenever a step is completed. GTM listens to these events and sends them to GA4.

---

## Step 1 – Location and Specialty Selected

### dataLayer Push

```json id="ewtk3r"
{
  "event": "booking_step_complete",
  "step_number": 1,
  "step_name": "location_specialty_selected",
  "clinic_location": "Indiranagar",
  "specialty": "Knee Pain"
}
```

### GTM Trigger

- Trigger Type: Custom Event
- Event Name: `booking_step_complete`
- Condition: `step_number = 3`

---

## Step 2 – Patient Details Entered

### dataLayer Push

```json id="z2lpg8"
{
  "event": "booking_step_complete",
  "step_number": 2,
  "step_name": "patient_details_entered",
  "clinic_location": "Indiranagar",
  "patient_name_present": true,
  "phone_present": true,
  "preferred_date": "2026-07-15"
}
```

### GTM Trigger

- Trigger Type: Custom Event
- Event Name: `booking_step_complete`
- Condition: `step_number = 2`

---

## Step 3 – Booking Confirmed

### dataLayer Push

```json id="5kll0l"
{
  "event": "booking_step_complete",
  "step_number": 3,
  "step_name": "booking_confirmed",
  "clinic_location": "Indiranagar",
  "booking_id": "ORT12345",
  "specialty": "Knee Pain"
}
```

---

## Final Booking Conversion Event

```json id="wp0j61"
{
  "event": "booking_completed",
  "booking_id": "ORT12345",
  "clinic_location": "Indiranagar",
  "specialty": "Knee Pain",
  "appointment_date": "2026-07-15"
}
```

---

# 3. GA4 Funnel Exploration Setup

Create a Funnel Exploration using:

| Funnel Step | Event Condition                             |
| ----------- | ------------------------------------------- |
| Step 1      | booking_step_complete where step_number = 1 |
| Step 2      | booking_step_complete where step_number = 2 |
| Step 3      | booking_step_complete where step_number = 3 |

This setup will show:

- Drop-off between Step 1 and Step 2
- Drop-off between Step 2 and Step 3
- Overall booking conversion rate
- High-converting clinic locations and specialties

---

# 4. Google Ads Conversion to Import

## Conversion Event:

`booking_completed`

## Why this event?

`booking_completed` represents a confirmed patient appointment and is the closest event to actual business revenue.

Events such as:

- `call_now_click`
- `whatsapp_click`
- `booking_form_started`

are micro-conversions and may not indicate strong purchase intent.

Importing `booking_completed` into Google Ads provides the highest-quality conversion signal and allows Smart Bidding to optimise campaigns toward confirmed appointments rather than intermediate interactions.
