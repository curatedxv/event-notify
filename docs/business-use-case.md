# Discover, book, and attend an event
End-to-end flow of the event-notify platform: a venue owner lists a space, an organizer books it and publishes an event, a user finds the event, books a ticket, receives notifications, and gets checked in at the entrance. This single flow covers the core value of the platform for all actors.
## Actor(s)
- User (visitor / registered) — searches, books, attends
- Organizer — finds a venue, publishes and manages the event, validates tickets
- Venue owner — lists available spaces and confirms venue bookings
- System — reserves tickets, generates QR codes, sends notifications
## Trigger / preconditions
- **Trigger:** A user opens the platform to find an event to attend
- **Preconditions:** The venue owner has listed an available space; the organizer has a registered account; the user is registered (or registers during the flow)
## Main flow
1. Venue owner lists a space on the platform: location, capacity, available dates, rental terms
2. Organizer browses available venues, selects a suitable space, and sends a booking request for a date
3. Venue owner confirms the request; system marks the venue as booked for that date
4. Organizer creates an event in the dashboard (title, description, category, date, venue, ticket count, booking limit) and publishes it
5. System validates the data and adds the event to the public catalog
6. User browses the catalog, filters by keyword, category, date, or location
7. System shows matching events; user opens the event details page
8. User selects the number of tickets and confirms the booking
9. System checks availability, reserves the tickets, decreases the available count, and generates a QR code ticket
10. System sends a booking confirmation notification and shows the booking in the user's dashboard
11. System sends a reminder notification before the event starts
12. At the entrance, the user shows the QR code and the organizer scans it
13. System verifies the ticket (valid, for this event, not used yet) and marks it as checked-in
14. Organizer admits the user; attendance is recorded in the event statistics
## Alternate / edge cases
- **Venue request declined:** Venue owner rejects the booking request; organizer picks another venue or date
- **Venue date conflict:** System prevents double-booking a venue for the same date
- **No search results:** System shows an empty state and suggests clearing filters or browsing other categories
- **Tickets sold out:** Event stays visible but booking is disabled; if tickets sell out during booking, the system rejects it and informs the user
- **Booking limit exceeded:** System blocks booking more tickets than the organizer's per-user limit
- **User not logged in:** System redirects to login/registration and returns to the booking afterwards
- **User cancels the booking:** System releases the tickets back to availability and confirms the cancellation
- **Organizer edits the event:** System updates the event and notifies all users with active bookings about the change
- **Organizer cancels the event:** System removes the event from the catalog, cancels all bookings, notifies affected users, and releases the venue date
- **Notification delivery failure:** System retries; the information stays visible in the user's dashboard
- **Ticket already used or invalid:** System rejects the scan with a clear reason; organizer can look up the booking manually by name or booking ID
## Outcome
The user attended an event they would otherwise have missed; the organizer found a venue and reached an audience without overbooking; the venue owner filled a free date — all through one platform with accurate attendance data.
