# AI Voice Receptionist

An AI voice receptionist for small businesses, built with **Vapi**, **n8n** and **Google Sheets / Google Calendar**. It answers every call 24/7, quotes your real prices, checks availability, books the appointment and alerts the owner, so no booking is lost to a missed call.

Built for salons, clinics, academies, gyms and restaurants.

## What it does

- Answers business calls 24/7 as a natural conversation (no keypad menus)
- Detects the caller's language: Urdu or English (international version is English only)
- Quotes live prices for services and packages from Google Sheets
- Checks real availability in Google Calendar and books the appointment
- Logs every booking to a Google Sheet
- Alerts the owner by email and WhatsApp for each booking
- Transfers to a human if the caller wants to negotiate or asks for a person

## How it works

```
Caller ──► Phone number ──► Vapi voice agent
                                 │
                                 ▼
                          n8n webhook workflow
                ┌────────────────┼─────────────────┐
                ▼                ▼                 ▼
        Google Sheets     Google Calendar     Clients Registry
       (prices, bookings) (availability)      (per business config)
                                 │
                                 ▼
                  Owner alert: Gmail + WhatsApp Cloud API
```

1. A customer calls the business number, routed to the Vapi agent.
2. The agent talks with the caller and calls n8n tools to fetch prices and check free slots.
3. Once the caller confirms, n8n creates the calendar event and writes the booking to the sheet.
4. The owner gets the booking details by email and WhatsApp.
5. If the caller wants to negotiate or speak to someone, the call is transferred to a human.

## Multi client by design

- **One shared n8n workflow** serves every business.
- **One Clients Registry** sheet holds each client's config (sheet IDs, calendar, owner contacts, agent name).
- **One agent template per market**: bilingual Urdu/English for local clients, English only for international clients.
- The agent name is set per client (default persona: Sophie).
- A new business goes live by adding a row to the registry.

## Tech stack

| Layer | Tool |
|---|---|
| Voice agent | Vapi |
| Automation | n8n (self hosted, Docker) |
| Prices and bookings | Google Sheets |
| Availability and scheduling | Google Calendar |
| Owner alerts | Gmail, WhatsApp Cloud API |
| Telephony | Telnyx / Twilio compatible number |

## Setup

1. Import the n8n workflow JSON into your n8n instance.
2. Add credentials in n8n: Google Sheets, Google Calendar, Gmail and WhatsApp Cloud API.
3. Create the Clients Registry sheet and a price/booking sheet for each client.
4. Create the Vapi assistant from the prompt template, then point its tools at your n8n webhook URLs.
5. Connect a phone number to the Vapi assistant.
6. Add the business as a row in the Clients Registry and place a test call.

> Never commit API keys, tokens or webhook secrets. Keep them in n8n credentials or environment variables.

## Demo

Want to see it in action? Reach out and I will share a demo.

## Author

**Sameer Faisal**, AI Automation Engineer

- LinkedIn: [sameer-faisal-](https://www.linkedin.com/in/sameer-faisal-/)
- GitHub: [Sameer051022](https://github.com/Sameer051022)

Open to freelance AI automation projects.
