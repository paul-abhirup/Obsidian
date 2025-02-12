similar projects -
zep

Why are you building the project / What can I learn from it --
- Learn how to think like Harkirat
- A preety good real world project 
	- Huge backend practice
	- Huge Frontend skill needed too
- 

*QDD [Question Driven Development]
- Think of an end goal
- Break it into a series of question or modules smallest parts then integrate them together; and google out things
- Cloning to upskill and learn the art

### Features -
 - talk in private lounges


### Harkirat thinking pattern
- feature planning
- designing architechture
- question driven development
- test driven development
- solving bugs learning and applying
- improving the app

//// generaly, the frontend is a side track along with building the backend app.


## **Thinking Process step by step --->

- [ ] Figure out the Architechture
- [ ] Designing the API
	- [ ] Websocket Schema
		- [ ] Client Server Events
		      - Join a space
		      - Movement
		        
		- [ ] Sever Sent Events
		      - Space Joined
		      - Movement Required
		      - Movement
		      - Leave
		      - Join Event
		        
	- [ ] Building the API
	      
	- [ ] DB Schema	
		 [https://www.prismabuilder.io/](https://www.prismabuilder.io/)	
		```sql
		model User {
		  id       String  @id @unique @default(cuid())
		  username String  @unique
		  password String  @unique
		  avatarId String?
		  role     Role
		}
		
		model Space {
		  id        String  @id @unique @default(cuid())
		  name      String
		  width     Int
		  height    Int?
		  thumbnail String?
		}
		
		model spaceElements {
		  id        String @id @unique @default(cuid())
		  elementId String
		  spaceId   String
		  x         Int
		  y         Int
		}
		
		model Element {
		  id       String @id @unique @default(cuid())
		  width    Int
		  height   Int
		  imageUrl String
		}
		
		model Map {
		  id     String  @id @unique @default(cuid())
		  width  Int
		  height Int
		  name   String
		}
		
		model mapElements {
		  id        String  @id @unique @default(cuid())
		  mapId     String
		  elementId String?
		  x         Int?
		  y         Int?
		}
		
		model Avatar {
		  id       String  @id @unique @default(cuid())
		  imageUrl String?
		  name     String?
		}
		
		enum Role {
		  Admin
		  User
		}
		```
		
- [ ] writing the tests **(TDD) // Test driven development**
- [ ] Creating a monorepo
- [ ] writing the backend
- [ ] writing the websocket layer
- [ ] Dockerizing the APP
- [ ] Pushing to github
- [ ] Creating a fresh kubernates clusture
	- [ ] Adding cert-manager, nginx-ingress and AgroCD
	- [ ] Initializing a gitrepo, adding all the manifests
- [ ] writing the CI/CD pipelines to deploy to cluster
- [ ] Frontend
- [ ] Discussing the video architechture
- [ ] DB/Redis in cluster? or outiside?
- [ ] Migrating to Go ?