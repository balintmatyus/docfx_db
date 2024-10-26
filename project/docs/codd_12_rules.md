# Codd's 12 rules

Edgar F. Codd proposed 12 rules to define what qualifies a system as a truly relational database management system (RDBMS). Here are Codd's 12 rules:

1. **Information Rule**
   All information in a database must be represented in one and only one way, as values within tables.
2. **Guaranteed Access Rule**
   Every data element (value) is accessible by using a combination of table name, primary key (or unique identifier), and column name.
3. **Systematic Treatment of Null Values**
   Null values (representing missing or inapplicable information) must be uniformly supported in databases and should be independent of data types.
4. **Dynamic Online Catalog Based on the Relational Model**
   The metadata (data dictionary or catalog) must be stored in the form of tables, accessible through standard relational database operations.
5. **Comprehensive Data Sublanguage Rule**
   A database must support at least one language that allows users to define, manipulate, and query data, with operations like SELECT, INSERT, UPDATE, and DELETE, along with transaction control.
6. **View Updating Rule**
   All views (virtual tables derived from base tables) should theoretically be updatable, reflecting the changes in underlying base tables.
7. **High-Level Insert, Update, and Delete**
   A database must support set-based operations, allowing users to retrieve, insert, update, or delete data in sets (rows), not just single rows.
8. **Physical Data Independence**
   Changes to the physical storage of data should not affect the applications accessing it, making the database independent of hardware and storage methods.
9. **Logical Data Independence**
   Changes to logical database structures (like tables) should not impact the applications accessing them, ensuring flexibility.
10. **Integrity Independence**
    Database integrity constraints, such as primary keys and foreign keys, must be stored in the catalog and enforceable within the RDBMS.
11. **Distribution Independence**
    The distribution of data across locations should be transparent, meaning that users should not be aware of data being distributed across multiple locations.
12. **Non-Subversion Rule**
    If a database supports low-level access (like direct access), it should not be able to bypass the integrity rules and constraints enforced by the RDBMS.

These rules outline what a relational database should support, though very few modern RDBMS systems strictly conform to all of Codd’s rules.