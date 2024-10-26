## Key concepts and objectives

1. **Constraints**: Rules applied to data to ensure integrity and validity. Common types include:
   - **Unique Constraints**: Ensures all values in a column are distinct.
   - **Not Null Constraints**: Ensures a column cannot have null values.
   - **Check Constraints**: Validates that values in a column meet specified conditions.
2. **Indexes**: Data structures that improve the speed of data retrieval operations on a database table at the cost of additional space and maintenance overhead.
3. **Views**: Virtual tables that represent a subset of the data from one or more tables, allowing users to access data without modifying the underlying tables.

Additional Terms

- **Schema**: The blueprint of the database, defining the structure, including tables, fields, data types, and relationships.
- **Data Type**: Defines the kind of data that can be stored in a column (e.g., integer, varchar, date).
- **Transaction**: A sequence of operations performed as a single logical unit of work. Transactions follow the ACID properties (Atomicity, Consistency, Isolation, Durability).
- **Stored Procedure**: A precompiled collection of SQL statements that can be executed as a single unit, improving performance and reusability.

Understanding these concepts is crucial for effective relational database design and implementation, ensuring that the database is efficient, scalable, and maintainable.

## Activities

### Work with SSMS

Build the "Simple e-commerce DB" with the guidance of the instructor. Set data types, foreign key constraints, etc. 

Generate sample data using ChatGPT, and fill products and customers table - sample data is a MUST for testing and demonstration!

Set *Not Null Constraints* and *Check Constraints* where necessary.

### "7 minutes 7 randoms" dating club

Students can ask the lecturer on the details of the task and create a Mermaid diagram that can be converted to SQL script using ChatGPT. 

The "7 Minutes 7 Randoms" dating service organizes dating events. Members of the club can apply for events. Each event hosts 14 participants: 7 boys and 7 girls. Each girl sits at a table, and each boy has a chance to talk to each girl for 7 minutes. At the end of the event, participants can give "hearts" to the ones they like. In case of mutual sympathy, organizers hand out contacts. The system ensures that those who have already met do not attend the same event again.

``` mermaid
erDiagram
    MEMBER {
        int id PK "Primary key"
        string name
        string email
        string gender
    }

    EVENT {
        int id PK "Primary key"
        string date
        string location
        string status
    }

    PARTICIPANT {
        int id PK "Primary key"
        int memberId FK "Foreign key to Member"
        int eventId FK "Foreign key to Event"
    }

    HEART {
        int id PK "Primary key"
        int giverId FK "Foreign key to Member (giver)"
        int receiverId FK "Foreign key to Member (receiver)"
        int eventId FK "Foreign key to Event"
    }

    MEMBER ||--o{ PARTICIPANT : "attends"
    EVENT ||--o{ PARTICIPANT : "includes"
    MEMBER ||--o{ HEART : "gives"
    MEMBER ||--o{ HEART : "receives"
    EVENT ||--o{ HEART : "related to"

```



Lessons to learn:

① The number 7 does NOT appear in the database

② There is no way to set check constraints do the number of participants to an event. It has to be solved using a Stored Procedure or some background logic.

③ Mermaid diagram can be converted to SQL - and vice verse. 









