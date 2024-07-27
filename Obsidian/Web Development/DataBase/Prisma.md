https://projects.100xdevs.com/tracks/gZf9uBBNSbBR7UCqyyqT/prisma-10

```ts
//Schema.prisma

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = "postgresql://neonDB.url"
}

model User {
  id         Int      @id @default(autoincrement())
  username   String   @unique
  password   String
  // firstName  String?   //means optional
  firstName  String
  lastName   String
}

model Todo {
  id          Int     @id @default(autoincrement())
  title       String
  description String
  done        Boolean @default(false)
  userId      Int
}
```

now as the schema is being created we need to generate migrations 
so that the DB can now have the updated schema
`npx prisma migrate dev --name Initialize the schema`

```sql
-- Migration.sql

-- CreateTable
CREATE TABLE "User" (
    "id" SERIAL NOT NULL,
    "username" TEXT NOT NULL,
    "password" TEXT NOT NULL,
    "firstName" TEXT NOT NULL,
    "lastName" TEXT NOT NULL,

    CONSTRAINT "User_pkey" PRIMARY KEY ("id")
);

-- CreateTable
CREATE TABLE "Todo" (
    "id" SERIAL NOT NULL,
    "title" TEXT NOT NULL,
    "description" TEXT NOT NULL,
    "done" BOOLEAN NOT NULL DEFAULT false,
    "userId" INTEGER NOT NULL,

    CONSTRAINT "Todo_pkey" PRIMARY KEY ("id")
);

-- CreateIndex
CREATE UNIQUE INDEX "User_username_key" ON "User"("username");

```

now as the schema and all has been created we need to generate clients so that we can use then in the app 
`npx prisma generate`

**uuid is a popular way to store id in the db**

#### Insert Function
Create a function that lets you inserts data in the user table
```ts
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

// prisma creates the user schema in the database by autogenerating the client
// prisma.user.create({
// })

// Insert Function
async function insertUser(
  username: string,
  password: string,
  firstName: string,
  lastName: string
) {
  const res = await prisma.user.create({
    data: {
      username,
      password,
      firstName,
      lastName,
    },
    // this tells what should be selected from the query
    //say, i want to put in data but i only want the id to be returned back the query, i dont want username, password, etc
    select: {
      id: true,
    },
    //so now res will contain just the id
  });
  console.log(res);
}

insertUser("admin1", "123456", "harkirat", "singh");
```

Output in the terminal
```bash
❯ tsc -b
❯ node dist/index.js
{
  id: 7,
  username: 'DishaLOver',
  password: '123456',
  firstName: 'Disha',
  lastName: 'Patani'
}
```
why the id is changed or jumped 
- due to errornous queries
#### Update Data in the users table
```ts
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

interface UpdateParams {
  firstName: string;
  lastName: string;
}

async function updateUser(
  username: string,
  { firstName, lastName }: UpdateParams,
) 
{
  const res = await prisma.user.update({
    where: { username },
    data: {
      firstName,
      lastName,
    },
  });
  console.log(res);
}

//so u are updating user based on username
updateUser("admin1", {
  firstName: "BAncho",
  lastName: "singh",
});
```

output
```bash
❯ node dist/index.js
{
  id: 4,
  username: 'admin1',
  password: '123456',
  firstName: 'BAncho',
  lastName: 'singh'
}
```

#### Fetch the details of a user given their email
```ts
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

async function getUser(username: string) {
  const user = await prisma.user.findFirst({
    where: {
        username: username
    }
  })
  console.log(user);
}

getUser("admin1");
```

Output
```bash
❯ node dist/index.js
{
  id: 4,
  username: 'admin1',
  password: '123456',
  firstName: 'BAncho',
  lastName: 'singh'
}
```

#### Relationship
types of relationship --
- one to one 
- one to many
- many to one
- many to many 

For a simple todo app, there id one to many relationship
So a person can have multiple todos associated with him

Updating prisma schema
```ts
//Prisma.schema

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = "postgresql://postgres:mysecretpassword@localhost:5432/postgres"
}

model User {
  id         Int      @id @default(autoincrement())
  username   String   @unique
  password   String
  firstName  String
  lastName   String
  todos      Todo[]
}

model Todo {
  id          Int     @id @default(autoincrement())
  title       String
  description String
  done        Boolean @default(false)
  userId      Int
  user        User    @relation(fields: [userId], references: [id])
}
```

update db, create migrations and client
```
npx prisma migrate dev --name relationship
npx prisma generate
```

#### Todo Functions
-  Create Todo --- put todo in the db
```ts
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

async function createTodo(userId: number, title: string, description: string) {
  const todo = await prisma.todo.create({
    data: {
      title,
      description,
      userId
    },
  });
  console.log(todo);

}

getUser(1, "go to gym", "go to gym and do 10 pushups");
```

- get Todos --- get all the todos for a user
```ts
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

async function getTodos(userId: number, ) {
    const todos = await prisma.todo.findMany({
        where: {
        userId: userId,
        },
    });
    console.log(todos);
}

getTodos(1);
```

- getTodosAndUserDetails 
```ts
//Wrong Approach using 2 Queries

import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

async function getTodosAndUserDetails(userId: number) {
    const user = await prisma.user.findUnique({
        where: {
            id: userId
        }
    });
    const todos = await prisma.todo.findMany({
        where: {
            userId: userId,
        }
    });
    console.log(todos);
    console.log(user)
}

getTodosAndUserDetails(1);
```

```ts
// Elegant approach --->  using Joins

import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

async function getTodosAndUserDetails(userId: number, ) {
    const todos = await prisma.todo.findMany({
        where: {
            userId: userId,
        },
        select: {
            user: true,
            title: true,
            description: true
        }
    });
    console.log(todos);
}

getTodosAndUserDetails(1);
```
