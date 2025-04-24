# 🏋️ Gym Management System – Entity Relationship Model

## 📘 Scenario

You visit a well-known gym chain and discover they are still using physical cards to manage client sessions. After witnessing a registration error, the owner shares that:

- He owns **multiple gymnasiums**, each with a name, address, and phone number.
- **Members** register at one gym and must provide:
  - ID, last name, first name, address, date of birth, and gender.
- Each **session**:
  - Has a sport type, a schedule, and a **maximum of 20 members**.
- Each session is **led by up to 2 coaches**, who have:
  - Last name, first name, age, and specialty.

In exchange for a 3-month free membership, you propose a digital system based on an Entity-Relationship Model.

---

## 🧩 Entities and Attributes

### 🏢 Gymnasium
- `GymID` (Primary Key)
- `Name`
- `Address`
- `PhoneNumber`

### 🧍 Member
- `MemberID` (Primary Key)
- `LastName`
- `FirstName`
- `Address`
- `DateOfBirth`
- `Gender`
- `GymID` (Foreign Key → Gymnasium)

### 🧘 Session
- `SessionID` (Primary Key)
- `SportType`
- `Schedule`
- `MaxCapacity` (default = 20)

### 🧑‍🏫 Coach
- `CoachID` (Primary Key)
- `LastName`
- `FirstName`
- `Age`
- `Specialty`

---

## 🔗 Relationships

### 1. Member ↔ Session
- **Many-to-Many** (via `MemberSession`)
- A member can register for several sessions.
- Each session can hold up to 20 members.

**Table: `MemberSession`**
- `MemberID` (FK)
- `SessionID` (FK)

---

### 2. Coach ↔ Session
- **Many-to-Many** (via `CoachSession`)
- A session can have up to 2 coaches.
- A coach can lead multiple sessions.

**Table: `CoachSession`**
- `CoachID` (FK)
- `SessionID` (FK)

---

## 🧠 Conceptual ER Diagram (Textual View)

## 🧠 Conceptual ER Diagram (Textual View)

Entities and Relationships:

1. Gymnasium
   ├── GymID (PK)
   ├── Name
   ├── Address
   ├── PhoneNumber
   └── has many → Members

2. Member
   ├── MemberID (PK)
   ├── LastName
   ├── FirstName
   ├── Address
   ├── DateOfBirth
   ├── Gender
   ├── GymID (FK)
   └── registers for → Sessions (via MemberSession)

3. Session
   ├── SessionID (PK)
   ├── SportType
   ├── Schedule
   ├── MaxCapacity
   ├── has many → Members (via MemberSession)
   └── is led by → Coaches (via CoachSession)

4. Coach
   ├── CoachID (PK)
   ├── LastName
   ├── FirstName
   ├── Age
   └── Specialty
        └── leads → Sessions (via CoachSession)

5. MemberSession (junction table)
   ├── MemberID (FK)
   └── SessionID (FK)

6. CoachSession (junction table)
   ├── CoachID (FK)
   └── SessionID (FK)


---

## 📌 Notes
- The system is designed to **avoid overbooking** and **ensure accurate registration tracking**.
- It’s fully scalable and can support **multiple gym branches** and **dynamic session scheduling**.

---
