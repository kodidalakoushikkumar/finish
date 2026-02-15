# 1️⃣ Types of Databases

| Database Type      | Structure               | Best Use Case                         | Examples          |
| ------------------ | ----------------------- | ------------------------------------- | ----------------- |
| Relational (RDBMS) | Tables (rows & columns) | Banking, ERP, users, transactions     | MySQL, PostgreSQL |
| Document           | JSON documents          | APIs, flexible apps, product catalogs | MongoDB           |
| Key-Value          | key → value             | Cache, sessions, OTP, tokens          | Redis             |
| Column Family      | Distributed columns     | Big data, analytics, logs             | Apache Cassandra  |
| Graph              | Nodes & relationships   | Social network, recommendations       | Neo4j             |

# 2️⃣ Query Languages

|Language Type|Used For|Syntax Style|Example DB|
|---|---|---|---|
|SQL|Relational DB|Structured English-like|MySQL|
|JSON Query|Document DB|JavaScript-like|MongoDB|
|Key Commands|Key-Value DB|Simple commands|Redis|
|CQL|Column DB|SQL-like distributed|Apache Cassandra|
|Cypher|Graph DB|Relationship query|Neo4j|

# 3️⃣ SQL Query Categories

|Category|Purpose|Commands|
|---|---|---|
|DDL|Define structure|CREATE, ALTER, DROP|
|DML|Modify data|INSERT, UPDATE, DELETE|
|DQL|Read data|SELECT|
|DCL|Permissions|GRANT, REVOKE|
|TCL|Transactions|COMMIT, ROLLBACK, SAVEPOINT|

# 4️⃣ Real Company Usage (How systems actually run)

| System Part          | Database Used    | Why                   |
| -------------------- | ---------------- | --------------------- |
| User accounts        | MySQL            | structured + reliable |
| Login sessions       | Redis            | ultra fast            |
| Product catalog      | MongoDB          | flexible fields       |
| Logs / analytics     | Apache Cassandra | massive scale         |
| Friend relationships | Neo4j            | relationship queries  |