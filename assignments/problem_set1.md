# Problem Set 1: Reading and Writing Concepts

## Exercise 1: Reading a Concept
1. **Invariants:** What are two invariants of the state? Say which one is more important and why; identify the action whose design is most affected by it, and say how it preserves it.
- The sum of the `counts` in `Purchases` should not exceed the `count` Number for that `Request`
- The item field in each `Purchase` in `Purchases` must exist in `Requests`

- The second invariant listed is more important--a user can not purchase and item that is not requested. This is more important because the whole purpose of the concept is to give the registration creator the gifts that they want, and not upholding this invariant would defeat the purpose. The `GiftRegistration` owners' design is most affected by it, as they need to ensure that users are ONLY allowed to purchase items that are requested.
2. **Fixing an Action:** Can you identify an action that potentially breaks this important invariant, and say how this might happen? How might this problem be fixed?
- Let's say I have a request for 2 hamburgers and someone buys 1 for me. If I then call `removeItem(registry, hamburger)` then there exists a `Purchase` for an item no longer in `Requests`, breaking the invariant. We can fix this problem by adding a precondition to the `removeItem` action: **requires** no purchases exist for this item.
3. **Inferring Behavior:** By reading the specs of the concept actions, say whether a registry can be opened and closed repeatedly. What is a reason to allow this?
- A registry ***can*** be opened and closed repeatedly. Nothing in the pre or postconditions prevent this from happening. We would want to allow this because in the case where a user changes their mind and open/closes a registry a bunch of times, we wouldn't want them to have to recreate their registry if say we prevented reopening after a registry is closed.
4. **Registry Deletion:** There is no action to delete a registry. Would this matter in practice?
- Since not having a `delete` action does not break any invariants, the concept can function without it. However, when we take database storage into account, there could be an argument made for the capability to delete registries.
5. **Queries:** What are two common queries likely to be executed against the concept state?
- The registry owner is likely to query what items have been purchased in their registry.
- A gift giver is likely to query what gifts have not met their item count yet (what gifts they can still purchase).
6. **Hiding Purchases:** A common feature of gift registries is to allow the recipient to choose not to see purchases so that an element of surprise is retained. How would you augment the concept specification to support this?
- We would add a `hiddenPurchases` boolean flag to each registry. We would also want to add actions `hidePurchases(r: Registry)` and `showPurchases(r: Registry)` to enable the toggling of this feature.
7. **Generic Types:** Generic types for the items specifically give more flexibility in ways to represent the same item. Since the same item can (most likely) be purchased from many places, we would want to group similar items, even if their description, price, or place or purchase might be different.

## Exercise 2: Extending a Familiar Concept
1-2.\
**concept** PasswordAuthentication \
**purpose** limit access to known users \
**principle** after a use registers with a username and password, they can authenticate with that same username and password and can be treated each time as the same user \
**state**\
&nbsp;&nbsp;a set of `Users` with \
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: yellow">    a username String<span>\
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: yellow">    a password String<span>\
**actions**\
&nbsp;&nbsp;`register(username: String, password: String): (user: User)`\
&nbsp;&nbsp;&nbsp;&nbsp; **requires** username does not exist\
&nbsp;&nbsp;&nbsp;&nbsp; **effect** create and return newly created user, add user to Users\
&nbsp;&nbsp;`authenticate (username: String, password: String): (user: User)`\
&nbsp;&nbsp;&nbsp;&nbsp; **requires** username to exist\
&nbsp;&nbsp;&nbsp;&nbsp; **effect** return that user\
<span style="color:white"><span>
3. What essential invariant must hold on the state? How is it preserved?
- An essential invariant that must hold in this state is that each username in `Users` is unique. It is preserved by the precondition on the `register` action--only create the new user if the username doesn't currently exist.
4. One widely used extension of this concept requires that registration be confirmed by email. Extend the concept to include this functionality.\
**concept** PasswordAuthenticationWithEmailConfirmation \
**purpose** limit access to known users \
**principle** after a use registers with a username and password, they can authenticate with that same username and password and can be treated each time as the same user \
**state**\
&nbsp;&nbsp;a set of `Users` with \
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: white">    a username String<span>\
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: white">    an isConfirmed Flag<span>\
**actions**\
&nbsp;&nbsp;`register(username: String, password: String): (user: User, token: Token)`\
&nbsp;&nbsp;&nbsp;&nbsp; **requires** username does not exist\
&nbsp;&nbsp;&nbsp;&nbsp; **effect** create and return newly created user, add user to Users\
&nbsp;&nbsp;`confirm(username: String, token: Token)`\
&nbsp;&nbsp;&nbsp;&nbsp; **requires** user's registration is not already confirmed\
&nbsp;&nbsp;&nbsp;&nbsp; **effect** confirms the user's registration\
&nbsp;&nbsp;`authenticate (username: String, password: String): (user: User)`\
&nbsp;&nbsp;&nbsp;&nbsp; **requires** username to exist, user's registration is confirmed\
&nbsp;&nbsp;&nbsp;&nbsp; **effect** return that user

## Exercise 3: Comparing Concepts
**concept** PersonalAccessToken\
**purpose** provide an authentication method that is more manageable and configurable\
**principle** a user generates a token, then the token can then be used by the user for authentication\
**state**\
&nbsp;&nbsp; a set of `Users` with\
&nbsp;&nbsp;&nbsp;&nbsp; a username String\
&nbsp;&nbsp;&nbsp;&nbsp; a password String\
&nbsp;&nbsp;&nbsp;&nbsp; a set of `Tokens`\
&nbsp;&nbsp; a set of `Tokens` with\
&nbsp;&nbsp;&nbsp;&nbsp; a token String\
&nbsp;&nbsp;&nbsp;&nbsp; an active Flag\
&nbsp;&nbsp;&nbsp;&nbsp; an expiration Date\
**actions**\
&nbsp;&nbsp; `createToken(user: User): (token: Token)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** user exists\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** generates a new random token string, add to user's tokens, returns the token string\
&nbsp;&nbsp;`deactivateToken(user: User, token: Token)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** token to belong to user\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** makes token inactive\
&nbsp;&nbsp;`authenticateWithToken(username: String, token: Token): (user: User)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** user exists, token is active and belongs to user\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** return that user

In general, GitHub should avoid using language about the similarities of passwords and access tokens (e.g. "treat your personal access tokens like passwords"). To drive home the difference in concepts, they should focus on language that highlights the ***differences*** between the concepts. I think the page would also benefit from a table directly comparing passwords and access tokens. This could help the user clearly differentiate between the two and identify any tradeoffs.

## Exercise 4: Defining Familiar Concepts
### URL Shortener
**concept** URLShortener\
**purpose** Provide short links that redirect to longer URLs \
**principle** A user submits a URL to be shortened, a shorter URL alias is created, when the shortened URL is navigated to, the user gets redirected to the original URL \
**state** \
&nbsp;&nbsp; a set of `Mappings` with \
&nbsp;&nbsp;&nbsp;&nbsp; a `URL` String \
&nbsp;&nbsp;&nbsp;&nbsp; a `shortURL` String \
&nbsp;&nbsp;&nbsp;&nbsp; an `active` Flag \
**actions**\
&nbsp;&nbsp;`shorten(url: String): (shortURL: String)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** `url` is a valid URL\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** makes a mapping with the url and the generated shortened url (NOTE: the shortened url is unique)\
&nbsp;&nbsp;`redirect(shortURL: String): (url: String)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** short url to correspond to an active mapping \
&nbsp;&nbsp;&nbsp;&nbsp;**effect** return the url for that short url \
&nbsp;&nbsp;`deactivate(mapping: Mapping)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** mapping to exist, mapping is active\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** marks mapping as inactive\
&nbsp;&nbsp;`activate(mapping: Mapping)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** mapping to exist, mapping is not active\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** marks mapping as active\
&nbsp;&nbsp;`delete(mapping: Mapping)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** mapping exists, mapping is inactive
&nbsp;&nbsp;&nbsp;&nbsp;**effect** removes mapping



### Billable Hours Tracking
**concept** BillableHoursTracking\
**purpose** Keep track of work sessions for employees on projects so that billable hours can be calculated correctly\
**principle** An employee starts a session by choosing a project and gives a description of the work, the system records the start time and keeps the session open, the system records the end time when the employee ends the session. If a session is left open unintentionally, the system will close the session. Finally, billable hours are calculated\
**state**\
&nbsp;&nbsp; a set of `Sessions` with\
&nbsp;&nbsp;&nbsp;&nbsp; an `Employee`\
&nbsp;&nbsp;&nbsp;&nbsp; a `Project`\
&nbsp;&nbsp;&nbsp;&nbsp; a `description` String\
&nbsp;&nbsp;&nbsp;&nbsp; a `startTime` Number\
&nbsp;&nbsp;&nbsp;&nbsp; an `endTime` Number\
&nbsp;&nbsp;&nbsp;&nbsp; a `isOpen` Flag\
**actions**\
&nbsp;&nbsp;`startSession(employee: Employee, project: Project, description: String): (session: Session)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** employee, project to exist, employee has no other open session\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** create and return new, open session with current time as `startTime`\
&nbsp;&nbsp;`endSession(session: Session)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** session exists, session open\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** set `endTime` to current time, set session as closed\
&nbsp;&nbsp;`autoClose(session: Session, cutoff: Number)`
&nbsp;&nbsp;&nbsp;&nbsp;**requires** session exists, session open, `curr_time-start_time>cutoff`\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** set `endTime` to `startTime+cutoff`, set session as closed\
&nbsp;&nbsp;`modifySession(session: Session, description?: String, startTime?: Number, endTime?: Number)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** session is inactive\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** modifies some amount of information about the session\
&nbsp;&nbsp;`getHours(project: Project): (hours: Number)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** project exists\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** returns sum of durations of closed sessions for the project\


### Conference Room Booking
**concept** ConferenceRoomBooking\
**purpose** Allow users to reserve conference rooms for meetings, prevents overlapping reservations\
**principle** A user selects a room, start time, and end time, the system creates a booking if the room is available, users may later cancel their bookings, and the system maintains a record of both active and canceled bookings\
**state**\
&nbsp;&nbsp;a set of `Rooms` with\
&nbsp;&nbsp;&nbsp;&nbsp;an `id` String\
&nbsp;&nbsp;&nbsp;&nbsp;a `capacity` Number\
&nbsp;&nbsp;&nbsp;&nbsp;a `location` String\
&nbsp;&nbsp;a set of `Bookings` with\
&nbsp;&nbsp;&nbsp;&nbsp;a `Room`\
&nbsp;&nbsp;&nbsp;&nbsp;a `User`\
&nbsp;&nbsp;&nbsp;&nbsp;an `attendees` Number\
&nbsp;&nbsp;&nbsp;&nbsp;a `startTime` Number\
&nbsp;&nbsp;&nbsp;&nbsp;an `endTime` Number\
&nbsp;&nbsp;&nbsp;&nbsp;an `isActive` Flag\
**actions**\
&nbsp;&nbsp;`bookRoom(user: User, room: Room, attendees: Number, startTime: Number, endTime: Number): (booking: Booking)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** room exists, `startTime < endTime`, `attendees < capacity`, no active booking overlaps this interval for the room \
&nbsp;&nbsp;&nbsp;&nbsp;**effect** create new booking with status active, return it\
&nbsp;&nbsp;`cancelBooking(booking: Booking)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** booking exists, booking active\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** set booking status to canceled\
&nbsp;&nbsp;`listBookings(room: Room): (bookings: Set of Booking)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** room exists\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** return all bookings for the room (active and canceled)\
