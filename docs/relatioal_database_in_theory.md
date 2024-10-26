# Relational database principles

### Key Concepts and objectives

> [!NOTE]
>
> Concepts and objectives are to explained in Excel. Database diagrams will be introduced later. 

1. **Tables (Relations)**: The primary structure of a relational database, where data is organized in rows and columns. Each table represents an entity (e.g., customers, orders).
2. **Rows (Records/Tuples)**: Each row in a table represents a single instance of the entity and contains data corresponding to the table's attributes.
3. **Columns (Attributes/Fields)**: Each column in a table defines a specific attribute of the entity. For example, in a customer table, columns might include `CustomerID`, `Name`, and `Email`.
4. **Primary Key**: A unique identifier for each record in a table. It ensures that no two rows have the same value in the primary key column(s).
5. **Foreign Key**: A field (or collection of fields) in one table that uniquely identifies a row of another table. It establishes a relationship between the two tables.
6. **Relationships**:
   - **One-to-One**: Each record in one table is related to one record in another table.
   - **One-to-Many**: A single record in one table can be associated with multiple records in another table.
   - **Many-to-Many**: Records in one table can relate to multiple records in another table and vice versa, often implemented using a junction table.



## Example #1: The new social network

Here’s a database design for a simple social network where members can indicate each other as friends. The design will include tables for members and their friendships, along with some sample data.

### Database Design

#### Entities

1. **Member**: Represents users in the social network.
2. **Friendship**: Represents the friendship relationships between members.

### Tables with Sample Data

#### **Member Table**

| MemberID | FullName    | Email             | JoinDate   |
| -------- | ----------- | ----------------- | ---------- |
| 1        | Alice Smith | alice@example.com | 2020-01-15 |
| 2        | Bob Johnson | bob@example.com   | 2021-05-22 |
| 3        | Carol White | carol@example.com | 2019-11-30 |
| 4        | David Brown | david@example.com | 2022-03-10 |
| 5        | Emma Green  | emma@example.com  | 2023-02-14 |

#### **Friendship Table**

| FriendshipID | MemberID1 | MemberID2 | Status   | Since      |
| ------------ | --------- | --------- | -------- | ---------- |
| 1            | 1         | 2         | Accepted | 2020-06-01 |
| 2            | 1         | 3         | Accepted | 2021-07-15 |
| 3            | 2         | 3         | Pending  | 2024-10-01 |
| 4            | 4         | 5         | Accepted | 2023-03-05 |
| 5            | 2         | 4         | Rejected | 2022-05-22 |

### Explanation of Sample Data

- **Members**:
  - Five members are represented in the `Member` table, each with a unique `MemberID`, full name, email, and the date they joined the network.
- **Friendships**:
  - The `Friendship` table captures friendships between members.
  - Each friendship has a unique `FriendshipID` and includes `MemberID1` and `MemberID2` to represent the two members involved in the friendship.
  - The `Status` column indicates the status of the friendship, which can be "Accepted," "Pending," or "Rejected."
  - The `Since` column shows the date when the friendship was established or requested.

### Relationships

- **One-to-Many**: Each member can have multiple friendships.
- **Many-to-Many**: Since friendships are bi-directional, both `MemberID1` and `MemberID2` reference the same `Member` table, allowing any member to be friends with another.

This design allows for a basic social networking functionality, where members can connect as friends and the system can track the status of these connections. You can expand this model further by adding features like messaging, user posts, or friend requests.



## Example #2: **Library Management System**

**Task**: Design a database to manage a library’s collection of books, authors, and members. The system should track which books are borrowed by which members, and when they are due for return.

- **Entities**: Book, Author, Member, Borrow
- **Key Concepts**: One-to-many relationship between Author and Book, Many-to-many relationship between Book and Member (borrowed books), primary and foreign keys, handling dates for borrow/return.

### Tables with Sample Data

#### **Author Table**

| <u>AuthorID</u> 🔑 | Name               | BirthDate  |
| ----------------- | ------------------ | ---------- |
| 1                 | J.K. Rowling       | 1965-07-31 |
| 2                 | George R.R. Martin | 1948-09-20 |
| 3                 | Jane Austen        | 1775-12-16 |
| 4                 | Mark Twain         | 1835-11-30 |

#### **Book Table**

| <u>BookID</u> 🔑 | Title                                   | AuthorID | PublishedYear |
| --------------- | --------------------------------------- | -------- | ------------- |
| 1               | Harry Potter and the Sorcerer's Stone   | 1        | 1997          |
| 2               | A Game of Thrones                       | 2        | 1996          |
| 3               | Pride and Prejudice                     | 3        | 1813          |
| 4               | The Adventures of Tom Sawyer            | 4        | 1876          |
| 5               | Harry Potter and the Chamber of Secrets | 1        | 1998          |

#### **Member Table**

| <u>MemberID 🔑</u> | FullName    | MembershipDate |
| ----------------- | ----------- | -------------- |
| 1                 | Alice Smith | 2020-01-15     |
| 2                 | Bob Johnson | 2021-05-22     |
| 3                 | Carol White | 2019-11-30     |
| 4                 | David Brown | 2022-03-10     |

#### <u>**Borrow Table**</u>

| <u>BorrowID</u> 🔑 | BookID | MemberID | BorrowDate | DueDate    | ReturnDate |
| ----------------- | ------ | -------- | ---------- | ---------- | ---------- |
| 1                 | 1      | 1        | 2024-10-01 | 2024-10-15 | NULL       |
| 2                 | 2      | 2        | 2024-10-05 | 2024-10-19 | NULL       |
| 3                 | 3      | 3        | 2024-10-10 | 2024-10-24 | 2024-10-20 |
| 4                 | 4      | 4        | 2024-10-12 | 2024-10-26 | NULL       |
| 5                 | 5      | 1        | 2024-10-15 | 2024-10-29 | NULL       |

### Explanation of Sample Data

- **Authors**:
  - Four authors are listed, each with a unique `AuthorID`, name, and birth date.
- **Books**:
  - There are five books associated with the authors. Each book has a unique `BookID`, a title, the `AuthorID` of the author who wrote it, and the year it was published.
- **Members**:
  - Four members are registered in the library. Each member has a unique `MemberID`, full name, and membership date.
- **Borrows**:
  - The `Borrow` table keeps track of which member borrowed which book, along with dates.
  - The `ReturnDate` for books that have been returned is recorded, while `NULL` indicates books that are still borrowed.

This design and the corresponding sample data provide a comprehensive view of how the library database can effectively manage its collections and member activities. You can expand this model by adding more details, such as book genres or member contact information, as needed.

## Example #3: Organizational Hierarchy Database Design

**Task**: Create a single-table database in which a company's organizational hierarchy can be represented! Enhance the database with a table containing employees, where each employee is a member of an organizational unit. 

Expand the database so that each organizational unit must have a leader who is an employee.

``` mermaid
graph TD;
    A[Company] --> B[Sales Department]
    A --> C[Engineering Department]
    A --> D[HR Department]
    
    %% Subdepartments
    B --> E[Domestic Sales]
    B --> F[International Sales]
    
    C --> G[Software Development]
    C --> H[Quality Assurance]
    
    D --> I[Recruitment]
    D --> J[Employee Relations]
    

```