https://projects.100xdevs.com/tracks/g0AcDSPl74nk45ZZjRdU/aws-4

use of Aws-AWS is Amazon’s cloud service. It let’s you 
- Rent servers
- Manage domains
- Upload objects (mp4 files, jpgs, mp3s …)
- Autoscale servers
- Create k8s clusters

## EC2
Vms on AWS are known as EC2 servers [ Elastic Compute Machine Version 2]
- Elastic - u can easily increase or decrease the compute of the machine 
- compute - the machine which has its own cpu, memory ,etc

### initializing a EC2
- intialize an EC2 instance , allow traffic on the http,https
- save the key pair file 
- ssh into the vm using it

keypair helps to ssh into the VM 

```
chmod 700 password.pem
```
this 'chmod' cmd helps to prevent other user from accessing the file, so that only you can access it

ssh into the machine 
```jsx
ssh -i kirat-class.pem ubuntu@ec2-65-0-180-32.ap-south-1.compute.amazonaws.com
```

#### Hitting the Server 
