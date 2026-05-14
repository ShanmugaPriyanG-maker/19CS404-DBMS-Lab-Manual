# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1024" height="395" alt="S1" src="https://github.com/user-attachments/assets/9149d9e6-c37d-4b20-9586-5970487b305c" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|     Member   |     member_id (PK), name, membership_type, start_date               |    Gym member details   |
|   Program     |          program_id (PK), program_name, schedule          |   Yoga, Zumba, etc.    |
|   Trainer     |     trainer_id (PK), name, specialization               |    Trainers can handle multiple programs   |
|  Session      |           session_id (PK), session_date, time, member_id (FK), trainer_id (FK)         |   Personal training    |
|     Attendance   |           attendance_id (PK), session_id (FK), member_id (FK), status         |   Present/Absent    |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|     Relationship         |      M:N      |        Partial       |    Member can join many programs   |
|      Program–Trainer (Assigned)        |     M:N       |         Total      |  Program must have trainers     |
|     Member–Session (Books)         |       1:M     |         Partial      |    Optional personal sessions   |

### Assumptions
- A member can exist without joining programs initially.
- Payments can be for membership or sessions.
- Trainers must be assigned to at least one program.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="1024" height="434" alt="S2" src="https://github.com/user-attachments/assets/6ee984df-aadb-410d-b598-2185cae11e75" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|    Member    |       member_id (PK), name, contact             |    Library member   |
|    Book    |            book_id (PK), title, author, category_id (FK)        |   Each copy tracked    |
|    Category    |          category_id (PK), category_name          |    Fiction, Science, etc.   |
|   Loan     |          loan_id (PK), book_id (FK), member_id (FK), loan_date, return_date          |    Borrowing record   |
|    Event    |          event_id (PK), event_name, event_date, room_id (FK)          |   Cultural events    |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|       Member–Book (Borrow)       |       M:N     |       Partial        |    Via Loan entity   |
|       Book–Category       |          M:1  |        Total       |    Each book must have categoryEach book must have category   |
|        Member–Event (Register)      |        M:N    |       Partial        |     Optional events  |

### Assumptions
- A book can be borrowed multiple times but by one member at a time.
- Rooms cannot host two events at same time.
- Fines apply only after due date.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="1024" height="690" alt="S3" src="https://github.com/user-attachments/assets/caa24c2a-727f-47c9-a04c-8a086d692293" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|    Customer    |          customer_id (PK), name, phone          |   Walk-in or reserved    |
|   Reservation     |              reservation_id (PK), date, time, guests, customer_id (FK), waiter_id (FK)      |    Table booking   |
|     Waiter   |          waiter_id (PK), name, shift          |    Staff   |
|    Order    |         order_id (PK), reservation_id (FK), order_time           |  Multiple per reservation     |
|    Dish    |        dish_id (PK), dish_name, price, category_id (FK)            |  Menu item     |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|        Customer–Reservation      |       1:M     |     Partial          |   Walk-ins allowed    |
|         Reservation–Waiter     |      M:1      |       Total        |  Must be served     |
|      Reservation–Order        |    1:M        |        Total       |   Orders belong to reservation    |

### Assumptions
- Walk-in customers are stored as reservations without prior booking.
- A waiter can handle multiple reservations per shift.
- Bill is generated after all orders are completed.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
