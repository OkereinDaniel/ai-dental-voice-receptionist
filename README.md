# AI Dental Voice Receptionist

An end-to-end AI voice receptionist and appointment automation system for dental clinics. The system turns inbound phone conversations into structured appointment requests, checks Google Calendar availability, creates confirmed appointments, writes booking data to a Supabase CRM, and provides appointment reporting.

## What this solves

Dental reception teams can lose time handling repetitive calls, collecting patient details, checking calendars, creating appointments, and updating CRM records manually. This project connects those steps into one automated workflow.

## Architecture

```text
Patient phone call
        |
        v
Vapi AI Voice Receptionist
        |
        | appointment details
        v
n8n Production Workflow
        |
   +----+----------------+
   |                     |
   v                     v
Google Calendar      Supabase CRM
Availability         Appointment Record
   |                     |
   +----------+----------+
              v
      Patient Confirmation
              |
              v
     Appointment Reporting
```

## Core workflow

1. The AI receptionist answers an inbound call.
2. The assistant collects patient name, phone number, patient type, appointment type, preferred date, preferred time, and timezone.
3. n8n validates and normalizes the appointment request.
4. Google Calendar is checked for availability.
5. If the requested slot is available, the appointment is created.
6. The confirmed booking is sent to the Supabase CRM.
7. Invalid requests and unavailable slots follow separate response paths.
8. Appointment activity is summarized in an Observability dashboard.

## Reliability and accuracy features

- Production webhook-based automation
- Separate validation and unavailable-slot handling
- CRM data normalization
- Google Calendar availability checking
- Supabase persistence
- Background speech denoising for voice calls
- Dental-domain transcription context
- Automatic transcriber fallback
- Appointment reporting by type, status, and time

## Technology

- Vapi — AI voice receptionist and phone interface
- n8n — workflow orchestration and business logic
- Google Calendar — availability and appointment scheduling
- Supabase/PostgreSQL — CRM database and reporting
- OpenAI — conversational model used by the receptionist

## Portfolio notes

This repository contains the non-secret project structure and documentation. Production credentials, API keys, private webhook secrets, real patient records, and other sensitive configuration are intentionally excluded.

## Important security note

Before publishing any workflow export or configuration file, remove credentials, tokens, authorization headers, private webhook URLs, personal phone numbers, private calendar IDs, and real patient/customer information. Use environment variables or placeholders for deployment-specific values.

## Testing approach

The system was tested as an external-user flow rather than relying only on manual n8n execution. A caller can place an inbound call, complete an appointment conversation, trigger the production workflow automatically, and verify the booking in Google Calendar and Supabase.
