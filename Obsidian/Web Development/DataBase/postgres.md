https://projects.100xdevs.com/tracks/YOSAherHkqWXhOdlE4yE/sql-11

Connecting to PostgreSQL Using SSL. 
SSL (Secure Sockets Layer) is a standard protocol for secure access to a remote machine over untrusted networks.
so connecting to PSQL db using ssl is secured
#### Create Table in Postgres 
```jsx

// write a function to create a users table in your database.
import { Client } from 'pg'

const client = new Client({
  connectionString: "sql-string"
})

async function createUsersTable() {
  await client.connect()
  const result = await client.query(`
        CREATE TABLE users (
            id SERIAL PRIMARY KEY,
            username VARCHAR(50) UNIQUE NOT NULL,
            email VARCHAR(255) UNIQUE NOT NULL,
            password VARCHAR(255) NOT NULL,
            created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
        );
    `)
  console.log(result)
}
 
createUsersTable();
  
  // `` is a template string //used to write multi-line query  
```

#### Interacting with the database
- Insert
```
INSERT INTO users (username, email, password)
VALUES ('username_here', 'user@example.com', 'user_password');
```

- Update
```
UPDATE users
SET password = 'new_password'
WHERE email = 'user@example.com';
```

- Delete
```
DELETE FROM users
WHERE id = 1;
```

- Select
```
SELECT * FROM users
WHERE id = 1;
```
asterix is a wildcard character that represents all columns in the table

#### Creating a NodeJS app
```bash 
npm init -y

npx tsc --init
"rootDir": "./src",
"outDir": "./dist",

npm install pg
npm install @types/pg
```
#### Insert Data into a table
```ts
import { Client } from "pg";

// Async function to insert data into a table
async function insertData(username: string, email: string, password: string) {
  const client = new Client({
    host: "localhost",
    port: 5432,
    database: "postgres",
    user: "postgres",
    password: "mysecretpassword",
  });

  //we can also use connection string to connect to the database instead
  // const client = new Client({
  //   connectionString: "sql-string"
  // });

  try {
    await client.connect(); // Ensure client connection is established

    //wrong approach
    //this leaads to sql injection
    //dont put the data provided by the user directly into the query
    // const insertQuery = "INSERT INTO users (username, email, password) VALUES ('username2', 'user3@example.com', 'user_password');";

	//you dont put the user provided strings in the SQL string
    // Use parameterized query to prevent SQL injection
    const insertQuery =
      "INSERT INTO users (username, email, password) VALUES ($1, $2, $3)";
    const values = [username, email, password];
    const res = await client.query(insertQuery, values);

    console.log("Insertion success:", res); // Output insertion result
  } catch (err) {
    console.error("Error during the insertion:", err);
  } finally {
    await client.end(); // Close the client connection
  }
}

// Example usage
insertData("username5", "user5@example.com", "user_password").catch(
  console.error
);

```

#### Fetch data from the database given a email as input
```ts
import { Client } from "pg";

// Async function to fetch user data from the database given an email
async function getUser(email: string) {
  const client = new Client({
    host: "localhost",
    port: 5432,
    database: "postgres",
    user: "postgres",
    password: "mysecretpassword",
  });

  try {
    await client.connect(); // Ensure client connection is established
    const query = "SELECT * FROM users WHERE email = $1";
    const result = await client.query(query, [email]);

    if (result.rows.length > 0) {
      console.log("User found:", result.rows[0]); // Output user data
      return result.rows[0]; // Return the user data
    } else {
      console.log("No user found with the given email.");
      return null; // Return null if no user was found
    }
  } catch (err) {
    console.error("Error during fetching user:", err);
    throw err; // Rethrow or handle error appropriately
  } finally {
    await client.end(); // Close the client connection
  }
}

// Example usage
getUser("user5@example.com").catch(console.error);

```


#### Relationship
```SQL
-- Relationship - the connection between the address table and user table
-- here we are creating the table, while defining the relationship  between the address and users

CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE addresses (
    id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL,
    city VARCHAR(100) NOT NULL,
    country VARCHAR(100) NOT NULL,
    street VARCHAR(255) NOT NULL,
    pincode VARCHAR(20),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

SQL Query 
```sql

INSERT INTO addresses (user_id, city, country, street, pincode)
VALUES (1, 'New York', 'USA', '123 Broadway St', '10001');

SELECT city, country, street, pincode
FROM addresses
WHERE user_id = 1;
```

#### Transactions
transactions  in SQL to ensure either both the user information and address goes in, or neither does

Sql queries
```sql
BEGIN; -- Start transaction

INSERT INTO users (username, email, password)
VALUES ('john_doe', 'john_doe1@example.com', 'securepassword123');

INSERT INTO addresses (user_id, city, country, street, pincode)
VALUES (currval('users_id_seq'), 'New York', 'USA', '123 Broadway St', '10001');

COMMIT; -- End transaction
```

NodeJS code implementing the queries
```ts
import { Client } from 'pg';

async function insertUserAndAddress(
    username: string, 
    email: string, 
    password: string, 
    city: string, 
    country: string, 
    street: string, 
    pincode: string
) {
    const client = new Client({
        host: 'localhost',
        port: 5432,
        database: 'postgres',
        user: 'postgres',
        password: 'mysecretpassword',
    });

    try {
        await client.connect();

        // Start transaction
        await client.query('BEGIN');

        // Insert user
        const insertUserText = `
            INSERT INTO users (username, email, password)
            VALUES ($1, $2, $3)
            RETURNING id;
        `;
        const userRes = await client.query(insertUserText, [username, email, password]);
        const userId = userRes.rows[0].id;

        // Insert address using the returned user ID
        const insertAddressText = `
            INSERT INTO addresses (user_id, city, country, street, pincode)
            VALUES ($1, $2, $3, $4, $5);
        `;
        await client.query(insertAddressText, [userId, city, country, street, pincode]);

        // Commit transaction
        await client.query('COMMIT');

        console.log('User and address inserted successfully');
    } catch (err) {
        await client.query('ROLLBACK'); // Roll back the transaction on error
        console.error('Error during transaction, rolled back.', err);
        throw err;
    } finally {
        await client.end(); // Close the client connection
    }
}

// Example usage
insertUserAndAddress(
    'johndoe', 
    'john.doe@example.com', 
    'securepassword123', 
    'New York', 
    'USA', 
    '123 Broadway St', 
    '10001'
);
```
### Joins
https://projects.100xdevs.com/tracks/YOSAherHkqWXhOdlE4yE/sql-11