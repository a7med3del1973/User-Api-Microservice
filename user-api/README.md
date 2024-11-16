# User-Api
The User API manages admin users, allowing for adding, activating, and deactivating them. It also provides functionality to view a list of all users.

## Entity Relationship Diagram (ERD)

The database schema for the `user-api` consists of two main tables: `USER` and `TRANSACTION`. These tables are structured to manage admin users and their related transactions.


```mermaid
erDiagram
    USER {
        int id PK "Auto Increment, Primary Key"
        varchar username "Unique, not null"
        varchar email "Unique, not null"
        varchar password_hash "Hashed password, not null"
        varchar full_name "Not null"
        enum role "ENUM('admin', 'superadmin')"
        enum status "ENUM('active', 'inactive', 'deactivated')"
        timestamp created_at "Default: CURRENT_TIMESTAMP"
        timestamp updated_at "Default: CURRENT_TIMESTAMP ON UPDATE"
    }
    
    TRANSACTION {
        int id PK "Auto Increment, Primary Key"
        int user_id FK "Foreign Key to USER"
        decimal amount "Transaction amount"
        text notes "Transaction notes"
        timestamp created_at "Default: CURRENT_TIMESTAMP"
    }
    
    USER ||--o{ TRANSACTION : "has many"
