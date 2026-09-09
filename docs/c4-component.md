# C4: Component

Zooms into each domain container from [c4-container.md](c4-container.md).
Grey nodes are outside the container in focus.

## Venues

```mermaid
flowchart LR
    owner(["<b>Venue owner</b>"]):::ext
    organizer(["<b>Organizer</b>"]):::ext
    events["<b>Events &amp; Discovery</b><br><i>Container</i>"]:::ext

    subgraph venues["Venues"]
        directory["<b>Venue Directory</b><br><i>Component</i><br>Venue listings: address,<br>capacity, photos"]
        calendar["<b>Availability Calendar</b><br><i>Component</i><br>Free / held dates per venue"]
        requests["<b>Booking Requests</b><br><i>Component</i><br>Organizer asks for a venue<br>and date; places a hold"]
        confirm["<b>Confirmation Workflow</b><br><i>Component</i><br>Owner confirms or declines;<br>commits or releases the hold"]
    end

    owner -- Manages listings --> directory
    owner -- Confirms / declines --> confirm
    organizer -- Requests a venue --> requests
    requests -- Reads venue --> directory
    requests -- Places hold --> calendar
    confirm -- Commits / releases hold --> calendar
    confirm -- Confirmed venue &amp; date --> events

    classDef component fill:#1168bd,stroke:#0b4884,color:#fff
    classDef ext fill:#999999,stroke:#6b6b6b,color:#fff
    class directory,calendar,requests,confirm component
```

## Events & Discovery

```mermaid
flowchart LR
    organizer(["<b>Organizer</b>"]):::ext
    visitor(["<b>Visitor</b>"]):::ext
    venues["<b>Venues</b><br><i>Container</i>"]:::ext
    ticketing["<b>Ticketing &amp; Admission</b><br><i>Container</i>"]:::ext
    notifications["<b>Notifications</b><br><i>Container</i>"]:::ext

    subgraph events["Events &amp; Discovery"]
        authoring["<b>Event Authoring</b><br><i>Component</i><br>Creates and edits draft events;<br>attaches the confirmed venue"]
        publishing["<b>Publishing</b><br><i>Component</i><br>Validates a draft, publishes it,<br>emits lifecycle events"]
        catalog["<b>Catalog</b><br><i>Component</i><br>Published events for<br>public reads"]
        search["<b>Search &amp; Filtering</b><br><i>Component</i><br>Query by city, date, category"]
    end

    organizer -- Creates / edits --> authoring
    venues -- Confirmed venue &amp; date --> authoring
    authoring -- Submits --> publishing
    publishing -- Publishes to --> catalog
    visitor -- Browses --> catalog
    visitor -- Searches --> search
    search -- Reads --> catalog
    publishing -- Event &amp; capacity data --> ticketing
    publishing -- Event changed / cancelled --> notifications

    classDef component fill:#1168bd,stroke:#0b4884,color:#fff
    classDef ext fill:#999999,stroke:#6b6b6b,color:#fff
    class authoring,publishing,catalog,search component
```

## Ticketing & Admission

```mermaid
flowchart LR
    visitor(["<b>Visitor</b>"]):::ext
    organizer(["<b>Organizer</b>"]):::ext
    events["<b>Events &amp; Discovery</b><br><i>Container</i>"]:::ext
    notifications["<b>Notifications</b><br><i>Container</i>"]:::ext

    subgraph ticketing["Ticketing &amp; Admission"]
        reservation["<b>Reservation</b><br><i>Component</i><br>Books a ticket; enforces<br>the per-event limit"]
        capacity["<b>Capacity Ledger</b><br><i>Component</i><br>Remaining seats per event"]
        qr["<b>QR Issuance</b><br><i>Component</i><br>Signs a QR token per<br>confirmed ticket"]
        checkin["<b>Check-in</b><br><i>Component</i><br>Validates a scanned QR<br>at the door"]
        attendance["<b>Attendance Records</b><br><i>Component</i><br>Who was admitted, when"]
    end

    events -- Event &amp; capacity data --> capacity
    visitor -- Books a ticket --> reservation
    reservation -- Reserves / releases seat --> capacity
    reservation -- Requests token --> qr
    organizer -- Scans at the door --> checkin
    checkin -- Verifies token --> qr
    checkin -- Records admission --> attendance
    reservation -- Booking made / cancelled --> notifications

    classDef component fill:#1168bd,stroke:#0b4884,color:#fff
    classDef ext fill:#999999,stroke:#6b6b6b,color:#fff
    class reservation,capacity,qr,checkin,attendance component
```

## Notifications

```mermaid
flowchart LR
    events["<b>Events &amp; Discovery</b><br><i>Container</i>"]:::ext
    ticketing["<b>Ticketing &amp; Admission</b><br><i>Container</i>"]:::ext
    emailProvider["<b>Email provider</b><br><i>External System</i>"]:::ext
    smsProvider["<b>SMS provider</b><br><i>External System</i>"]:::ext

    subgraph notifications["Notifications"]
        intake["<b>Event Intake</b><br><i>Component</i><br>Turns domain events into<br>notification intents"]
        scheduler["<b>Reminder Scheduler</b><br><i>Component</i><br>Schedules reminders;<br>retracts on cancellation"]
        composer["<b>Message Composer</b><br><i>Component</i><br>Renders a template for the<br>recipient, locale, channel"]
        emailDispatch["<b>Email Dispatcher</b><br><i>Component</i>"]
        smsDispatch["<b>SMS Dispatcher</b><br><i>Component</i>"]
        log["<b>Delivery Log</b><br><i>Component</i><br>What was sent; dedupe, retry"]
    end

    events -- Event changed / cancelled --> intake
    ticketing -- Booking made / cancelled --> intake
    intake -- Immediate --> composer
    intake -- Later --> scheduler
    scheduler -- Due --> composer
    composer -- Email --> emailDispatch
    composer -- SMS --> smsDispatch
    emailDispatch -- Sends via --> emailProvider
    smsDispatch -- Sends via --> smsProvider
    emailDispatch -- Outcome --> log
    smsDispatch -- Outcome --> log

    classDef component fill:#1168bd,stroke:#0b4884,color:#fff
    classDef ext fill:#999999,stroke:#6b6b6b,color:#fff
    class intake,scheduler,composer,emailDispatch,smsDispatch,log component
```

## Identity & Access

```mermaid
flowchart LR
    support(["<b>Platform support</b>"]):::ext
    actor(["<b>Any actor</b>"]):::ext
    domains["<b>Domain containers</b>"]:::ext

    subgraph identity["Identity &amp; Access"]
        authn["<b>Authentication</b><br><i>Component</i><br>Signs actors in; issues<br>a session token"]
        authz["<b>Authorization</b><br><i>Component</i><br>Decides whether an actor<br>may perform an action"]
        accounts["<b>Account Management</b><br><i>Component</i><br>User records; enabled<br>or disabled"]
        roles["<b>Role Management</b><br><i>Component</i><br>Roles held per account"]
    end

    actor -- Signs in --> authn
    support ~~~ authn
    support -- Enables / disables accounts --> accounts
    domains -- Authorizes request --> authz
    authn -- Checks account --> accounts
    authz -- Reads roles --> roles
    authz -- Reads account state --> accounts

    classDef component fill:#1168bd,stroke:#0b4884,color:#fff
    classDef ext fill:#999999,stroke:#6b6b6b,color:#fff
    class authn,authz,accounts,roles component
```
