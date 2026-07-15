# event-notify
A web-based event aggregator for Europe that brings event discovery, ticket booking, and notifications into one place — helping people stop missing events and helping small organizers get noticed.
## Problem
Event information across Europe is scattered: organizers post events on their own websites, so people rarely discover them, forget about them, or miss them entirely. Small organizers have no affordable way to reach an audience. Payments are fragmented across PayPal, card providers, and door sales, and on fast-selling events there is no reliable way to determine who booked first.
## Vision
A single European platform where users find any event by category, book it in a few clicks, and never miss it thanks to timely notifications — while organizers of any size publish events, reach their audience, and manage attendance from one dashboard.
## Goals
- Aggregate events across Europe in one searchable, categorized catalog
- Let users book tickets and receive them as QR codes
- Keep users informed with notifications (confirmations, reminders, changes, cancellations)
- Give organizers a self-service dashboard to publish and manage events
- Provide a feedback channel so organizers can tell the platform what features they need
## Non-goals
- No mobile application — web only
- No physical / printed ticket sales
- No content moderation system or full admin panel
- No built-in payment processing at this stage (booking only; payment handled by organizers)
## Success signals
- The platform runs end-to-end: a user can find an event, book it, and receive a QR ticket and notifications
- All core scenarios pass functional testing
- An organizer can create and manage an event without developer involvement
## Scope
### MVP
- Event catalog with search and category filtering
- Ticket booking (without online payment)
- Notifications: booking confirmation, event reminders, change/cancellation alerts
- Organizer dashboard: create, edit, and manage events
- QR code tickets
### Later
- Integrated online payments (single checkout instead of fragmented PayPal/card/door payments)
- Fair-queue mechanism for fast-selling events (reliable "who booked first")
- Waitlist for sold-out events
- Venue partnerships — agreements with space owners so organizers can find venues through the platform
- Event recommendations based on user interests
## Open questions
- Which notification channels for MVP — email only, or email + browser push?
- Which payment provider(s) to integrate later (Stripe, PayPal, etc.)?
- How to verify organizers to prevent fake events without a moderation system?
- Single language (English) or multilingual UI for the European audience?
