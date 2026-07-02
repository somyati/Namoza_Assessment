# Task 03 – Integration Design for OrthoNow

## Integration Architecture

The consultation landing page will submit the form data (Name, Phone, and Clinic Preference) to a secure backend API endpoint. I would use a **direct integration with the HubSpot CRM API** instead of Zapier or Make because it provides better reliability, lower latency, more control over error handling, and avoids additional third-party dependencies.

The flow would be:

**Landing Page → Backend API → HubSpot CRM API → Karix WhatsApp API → Google Ads Conversion Tracking**

When the form is submitted, the backend first checks whether a contact already exists in HubSpot using the patient's phone number. This step is important because HubSpot's default deduplication works primarily on email addresses, not phone numbers. Therefore, the backend should perform a search using a normalized phone number (stored in E.164 format). If a matching contact is found, the record is updated; otherwise, a new contact is created.

The contact will be stored with the following properties:

- Name
- Phone
- Clinic Preference
- Source = "Google Ads - Consultation Landing Page"
- Lead Status = "New Enquiry"

After HubSpot successfully creates or updates the contact, the backend calls the Karix WhatsApp Business API and sends a confirmation message to the patient acknowledging their enquiry.

Finally, the `consultation_form_submitted` conversion event is sent to Google Ads through Google Tag Manager and can also be reinforced using Enhanced Conversions for improved attribution.

## Biggest Failure Point

The biggest failure point is **phone number deduplication**. Since email is not collected on the form, relying on HubSpot's default behaviour may create duplicate contacts for the same patient. To avoid this, all phone numbers should be normalized to E.164 format and searched before every contact creation request.

## WhatsApp SLA (2 Minutes)

The two-minute SLA can fail due to API outages, network issues, backend failures, or message queue delays. To monitor this, the system should log the form submission timestamp and the WhatsApp sent timestamp. Alerts should be triggered if the delay exceeds 90 seconds. Failed messages should be retried automatically, and a dead-letter queue should store requests that continue to fail so they can be investigated manually.

This architecture provides reliable lead capture, proper CRM synchronization, timely patient communication, and accurate conversion tracking for campaign optimization.
