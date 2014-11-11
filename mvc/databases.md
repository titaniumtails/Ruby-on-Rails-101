#Databases
We usually create a model without a database first, and then add in the database connectivity later. But most models an rails will be connected to database tables; and in real world development, the process of creating those models, usually begins by first defining the database tables.

A database table is similar to an Excel table with columns and rows:
![Database Table Spreadsheet](https://www.dropbox.com/s/j8q8l2u35aoeyr8/Database%20tables.tiff "Database Table")
But they are not laid out in front of us like a visual medium above. We have to issue commands to interact the database.

You can have multiple tables. And so, databases can also have relationships between tables. This is why we call them: **Relational Databases**.

####Vocabulary
+ **Database** - a set of tables
  + not the same thing as  "a table". Its is a collection of tables.
  + One database = one application (typically).
  + Usually in snake_case
  + Access permissions are granted at database level

+ **Table**
  + A set of columns and rows
  + 1 Table = 1 Model
  + Plural
  + Where relationships are defined
+ **Columns** - These are table fields that define the data that will be stored. For e.g. `first_name` or '`city`.

+ **Column** -  A set of a single simple type, like a string or integer. (In a Rails Model, this is a single attribute).

+ **Rows**  - are the individual records or instances. For e.g. If I have 20 customers, I have 20 rows.

+ **Row** - Single record of data. E.g. "harry", "wong", "harrys@world.com"

+ **Field** - Intersection of a column and a row. E.g. Name: "Harry".

+ **Index** - Increases the lookup speed, like the back of a book.

+ **Foreign keys** - A table column, whose values reference rows in another table. Foreign keys plovide a relationship that is the foundation of relational databases. E.g. `post_id` Its singular.
**TIP**: Put indexes on foreign keys, so you can look up these ∝ very quickly

+ **Schema** - The structural definition of the database; the tables, the columns, the indexes, everything that makes up the database. If we import a schema into our database, it will create a complete database for us, although with no data in it, but with the correct structure.

+ **CRUD** - The 4 main ways we interact with the database.
  * Create  new data
  * Read    existing data
  * Update  existing data with new data
  * Delete  existing rows of data
