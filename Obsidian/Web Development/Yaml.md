[refference](https://www.freecodecamp.org/news/what-is-yaml-the-yml-file-format/#intro)
YAML is a human-readable data serialization language, just like XML and JSON
```xml
<Employees>
    <Employee> 
        <name> John Doe </name>
        <department> Engineering </department>
        <country> USA </country>
    </Employee>
     <Employee> 
        <name> Kate Kateson </name>
        <department> IT Support </department>
        <country> United Kingdom </country>
    </Employee>
</Employees>
```

```json
{
	"Employees": [
    {
			"name": "John Doe",
			"department": "Engineering",
			"country": "USA"
		},

		{
			"name": "Kate Kateson",
			"department": "IT support",
			"country": "United Kingdom"
		}
	]
}
```

```yaml
Employees:
- name: John Doe
  department: Engineering
  country: USA
- name: Kate Kateson
  department: IT support
  country: United Kingdom
```

we use ( : ) to create key/value pairs 
( - ) to create sequence 

indentation in yaml 
- no tabs
- ''Whitespace doesn't matter as long as child elements are indented inside the parent element''

we can write multiple yaml documents in a single yaml file 
separated by (---) or (...)
```yaml
---
Employees:
- name: John Doe
  department: Engineering
  country: USA
- name: Kate Kateson
  department: IT support
  country: United Kingdom
---
Fruit:
 - Oranges
 - Pears
 - Apples
```

docker compose yaml
```yaml
version: '3.8'
services:
  mongodb:
    image: mongo
    container_name: mongodb
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db

  backend22:
    image: backend
    container_name: backend_app
    depends_on:
      - mongodb
    ports:
      - "3000:3000"
    environment:
      MONGO_URL: "mongodb://mongodb:27017"

volumes:
  mongodb_data:

```

to json
```json
{
  "version": "3.8",
  "services": {
    "mongodb": {
      "image": "mongo",
      "container_name": "mongodb",
      "ports": [
        "27017:27017"
      ],
      "volumes": [
        "mongodb_data:/data/db"
      ]
    },
    "backend22": {
      "image": "backend",
      "container_name": "backend_app",
      "depends_on": [
        "mongodb"
      ],
      "ports": [
        "3000:3000"
      ],
      "environment": {
        "MONGO_URL": "mongodb://mongodb:27017"
      }
    }
  },
  "volumes": {
    "mongodb_data": null
  }
}
```