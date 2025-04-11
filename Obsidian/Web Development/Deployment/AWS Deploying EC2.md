have access of the pem file 
```
chmod 700 password.pem
```
this 'chmod' cmd helps to prevent other user from accessing the file, so that only you can access it
other user --- mean the users in the pc like other user profile - gogo,etc

ssh into the machine 
```jsx
ssh -i harkirat-passkey-awscls.pem ubuntu@54.90.184.231

ssh -i you-pem-file.pem os@ipv4-of-EC2
```
some time the aws server doesnt have the access to the internet --figure it out by googling not an imp thing to remember

short --
`sudo vi /etc/resolve.conf`
add `nameserver 8.8.8.8`
:wq ------> this saves the file 

this will sets you up to use the internet 
//google out for the issue

Installing node in the system
`Its prefferable to use the nvm for the node installation`

use the digitalOcean docs how to install nodeJS in ubuntu

```bash
npm install 

node index.js
//this turn on the server 
```
#### Hitting the Server
You have an IP and DNS of the EC2 machine that you can hit to access the server 
but this will not work as the port access of the machine is not open

so to open the ports of the machine go to the security group of the EC2
add open port 8080 and its access 

as the server is running at port 8080

you can't hit the server at https as it listen to the to the 443

so you have to hit the http port 
`http://54.90.184.231:8080/todos`   Ipv4 DNS
`http://ec2-54-90-184-231.compute-1.amazonaws.com:8080/todos`  public Ipv4

after running the `node index.js`
and closing the connection with the Ec2 instance, you can still hit the node machine in the server 

i mean the server is still running in the port:8080 

only rebotting the machine cleans out the port of the Ec2

// How to run the index.js process forever 
`npm i -g pm2`
pm2 lets you run the index.js process forever 

#### NGINX
by installng the nginx in the Ec2 instance 
it takes over the port 80 the default http port

now we need to program it in such sa way that it reverse-proxy the request coming to the port 

not an important thing to learn right now as you need subdomain to route the request

create a reverse-proxy
In the DNS section of the domain buyer like godaddy,etc 
and then create 2 sub-domains like
- backend1.100xdevs.com
- backend2.100xdevs.com
```
sudo rm sudo vi /etc/nginx/nginx.conf
// this command deletes the default nginx.conf

sudo vi /etc/nginx/nginx.conf
//this create the nginx conf for the new configuration
```

```bash 
events {
    # Event directives...
}

http {
	server {
    listen 80;
    server_name be1.100xdevs.com;

    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
	}
}
```

restart nginx
`sudo nginx -s reload`

# Certificate Management
https://certbot.eff.org/

