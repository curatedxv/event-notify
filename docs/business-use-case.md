# Business use cases
Core value-delivering flows of the event-notify platform, each complete and valuable on its own.
## Actor(s)
- Visitor — a person looking for something to attend; browses the catalog, books tickets, and attends events
- Organizer — the person or team running an event; lists and manages events, sells tickets, and checks in attendees at the entrance
- Venue owner — the person or business that owns or manages a physical space; lists available spaces and confirms or declines booking requests from organizers
- Platform support — event-notify staff who step in when something goes wrong; helps resolve issues outside the normal flow (e.g., a visitor whose ticket didn't arrive, or a disputed check-in at the door)

---

## Book a venue
**Actors:** Organizer (primary) — books a venue; Venue owner — confirms or declines.
Organizer requests a venue for a date; venue owner confirms, declines, or the system blocks it if already booked. **Outcome:** organizer has a venue, venue owner fills the date.

## Publish an event
**Actors:** Organizer (primary) — creates and publishes an event.
Organizer fills in title, description, category, date, venue, and ticket count; system validates it and lists it in the public catalog, or rejects it with the missing/invalid fields. **Outcome:** the event is discoverable by visitors.

## Discover and book an event
**Actors:** Visitor (primary) — finds and books an event.
Visitor searches or filters the catalog, opens an event, and books tickets; system reserves them and issues a QR code, or blocks the booking if tickets are sold out, the limit is exceeded, or the visitor isn't logged in. **Outcome:** visitor holds a valid ticket and gets confirmation/reminder notifications.

## Check in at the entrance
**Actors:** Organizer (primary) — validates entry; Visitor — presents the ticket.
Visitor shows their QR code; organizer scans it and the system confirms it's valid, unused, and for this event, or rejects it with a reason if already used or invalid. **Outcome:** attendance is verified and recorded.

## Manage a venue listing
**Actors:** Venue owner (primary) — lists, edits, or removes a space.
Venue owner adds a space with location, capacity, available dates, and rental terms, or edits/removes it later; the system blocks removal or date changes that conflict with an already-confirmed booking. **Outcome:** the platform's venue catalog stays accurate and available for organizers to book.

## Resolve a support issue
**Actors:** Platform support (primary) — investigates and resolves; Visitor or Organizer — reports the issue.
A visitor or organizer reports a problem outside the normal flow (e.g., a missing ticket notification or a disputed check-in); platform support looks up the booking or event and manually corrects it — reissuing a ticket, reversing a check-in, or restoring a listing. **Outcome:** the reported issue is resolved without the affected user losing access.

## Submit platform feedback
**Actors:** Organizer (primary) — submits feedback.
Organizer sends a feature request or issue report through the feedback channel; the system records it and confirms receipt. **Outcome:** the platform has visibility into what organizers need next.
