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

No transitive dependencies allowed. nonkey attributes can fully depend on each other.

Does CustomerFirstName, CustomerPhone, depend on another non-key attribute? yes they depend on customer ID. So I will take those out of there.

ReservationID(PK),EventID(FK), StaffID(FK), Date, PartySize, Special Accommodations,CustomerID(FK)

CustomerID(PK), CustomerFirstName,CustomerLastName, CustomerPhone, CustomerEmail

EventID(PK), EventDescription

StaffId(PK), StaffFirstName, StaffLastName

Everything here has cardinality to the reservation table.
Customer to reservation = a reservation must have a customer, but a customer can have zero one or many reservations.

Event to reservation = a reservation can have one and only one event, but an event can appear on zero one or many reservations

Staff to reservation = a reservation can have one and only one staff, but a staff can work on zero one or many reservation instances.

## Staff Training Status

Staff Training Status View

Ok so we need to keep in mind the purpose of this record. To record staff training status efficiently.

### Initial Table (attribute list only)

Candidate primary key will be StaffID. So we can search their training status using ID.

StaffId, (Name, StaffTypeId, StaffTypeDescription, Wage), TrainingId, CompletionDate, (TrainingStatusId, Description), Cost

So again I made a table in this form to help me identify repeating groups. I think I have found them above. So take them out, designate primary key and flag it as a foreign key in the new table.

  

We have three description attributes.

1. StaffTypeDescription(Server, Cook etc),
2. TrainingStatusDescription(Completed, registered ,etc)

**But it seems like TrainingDescripton eg. ProServe is NOT in the template.** and I only just noticed as I was going to 3NF. So will pop it in there because it's a transitive dependency anyway.

![1706802445907](image/Lab1Again/1706802445907.png)

### 1NF

StaffID(PK),TrainingStatusID(FK), TrainingID,Training Description, CompletionDate,Cost

StaffID(FK PK), Staff F.Name, Staff L.Name, StaffTypeID, StaffTypeDescription, Wage

TrainingStatusID(PK), TrainingStatusDescription

### 2NF

So, we are in 2NF above because we dont have any partial dependencies. TrainingID depends on StaffID of the specific staff taking that training, completion date depends on the if the staffID completed that training. However Cost depends on the trainingID but that is a transitive dependency. Same goes for StaffTypeID and StaffTypeDescription I think those are transitive dpendencies as well.

StaffID(PK FK),TrainingStatusID(FK), TrainingID, TrainingDescription, CompletionDate,Cost

StaffID(PK), Staff F.Name, Staff L.Name, StaffTypeID, StaffTypeDescription, Wage

TrainingStatusID(PK), TrainingStatusDescription

### 3NF

So we have a transitive dependency here in the top table. Training Description depends on trainingID same with Cost 

In the second table we have a transitive dependency between StaffTypeID and StaffTypeDescription including wage.

Staff Training
StaffID(PK FK),TrainingStatusID(FK), TrainingID(FK), CompletionDate,

Training
TrainingID(PK), TrainingDescription, Cost

StaffTypeInfo
StaffTypeID(PK), StaffTypeDescription, Wage

StaffPersonelInfo
StaffID(PK), Staff F.Name, Staff L.Name,StaffTypeID(Fk)


## Bills View

### Initial Table (attribute list only)

**There is no special requests attribute in the template.** 

Candidate keys, BillID + ReservationID composite key OR just ReservationID. Well since we can have many bills on one reservation I think a composite key would be a btter way of keeping track of what was ordered on what bill for which reservation rather than bill number alne or reservation id alone.

BillId(PK), ReservationId(PK), Date, (MenuItemId, ItemName, Description,Price, ExtendedPrice,SpecialRequests, Quantity,) Subtotal, GST, Tips, Total

### 1NF

BillId(PK), ReservationId(PK), Date, MenuItemID(FK), Subtotal, GST, Tips, Total

MenuItemId(PK), ItemName, Description,Price, ExtendedPrice,SpecialRequests, Quantity



### 2NF 

No partial dependencies, since we have a compisite key we can potentially have a violation. 
1. Date depends on entire primary key eg date of this reservation and bill
2. Special requests depends on entire key? eg special request for items on this bill for this reservation
but i think special request would fit better in a MenuBillItem Table.
3. Quantitiy depends on entire primary key
4. this one is tough but i think we are in 2NF

BillId(PK), ReservationId(PK), Date, MenuItemID(FK), Subtotal, GST, Tips, Total

MenuItemId(PK), ItemName, Description,Price, ExtendedPrice,SpecialRequests, Quantity

