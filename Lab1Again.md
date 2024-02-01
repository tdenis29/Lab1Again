# Lab 1 Tyson Denis DMIT-1508 A02

Hey Don, Tyson Denis here. I worked on the lab on Friday the 26th and Tuesday 30th, but then I did the practice labs JoesVideos and Memories forever and realized I wssn't following the normalization rules. For example, in my first lab I removed the customer info from the intital table because I recognized the pattern. I'm not sure if thats what you are asking for so I started it again. I will try to follow the normalization rules exactly and I will document my thought process just as in my first attempt.

## Reservation View

### Initial Table (attribute list only)

ReservationId, Date, PartySize, (EventId, EventDescription), SpecialAccomodations, (StaffId, Name), CustomerId, Name, Phone, Email

So, in order to visualize potential repeating groups I made a couple dummy entries into the table in this form.

![1706744123604](image/Lab1Again/1706744123604.png).

I have identified EventId and EventDescription as a repeating group and StaffId and StaffName as a repeating group. So I will copy the repeating groups to a new table and mark keys and do the cardinality.

### 1NF

All attributes atomic and no repeating groups.

ReservationID(PK),EventID(FK), StaffID(FK), Date, PartySize, Special Accommodations, CustomerID, CustomerFirstName,CustomerLastName, CustomerPhone, CustomerEmail

EventID(PK), EventDescription

StaffId(PK), StaffFirstName, StaffLastName

### 2NF

No partial dependency allowed. We do not have a composite key in these tables but I can see customer information sticking out. But because customer ID is not a key I'll leave it there until 3NF

ReservationID(PK),EventID(FK), StaffID(FK), Date, PartySize, Special Accommodations, CustomerID, CustomerFirstName,CustomerLastName, CustomerPhone, CustomerEmail

EventID(PK), EventDescription

StaffId(PK), StaffFirstName, StaffLastName




### 3NF
