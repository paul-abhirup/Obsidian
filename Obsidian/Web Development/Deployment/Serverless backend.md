##### Refferences
- [Serverless Backend](https://projects.100xdevs.com/tracks/eooSv7lnuwBO6wl9YA5w/serverless-1) notes
- [how cloudfare workers work](https://developers.cloudflare.com/workers/reference/how-workers-works/#:~:text=Though%20Cloudflare%20Workers%20behave%20similarly,used%20by%20Chromium%20and%20Node)
- [couldfare workers examples ,tutorials](https://developers.cloudflare.com/workers/examples/)
- [hono doc](https://hono.dev/docs/getting-started/cloudflare-workers)
## Initialize a Worker
using cloudfare gui worker to deploy app
```jsx
export interface Env {

}

export default {
async fetch(request, env, ctx): Promise<Response> {
	return new Response('Hello World!');
},
} satisfies ExportedHandler<Env>;
```

intializing worker from cli
```bash
npm create cloudflare -- my-app
//select no for deployment

npm run dev
// to run worker locally
```

Return a json
```jsx
export interface Env {

}

// return a json response
export default {
	async fetch(request: Request, env: Env, ctx: ExecutionContext): Promise<Response> {
		return Response.json({
			message: "hi"
		});
	},
};
```

```ts
//routing is difficult to implement in workers like this way 
// no clean routing like express
//app.get()
//app.post()
 
export default {
	async fetch(request: Request, env: Env, ctx: ExecutionContext): Promise<Response> {
		console.log(request.body);
		console.log(request.headers);
		console.log(request.method);

		// handles the get request
		if (request.method === "GET") {
			return Response.json({
				message: "you sent a get request"
			});
		} else {
			return Response.json({
				message: "you did not send a get request"
			});
		}
	},
};

```

cloudfare doesn't gives a routing library / http server like express in nodeJs
classic serverless - one that doesnt have their own runtime
```js
//login in the cloudfare accn in cli
npx wrangler login

//user details
npx wrangler whoami

//to run it locally
npm run dev

//delpoy the app in internet
wrangler delpoy
//or
npm run deploy
//then the app will start running if all is ok
```

### Creating Hono App
```jsx
//initializing hono app
//hono - routing engine that helps to route like express

npm create hono@latest my-app
//select cloudfare workers as the run time

cd my-app

npm i
```

```ts
//creating hono app
import { Hono } from 'hono'

const app = new Hono()

// (c) = context object
// (c) works both as (req,res)
app.get('/get', (c) => {
  // body, headers, query params, middlewares, connecting to a database, etc
  return c.json({
    msg:'Hello Hono!'
  });
})

app.post('/post', (c) => {
  return c.text('Hello Hono!')
})

export default app

```

#### Getting inputs from the user
```js
import { Hono } from 'hono'

const app = new Hono()

// fetch => await json
app.get('/', async (c) => {
  const body = await c.req.json()
  console.log(body);
  console.log(c.req.header("Authorization"));
  console.log(c.req.query("param"));

  return c.text('Hello Hono!')
})

export default app
```

## Middleware
https://hono.dev/docs/guides/middleware

```jsx
import { Hono } from "hono";

const app = new Hono();

function authMiddleware(c: any, next: any) {
  if (c.req.header("Authorization")) {
    //do validation
    return next();
  } else {
    return c.text("Unauthorized");
  }
}

// app.use(authMiddleware);

// fetch => await json
app.post("/", authMiddleware, async (c) => {
  const body = await c.req.json();
  console.log(body);
  console.log(c.req.header("Authorization"));
  console.log(c.req.query("param"));

  return c.text("Hello Hono!");
});

export default app;

```


### Connecting to a DB
- https://www.prisma.io/docs/orm/prisma-client/deployment/edge/deploy-to-cloudflare
- https://www.prisma.io/docs/accelerate
- https://projects.100xdevs.com/tracks/eooSv7lnuwBO6wl9YA5w/serverless-12

##### Connection pooling in prisma for a serverless app
```bash
// create  cloudflare project
// initalize hono app ,backend as dir,ts,npm

npm install --save-dev prisma

npx prisma init

// create a schema 

npx prisma migrate dev --name init

// use the Prisma Accelerate API key in the env variable

npm install @prisma/extension-accelerate

npx prisma generate --no-engine

//setup ur code

//deploy

```

wrangler.toml
- all env variables used in index.ts
- contains the env variables that will be used by the cloudflare workers        ---> connection pooling string 
- so the env variables stored here are being used by the /backend/hono-app running in the cloudflare workers , running in cloudflare runtime

.env 
- contains the original database url 
- as it need to generate the migration, schema files 
- deals with anything that runs in the CLI  --> nodeJS
	- EX-  prisma migrate , Prisma generate

Prisma Schema --->original DB url ---> .env
index.ts(hono app) --->connection pooling --->  wrangler.toml


Example of a hono app using pooling url to connect to DB
```ts
//index.ts

import { Hono, Next } from 'hono'
import { PrismaClient } from '@prisma/client/edge'
import { withAccelerate } from '@prisma/extension-accelerate'
import { env } from 'hono/adapter'

const app = new Hono()

app.post('/', async (c) => {
  // Todo add zod validation here
  const body: {
    name: string;
    email: string;
    password: string
  } = await c.req.json()
  const { DATABASE_URL } = env<{ DATABASE_URL: string }>(c)

  const prisma = new PrismaClient({
      datasourceUrl: DATABASE_URL,
  }).$extends(withAccelerate())

  console.log(body);

  await prisma.user.create({
    data: {
      name: body.name,
      email: body.email,
      password: body.password
    }
  })
  
  return c.json({msg: "as"})
})

export default app
```

Majority of this difficult concepts are cleared while making medium app