# Database

**Relational DBMS**: Oracle, MySQL, SQLite

**Key-value Stores**: Redis, Memcached

**Document stores**: MongoDB

**Graph**: Neo4j

**Wide column stores**: Cassandra, HBase

### Design and Modeling (a.k.a Data Definition)

#### 1\.1 Schema

A database schema of a database system is its structure described in a formal language supported by the database management system (DBMS) and refers to the organization of data as a blueprint of how a database is constructed (divided into database tables in the case of Relational Databases). The formal definition of database schema is a set of formulas (sentences) called integrity constraints imposed on a database. These integrity constraints ensure compatibility between parts of the schema. All constraints are expressible in the same language. A database can be considered a structure in realization of the database language. The states of a created conceptual schema are transformed into an explicit mapping, the database schema. This describes how real world entities are modeled in the database.

#### 1\.1.1 Type

In computer science and computer programming, a data type or simply type is a classification identifying one of various types of data, such as real, integer or Boolean, that determines the possible values for that type; the operations that can be done on values of that type; the meaning of the data; and the way values of that type can be stored.

`TEXT`, `INT`, `ENUM`, `TIMESTAMP`

#### 1.2 Cardinality (a.k.a Relationship)

`Foreign key`, `Primary key`

#### 1\.2 Indexing

A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space to maintain the index data structure. Indexes are used to quickly locate data without having to search every row in a database table every time a database table is accessed. Indexes can be created using one or more columns of a database table, providing the basis for both rapid random lookups and efficient access of ordered records. Why Indexing is important?

`Indexing in MySQL`

```sql
CREATE INDEX NameIndex ON Employee (name)
SELECT * FROM Employee WHERE name = 'Ashish'
```

### 2. Data Manipulation

#### Create - Read - Update - Delete

*   Create or add new entries
*   Read, retrieve, search, or view existing entries * Update or edit existing entries * Delete/deactivate existing entries

```sql
/* create */
CREATE TABLE Guests ( id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY, firstname VARCHAR(30) NOT NULL, lastname VARCHAR(30) NOT NULL, email VARCHAR(50), reg_date TIMESTAMP )
/* create (insert) */
INSERT INTO Guests (firstname, lastname, email) VALUES ('John', 'Doe', 'john@example.com')
/* read */
SELECT * FROM Guests WHERE id=1 /* update */ UPDATE Guests SET lastname='Doe' WHERE id=1
/* delete */
DELETE FROM Guests WHERE id=1`
```

### 3. Data Retrieve & Transaction

#### 3.1 Data Retrieve

`SELECT`, `WHERE`, `FROM`, `LIMIT`, `JOIN`, `GROUP BY`, `HAVING`

Get user id, user name and number of post of this user

```sql
SELECT user.id, user.name, COUNT(post.*) AS posts
FROM user LEFT OUTER JOIN post ON post.owner_id=user.id GROUP BY user.id`
```

Select user who only order one time.

```sql
SELECT name, COUNT(name) AS c FROM orders GROUP BY name HAVING c = 1;
```

Calculate the longest period (in days) that the company has gone without a hiring or firing anyone.

```sql
SELECT x.date, MIN(y.date) y_date, DATEDIFF(MIN(y.date),x.date) days
FROM ( SELECT hiredate date FROM employees UNION SELECT terminationdate FROM employees ) x
JOIN ( SELECT hiredate date FROM employees UNION SELECT terminationdate FROM employees UNION SELECT CURDATE()) y
ON y.date > x.date GROUP BY x.date ORDER BY days DESC LIMIT 1;
```

**Data Retrieve API**

<table>
<tbody>
<tr>
<td>API</td>
<td>Description</td>
</tr>
<tr>
<td>get</td>
<td>get single item</td>
</tr>
<tr>
<td colspan="2">
<p>Get dog by id</p>
<pre>Dog.get(1)</pre>
</td>
</tr>
<tr>
<td>find</td>
<td>
<p>find items</p>
<p>@see&nbsp;<a href="https://docs.mongodb.com/manual/reference/method/db.collection.find/">collection.find()</a></p>
</td>
</tr>
<tr>
<td colspan="2">&nbsp;&nbsp;
<p>Find dog name "Max"</p>
<pre> Dog.find({"name": "Max"})</pre>
</td>
</tr>
<tr>
<td>sort</td>
<td>
<p>sort items</p>
<p>@see&nbsp;<a href="https://docs.mongodb.com/manual/reference/method/cursor.sort/">cursor.sort</a></p>
</td>
</tr>
<tr>
<td colspan="2">
<p>Get 10 older dogs</p>
<pre>Dog.find().sort("age", {limit: 10})</pre>
</td>
</tr>
<tr>
<td>aggregate</td>
<td>
<p>sum, min, max items</p>
<p>@see&nbsp;<a href="&nbsp;https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/">collection.aggregate</a></p>
</td>
</tr>
<tr>
<td colspan="2">
<p>Get sum of dogs' age</p>
<pre>Dog.find().aggregate({
  "sum_age":  {
     $sum: "age"
   }
})</pre>
</td>
</tr>
</tbody>
</table>

#### 3.2 Transaction

A transaction symbolizes a unit of work performed within a database management system (or similar system) against a database, and treated in a coherent and reliable way independent of other transactions. A transaction generally represents any change in database. Example: Transfer 900$ from Account

`Bob` to `Alice`

```sql
start transaction
select balance from Account where Account_Number='Bob';
select balance from Account where Account_Number='Alice';
update Account set balance=balance-900 here Account_Number='Bob' ;
update Account set balance=balance+900 here Account_Number='Alice' ;
commit; //if all sql queries succed rollback; //if any of Sql queries failed or error
```

**ACID Properties**

In computer science, ACID (Atomicity, Consistency, Isolation, Durability) is a set of properties that guarantee that database transactions are processed reliably. In the context of databases, a single logical operation on the data is called a transaction.

For example, a transfer of funds from one bank account to another, even involving multiple changes such as debiting one account and crediting another, is a single transaction. ![][16]

### 4\. Backup and Restore

Sometimes it is desired to bring a database back to a previous state (for many reasons, e.g., cases when the database is found corrupted due to a software error, or if it has been updated with erroneous data). To achieve this a backup operation is done occasionally or continuously, where each desired database state (i.e., the values of its data and their embedding in database's data structures) is kept within dedicated backup files (many techniques exist to do this effectively). When this state is needed, i.e., when it is decided by a database administrator to bring the database back to this state (e.g., by specifying this state by a desired point in time when the database was in this state), these files are utilized to restore that state.

### 5\. Migration

In software engineering, schema migration (also database migration, database change management) refers to the management of incremental, reversible changes to relational database schemas. A schema migration is performed on a database whenever it is necessary to update or revert that database's schema to some newer or older version. Example: Android Migration by droid-migrate

```shell
droid-migrate init -d my_database droid-migrate generate up droid-migrate generate down
```

Example: Database Seeding with Laravel

### 6\. Active record pattern | Object-Relational Mapping (ORM)

Object-relational mapping in computer science is a programming technique for converting data between incompatible type systems in object-oriented programming languages. This creates, in effect, a "virtual object database" that can be used from within the programming language. There are both free and commercial packages available that perform object-relational mapping, although some programmers opt to create their own ORM tools.

**Example**

`php`

```php
$employee = new Employee(); $employee->setName("Joe"); $employee->save();
```

`Android`

```java
public class User {
  @DatabaseField(id = true) String username;
  @DatabaseField String password;
  @DatabaseField String email;
  @DatabaseField String alias;
  public User() {} }
```

**Implementations**

* Android: [ormlite-android]
* PHP: [Eloquent]

