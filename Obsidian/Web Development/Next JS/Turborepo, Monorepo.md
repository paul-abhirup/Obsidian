its more of coding practice, structure

- Why monorepo?
	- single repo for both frontend and backend
	- optimised builds, CI/CD, etc
- monorepo frameworks, History
- Build system v/s Build system orchestrator v/s Monorepo framework
- Turborepo as a build system orchestrator
- intialize Turborepo
- Folder Structure 
- root package.json
- packages/ui
- apps/web
- adding a page, importing an UI component
- turbo.json
	- https://turbo.build/repo/docs/getting-started/create-new#3-understanding-turbojson
	- https://turbo.build/repo/docs/reference/configuration#globaldependencies
- adding react 
	- https://turbo.build/repo/docs/core-concepts/monorepos/configuring-workspaces
	- importing ui compoenents into the react-app
- caching in turborepo
- adding Nodo.js app
	- imp base tsconfig
		- https://github.com/vercel/turbo/blob/main/examples/kitchen-sink/apps/api/tsconfig.json\
	```json
		{
	  "extends": "@repo/typescript-config/base.json",
	  "compilerOptions": {
	    "lib": ["ES2015"],
	    "module": "CommonJS",
	    "outDir": "./dist",
	    "rootDir": "./src"
	  },
	  "exclude": ["node_modules"],
	  "include": ["."]
	}
	```
	
	-  add dependencies, write code
	- update turbo.json
	```json
	{
	  "extends": ["//"],
	  "pipeline": {
	    "build": {
	      "outputs": ["dist/**"]
	    }
	  }
	}
	```

- adding common module
	- 

