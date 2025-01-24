part 1 - https://projects.100xdevs.com/tracks/Paytm/paytm17-1
part 2 - 

#### User login
1. Auth (In this case, probably email/phone)
2. On ramp from bank, off ramp to bank
3. Support transfers via phone number/name
4. Support scanning a QR code for transferring to merchants

#### Merchant login
1. Login with google
2. Generate a QR Code for acceptance
3. Merchants get an alert/notification on payment
4. Merchant gets money offramped to bank every 2 days

tech stack --->>>
- next js
- express backend
- typescript
- turborepo
- postgresDB
- Prisma ORM
- tailwind


## Documentation --
1. initialize turborepo
2. add tailwind
	1. intialize tailwind
	2. modify tailwind config
	3. debug if tailwind is not working
	// its imp to install tailwind in the user-app not in the root folder 
3. adding prisma
	1. init npm and ts
	2. change the npm package name @repo/db
	   // this can be any name used for the repo
	   paytm/deb , etc
	3. change tsconfig // edit the @repo/tsconfig/base.json
	4. npx prisma init
	5. edit .env with db url, add basic schema
	6. npx prisma migrate dev --name init
	7. *So when you do prisma migrate, 
	   u see that the migration file gets generated in the node modules
	   u can easily now use the client any where within the app 
	   but its a good practice to share it from the db folder *
	8. So we create a index.ts and migrate the prisma client   
	   `export * from '@prisma/client';`
	9. now add the export in package.json
	   ```js
	   "exports": {			
			"./client": "./index.ts"			
		}
		```
	   if you dont do this and instead use 
	   `./src/index.ts ` it gives an error in expoting the prisma client 
	10. also add the @repo/db as a dependency in the global package.json	    
	    **also using `npm i @repo/db` works fine **
4. *class 2 starts here; and 1-14 are being covered till monorepo part*
5. adding recoil/ store module
	1. cd packages/store
	   // used to store all the recoil/store module
	2. `npm init -y`  
	  `npx tsc --init`
	  `npm i recoil`
	3. configure tsconfig  @repo/typescript-config/react-library.json
	4. configure package.json @repo/store
	5. create a  
6. import recoil in the next app
7. next auth
8. add auth
9. adding appbar
10. on raming
11. create a generic appbar
12. create sidebar
13. create transfer page
14. add some seed data
15. make landing page redirect
16. 