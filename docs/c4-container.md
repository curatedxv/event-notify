# C4: Container

Zooms into event-notify to show its domain containers and how they communicate.
Each container owns a whole domain; its functions are shown one level down, at the
component level.

![C4 container diagram — event-notify decomposed into five domain containers: Venues, Events & Discovery, Ticketing & Admission, Notifications, and Identity & Access](c4-container.png)

> The `c4-container.png` bitmap is regenerated from the Mermaid source below.

<details>
<summary>Mermaid source</summary>

```mermaid
flowchart LR
 subgraph boundary["event-notify — domain containers"]
        venues["<b>Venues</b><br><i>Domain container</i><br>Venue listings and the<br>booking handshake between<br>organizers and owners"]
        events["<b>Events &amp; Discovery</b><br><i>Domain container</i><br>Event lifecycle — create,<br>edit, publish — plus the<br>public catalog, search,<br>and filtering"]
        ticketing["<b>Ticketing &amp; Admission</b><br><i>Domain container</i><br>Ticket reservations, QR<br>issuance, per-event limits,<br>and check-in at the door"]
        notifications["<b>Notifications</b><br><i>Domain container</i><br>Confirmations, reminders,<br>and cancellations over<br>email and SMS"]
        identity["<b>Identity &amp; Access</b><br><i>Shared domain container</i><br>Authenticates actors,<br>authorizes domain actions,<br>manages accounts and roles"]
 end
    venueOwner(["<b>Venue owner</b>"]) -- Lists venues; confirms or declines --> venues
    organizer(["<b>Organizer</b>"]) -- Requests a venue --> venues
    organizer -- Publishes, edits events --> events
    organizer -- Scans tickets at the door --> ticketing
    visitor(["<b>Visitor</b>"]) -- Searches, browses --> events
    visitor -- Books tickets --> ticketing
    support(["<b>Platform support</b>"]) -- Enables and disables user accounts --> identity

    venues -- Confirmed venue &amp; date --> events
    events -- Event &amp; capacity data --> ticketing
    events -- Event changed / cancelled --> notifications
    ticketing -- Booking made / cancelled --> notifications

    notifications -- Sends emails via --> emailProvider["<b>Email provider</b><br><i>External System</i>"]
    notifications -- Sends texts via --> smsProvider["<b>SMS provider</b><br><i>External System</i>"]

    emailProvider@{ shape: rounded}
    smsProvider@{ shape: rounded}
     venues:::container
     events:::container
     ticketing:::container
     notifications:::container
     identity:::shared
     visitor:::person
     organizer:::person
     venueOwner:::person
     support:::person
     emailProvider:::external
     smsProvider:::external
    classDef person fill:#08427b,stroke:#052e56,color:#fff
    classDef container fill:#1168bd,stroke:#0b4884,color:#fff
    classDef shared fill:#6b8fb5,stroke:#4a6e95,color:#fff
    classDef external fill:#999999,stroke:#6b6b6b,color:#fff
```

</details>
