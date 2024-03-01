#### aws:

- **region** - physical entity throughout the world.
- **1 region - 3 aval zone** (nearby 100km one -another)
- **availability zone** (inside region many ) - all servers are here.
- **local zones** - (inside aval -zone - city - delhi)
- **replica** - copy of resource (stored diff loc to avoid fault tolerance or any natural calamity.)

#### AWS - EC2 (Elastic Compute ):

- here we will create an compute instance or vm and access it using ssh

#### Steps to create:

1. set **name**
2. search your **os** and select
   - platform - ubuntu
   - root device - ebs
   - virtualization - hvm
3. Instance type:

   - select based on requirement

4. Create Key pair:

   - select .ppm type and download it

5. Firewall (security group):

   - create security group
   - allow ssh traffic from 0.0.0.0 for now or you can set it to your ip
   - if you want to run web server then can allow http, https also

6. Storage configure:
   - same to our c drive
7. create instance

#### How to connect:

change the permission

- chmod 400 "first-demo.pem"
  ssh -i `<name of .pem>` `<instance public dns> || ip`
- ssh -i "first-demo.pem" ubuntu@ec2-43-205-127-36.ap-south-1.compute.amazonaws.com

#### install nginx:

```bash
apt install nginx
nginx -t #to test conf


curl localhost #to see its index
cd /var/www/html
#  and see the index.html file

```

#### Problem:

- create a instance of EC2 - write script to install nginx and show custom message on index page
  soln- add the shell script in the user section during instance creation for ex - nginx installation and run index file on localhost

#### Security groups:

1. **inbound** - to connect with instance - should be set to ssh

   - In the inbound rule set ssh and source to your ip

2. **outbound** - instance will connect to which net by default all

**Note**

- using **security group** we can only add new rule not removed i.e. if we want to configure to restrict someone from specific ip we can't do that.
- we can set multiple security group to one server.

#### EC2 Instance Type:

1. general purpose
2. compute optimize
3. memory optimize
4. Accelated Computing

**Note**:

- Based on your requirement go to page and select

#### Pricing Model:

**On Demand Instance**:

- maxm pricing but available

**Reserved Instance**:

- maxm discount (depends duration, quantity, etc)

**Spot Instance**:

- maxm discount from all but no reliability if someone pay more than you the resource allocated to him/her.

**Dedicated Host Instance**:

- for private or not shared to anothers.

**saving plans**:

- for private or not shared to anothers.

#### Ways to find medata of vm:

- public ip
- private ip
- instance id

```bash
curl 169.254.169.254
hit enter and select latest/meta-data/network
```

using this info you can pass script to get info about the vm meta-data

**Note**:

- whenever you start and stop instance will change ip address to make it persist ?

#### How to set static ip to ec2 instance:

- create ip
- go to action tab -> associate elastic ip -> select the created one
- now on start/stop public ip will not change

**Use Cases**

- if you chage something on your server and which create stop/start your server then your website points to different ip address which was stopped one.
- or any change to your db which leads to start/stop your server
- we can set 5 elastic ip

#### EBS volume:

- it is connected via network
- if instance
- can we attach multiple instace to same ebs
  - yes, there are two types of ebs which can be attach to multiple instance
  - no, there are four types of ebs which can't be attach to multiple instance
- By default aws create one replica of ebs to same local zone to prevent loss
