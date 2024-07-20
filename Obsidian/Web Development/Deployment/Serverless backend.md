- [Serverless Backend](https://projects.100xdevs.com/tracks/eooSv7lnuwBO6wl9YA5w/serverless-1) notes
- [how cloudfare workers work](https://developers.cloudflare.com/workers/reference/how-workers-works/#:~:text=Though%20Cloudflare%20Workers%20behave%20similarly,used%20by%20Chromium%20and%20Node)
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
```
npm create cloudflare -- my-app
```

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

```jsx

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

```

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
// (c) worksd as both as (req,res)
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

### Refferences
- [couldfare workers examples ,tutorials](https://developers.cloudflare.com/workers/examples/)
- [hono doc](https://hono.dev/docs/getting-started/cloudflare-workers)

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
