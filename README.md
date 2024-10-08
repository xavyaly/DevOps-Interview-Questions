# Interview Questions and Answers

Basic defination of CI CD:

CI: Continuous Integration
It’s a part of both Continuous Delivery & Continuous Deployment, involves the testing and building of any new or updated source code.
	
CD: Continuous Delivery
Involves a manual trigger to Production

CD: Continuous Deployment
Involves an Automatic Release to Production

————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

Q: Why Elastic IP is important & why is it used ? Where can we insert in 3-Tier Architecture ?
An Elastic IP address is a reserved public IP address that you can assign to any EC2 instance in a particular region, 
until you choose to release it. To allocate an Elastic IP address to your account in a particular region
Link: https://asmed.com/amazon-aws-assign-an-elastic-ip-address-to-your-instance/

Q: What is ElasticSearch ? What have you implemented with ES ?


Q: Difference between EKS and ECS ? 

Q: What is Shard ?
A shard is both a unit of storage and a unit of computation. Elasticsearch deploys shards independently to the instances in the cluster to parallelize the storage and processing for the index. And it does this elastically (hence the “elastic” in the name “Elasticsearch”)
 
Symbolic links in Linux ?
A symbolic link (or "symlink") is file system feature that can be used to create a link to a specific file or folder. It is similar to a Windows "shortcut" or Mac "alias," but is not an actual file. Instead, a symbolic link is a entry in a file system that points to a directory or file.
Syntax:
ln -s [OPTIONS] FILE LINK
Eg:
Creating Symlink To a File 
ln -s source_file symbolic_link
ln -s my_file.txt my_link.txt
ls -l my_link.txt
lrwxrwxrwx 1 linuxize users  4 Nov  2 23:03  my_link.txt -> my_file.txt
Creating Symlinks To a Directory 
ln -s /mnt/my_drive/movies ~/my_movies
Overwriting Symlinks 
ln -s my_file.txt my_link.txt
ln: failed to create symbolic link 'my_link.txt': File exists
ln -sf my_file.txt my_link.txt
Removing Symlinks
unlink symlink_to_remove
rm symlink_to_remove
https://linuxize.com/post/how-to-create-symbolic-links-in-linux-using-the-ln-command/
 
Q:What will you do if SSH is not working ?
https://docs.digitalocean.com/products/droplets/resources/troubleshooting-ssh/connectivity/#:~:text=Verify%20that%20your%20network%20supports,t%20specific%20to%20your%20Droplet.
Issues:
ssh: Could not resolve hostname example.com: Name or service not known
Unable to open connection to example.com Host does not exist
ssh: connect to host 203.0.113.0 port 22: Connection timed out
Network error: Connection timed out
ssh: connect to host 203.0.113.0 port 22: Connection refused
Network error: Connection refused
Steps:
Checking Your Firewall
iptables -nL
firewall-cmd --list-services
O/P:dhcpv6-client http ssh
ufw status: To inspect the firewall-cmd
Checking the SSH Service Status
service ssh status
systemctl status sshd
Checking the SSH Service Port
grep Port /etc/ssh/sshd_config
 
Q: What does SSH-keygen do?
Ssh-keygen is a tool for creating new authentication key pairs for SSH. Such key pairs are used for automating logins, single sign-on, and for authenticating hosts.
In Cloud we have Key-Pairs to connect EC2 Servers
In Linux: ssh -keygen: provide one public and one private key
In Ansible Configuration: we add the public key to connect with Servers
 
Q: awk command in Linux ? where u have used ?
https://www.geeksforgeeks.org/awk-command-unixlinux-examples/
WHAT CAN WE DO WITH AWK ? 
1. AWK Operations: 
(a) Scans a file line by line 
(b) Splits each input line into fields 
(c) Compares input line/fields to pattern 
(d) Performs action(s) on matched lines 
2. Useful For: 
(a) Transform data files 
(b) Produce formatted reports 
3. Programming Constructs: 
(a) Format output lines 
(b) Arithmetic and string operations 
(c) Conditionals and loops 
Syntax:
awk options 'selection _criteria {action }' input-file > output-file
Options:
-f program-file : Reads the AWK program source from the file 
                  program-file, instead of from the 
                  first command line argument.
-F fs 
Examples:
$cat > employee.txt 
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
deepak clerk sales 23000
sunil peon sales 13000
satvik director purchase 80000 
1. Default behavior of Awk : By default Awk prints every line of data from the specified file. 
$ awk '{print}' employee.txt
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
$ awk '/manager/ {print}' employee.txt 
ajay manager account 45000
varun manager sales 50000
amit manager account 47000 
$ awk '{print $1,$4}' employee.txt 
ajay 45000
sunil 25000
varun 50000
amit 47000
tarun 15000
Built In Variables In Awk
Awk’s built-in variables include the field variables—$1, $2, $3, and so on ($0 is the entire line) — that break a line of text into individual words or pieces called fields. 
NR: NR command keeps a current count of the number of input records. Remember that records are usually lines. Awk command performs the pattern/action statements once for each record in a file. 
NF: NF command keeps a count of the number of fields within the current input record. 
FS: FS command contains the field separator character which is used to divide fields on the input line. The default is “white space”, meaning space and tab characters. FS can be reassigned to another character (typically in BEGIN) to change the field separator. 
RS: RS command stores the current record separator character. Since, by default, an input line is the input record, the default record separator character is a newline. 
OFS: OFS command stores the output field separator, which separates the fields when Awk prints them. The default is a blank space. Whenever print has several parameters separated with commas, it will print the value of OFS in between each parameter. 
ORS: ORS command stores the output record separator, which separates the output lines when Awk prints them. The default is a newline character. print automatically outputs the contents of ORS at the end of whatever it is given to print. 
$ awk '{print NR,$0}' employee.txt: Use of NR built-in variables (Display Line Number) 
1 ajay manager account 45000
2 sunil clerk account 25000
3 varun manager sales 50000
4 amit manager account 47000
5 tarun peon sales 15000
$ awk '{print $1,$NF}' employee.txt: Use of NF built-in variables (Display Last Field) 
ajay 45000
sunil 25000
varun 50000
amit 47000
tarun 15000
$ awk 'NR==3, NR==6 {print NR,$0}' employee.txt: Another use of NR built-in variables (Display Line From 3 to 6) 
3 varun manager sales 50000
4 amit manager account 47000
5 tarun peon sales 15000
6 deepak clerk sales 23000 
 
Q: sed in Linux ?
https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/
SED command in UNIX is stands for stream editor and it can perform lot’s of function on file like, searching, find and replace, insertion or deletion.
Syntax:
sed OPTIONS... [SCRIPT] [INPUTFILE...] 
Example:
$cat > geekfile.txt
unix is great os. unix is opensource. unix is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
 
$sed 's/unix/linux/' geekfile.txt: Replacing or substituting string (first occurance)
linux is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
 
$sed 's/unix/linux/2' geekfile.txt: Replacing the nth occurrence of a pattern in a line
unix is great os. linux is opensource. unix is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.linux is a multiuser os.Learn unix .unix is a powerful.
 
$sed 's/unix/linux/g' geekfile.txt: Replacing all the occurrence of the pattern in a line
linux is great os. linux is opensource. linux is free os.
learn operating system.
linux linux which one you choose.
linux is easy to learn.linux is a multiuser os.Learn linux .linux is a powerful.
 
$sed 's/unix/linux/3g' geekfile.txt: Replacing from nth occurrence to all occurrences in a line
unix is great os. unix is opensource. linux is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn linux .linux is a powerful.
 
 
$ echo "Welcome To The Geek Stuff" | sed 's/\(\b[A-Z]\)/\(\1\)/g': Parenthesize first character of each word
(W)elcome (T)o (T)he (G)eek (S)tuff

 
$sed '3 s/unix/linux/' geekfile.txt: Replacing string on a specific line number
unix is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
 
$sed 's/unix/linux/p' geekfile.txt: Duplicating the replaced line with /p flag
linux is great os. unix is opensource. unix is free os.
linux is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
linux linux which one you choose.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
 
$sed -n 's/unix/linux/p' geekfile.txt: Printing only the replaced lines
linux is great os. unix is opensource. unix is free os.
linux linux which one you choose.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
 
 
 
 
$sed '1,3 s/unix/linux/' geekfile.txt: Replacing string on a range of lines
linux is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
 
$sed '2,$ s/unix/linux/' geekfile.txt
unix is great os. unix is opensource. unix is free os.
learn operating system.
linux linux which one you choose.
linux is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful
 
Q: CloudFront in AWS ?
Amazon CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files, to your users. CloudFront delivers your content through a worldwide network of data centers called edge locations. When a user requests content that you're serving with CloudFront, the request is routed to the edge location that provides the lowest latency (time delay), so that content is delivered with the best possible performance.
If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately.
If the content is not in that edge location, CloudFront retrieves it from an origin that you've defined—such as an Amazon S3 bucket, a MediaPackage channel, or an HTTP server (for example, a web server) that you have identified as the source for the definitive version of your content.
 
Q: RDS: Relational Database System ?
Amazon Relational Database Service (Amazon RDS) makes it easy to set up, operate, and scale a relational database in the cloud. It provides cost-efficient and resizable capacity while automating time-consuming administration tasks such as hardware provisioning, database setup, patching and backups. It frees you to focus on your applications so you can give them the fast performance, high availability, security and compatibility they need.
Amazon RDS is available on several database instance types - optimized for memory, performance or I/O - and provides you with six familiar database engines to choose from, including Amazon Aurora, PostgreSQL, MySQL, MariaDB, Oracle Database, and SQL Server. You can use the AWS Database Migration Service to easily migrate or replicate your existing databases to Amazon RDS.
 
Q: How Fargate Works in AWS ?
With Fargate, you only pay for the resources that you have defined in your tasks. For your tasks that will run on demand or on a schedule and don't need a dedicated EC2 instance. With Fargate, you only pay when your task is running. For your tasks that have peaks Memory and/or CPU usage.
Fargate removes the need to provision and manage servers, lets you specify and pay for resources per application, and improves security through application isolation by design. ... You only pay for the resources required to run your containers, so there is no over-provisioning and paying for additional servers.
 
 
Q: Difference between Fargate and ECS ?
To run containers, you have two options. You can use ECS container instances, or you can use Fargate. Both options work together with ECS. The following figure demonstrates the difference.
ECS Container Service: per running EC2 instance	
Fargate: per running task.
 
Q: What is kubelet in K8s ?
Kubelet: An agent that runs on each node in the cluster. It makes sure that containers are running in a POD.
https://kubernetes.io/docs/concepts/overview/components/

Q: Which IAAS have worked upon ?
Cloud Formation Template


 
Q: What Dockerfile contents ?
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using docker build users can create an automated build that executes several command-line instructions in succession.
 
Q: Docker-Compose:
https://docs.docker.com/compose/gettingstarted/
 
Q: What is the difference between CMD and entrypoint in a Dockerfile?
In a nutshell: CMD sets default command and/or parameters, which can be overwritten from command line when docker container runs. ENTRYPOINT command and parameters will not be overwritten from command line. Instead, all command line arguments will be added after ENTRYPOINT parameters.
 
————————————————————————————————————————

Citadels: 06:00 AM | 06/14/2021

I heard u r busy in prod call, please explain me what is the issue and how you will going to fix it?
Where do you wanna to see yourself after one year?
In which tools you are working??
How important to work closely with Developer and benefits ??
What kind of Prod issue faced by you or your team and how u guys fixed it ??
How branching model, pipeline is working in your team ??
What kind of support u r giving to performance, data scientist team ?
Which monitoring tools were used by you??
He haven’t used any coding platform like as you said during an interview

————————————————————————————————————————————————————————————————————————————————

Explain BGP Border Gateway Protocol
Denial Service Attack
Proxy versus Reverse Proxy
Types of Loadbalancer
Which algorithm does an Elastic Load Balancer use?
HAPROXY VS NGINX (Comparing Load Balancing Options: Nginx vs. HAProxy vs. AWS ELB – See more at: http://www.mervine.net/comparing-load-balancing#sthash.jgaYgVC8.dpuf)
MYSql Storage Engine
MySQL Architecture
Hadoop Acrchitecture & HDFS, Named Node, Data Node, MapReduce
Web 3 tier Architecture
RPO & RTO in disaster Recovery
Bandwidth Throughput Latency
Bandwidth MTU
OLAP and OLTP
Difference between SAN & NAS
Blue Green Deployment
Replication technologies available
Difference between XML & JSON
What is CI(continuous integration) tool and example
Docker
Container
Difference between Docker & Container
What is Memcache
Details of VLAN
Content Delivery/Distribution Network(CDN)
MS SQL to Oracle Migration
Platforms (Power, Sparc, Intel X86)
How do you perform caching?
Do you know EMR and Redshift?
What is the biggest mistake you have made?
What is EBS?
How do you architect a design that is fault tolerant?
What are the services you have used in AWS?
What are some web protocols?
What is TCP and UDP?

————————————————————————————————————————————————————————————————————————————————
Constella Intelligence: 04:00 PM | 06/11/2021
————————————————————————————————————————————————————————————————————————————————

How are you handling services in AWS ?
CLI
CF Template
Manually

How can you give access to Containers to Developers ?
How to Give Developers Access to Kubernetes During Development · Kubernetes Development Blog (devspace.cloud)


How to remove logs older than 7 days from S3 bucket ?
https://thecattlecrew.net/2018/10/12/how-to-use-cloudfront-to-serve-private-s3-bucket-as-website/
https://docs.aws.amazon.com/AmazonS3/latest/API/API_DeleteBucketLifecycle.html


Read about:
s3 presigned url cloudfront


Read about Docker Compose ?

How will you deploy your code from Jenkins to Docker Swarm ?

How can I provide cross-account access to objects stored in my Amazon S3 bucket?

How to access EC2 from a different Region ?

Without stopping EC2 Instance how can copy the Volume to S3 bucket ?

Which Volume is being in Docker Swarm like EFS or Local or other volumes ?


How can your client access the S3 bucket ? Make S3 Public.
https://www.youtube.com/watch?v=6EU1usknD7E
https://digitalcloud.training/certification-training/aws-solutions-architect-associate/storage/amazon-s3/


Complete AWS Videos & Questions ?
https://www.youtube.com/c/DigitalCloudTraining/videos


How are volumes being managed in Docker Swarm ?

How to increase/decrease the volume in Docker ?

Where did you maintain the versioning in CF Template ?

How will you migrate your local volumes in S3 Bucket ?

How does ElasticSearch act in Kibana ?

Who creates the Dockerfile ?
What will you do if any services die in Docker Swarm ?


Production URLs monitoring ?
SiteScope Monitoring Tool


Kibana used for sharing logs with other POCs ?
https://www.elastic.co/kibana


On what basis Auto Scaling works in your CF Template ?


————————————————————————————————————————————————————————————————————————————————
General Python Questions:
https://www.toptal.com/python/interview-questions
————————————————————————————————————————————————————————————————————————————————

NetCracker: 04:00 PM | 05/06/2021
 
Recent Issue faced and how did you fixed it ?
I've been using infinite Pipeline for a demo. The job was running for a couple of hours, and then Jenkins master declined to build due to the StackOverflow.
node {
    int i = 0;
    while(true) {
        sh "echo 'Hello, world ${i}!'"
        sh "sleep 5"
        i = i + 1;
    }
}
//Explore it
https://issues.jenkins.io/browse/JENKINS-38383


How to use ad-hoc commands in Ansible ?
An Ansible ad-hoc command uses the /usr/bin/ansible command-line tool to automate a single task on one or more managed nodes. ... Ad-hoc commands demonstrate the simplicity and power of Ansible. The concepts you learn here will port over directly to the playbook language.
https://www.javatpoint.com/ansible-ad-hoc-commands
Syntax:
ansible <hosts> [-m <module_name>] -a <"arguments"> -u <username> [--become]  
Examples:
Transferring file on many machines or servers: abc is group name in inventory
$ ansible abc -m copy -a "src = /etc/yum.conf dest = /tmp/yum.conf" 
U can say a one line command 


While taking Jenkins complete backup every times our shell scripting code breaks
How to take the Backup & Restore Jenkins completely ?
https://medium.com/@_oleksii_/how-to-backup-and-restore-jenkins-complete-guide-62fc2f99b457
https://gist.github.com/alexsplashex/b996054561ebf9e2e234782e88941d8c
#!/bin/bash
# Jenkins Configuraitons Directory
cd $JENKINS_HOME
# Add general configurations, job configurations, and user content
git add -- *.xml jobs/*/*.xml userContent/* ansible/*
# only add user configurations if they exist
if [ -d users ]; then
    user_configs=`ls users/*/config.xml`
    if [ -n "$user_configs" ]; then
        git add $user_configs
    fi
fi
# mark as deleted anything that's been, well, deleted
to_remove=`git status | grep "deleted" | awk '{print $3}'`
if [ -n "$to_remove" ]; then
    git rm --ignore-unmatch $to_remove
fi
git commit -m "Automated Jenkins commit"
git push -q -u origin master	// Script always fails at here
OR
https://www.tutorialspoint.com/jenkins/jenkins_backup_plugin.htm
“Backup Manager” Plugin
Setup
Backup Hudson Configuration
Restore Hudson Configuration

————————————————————————————————————————————————————————————————————————————————

What is jenkinsfile in Jenkins ?
Using a Jenkinsfile
Jenkinsfile is a text file that contains the definition of a Jenkins Pipeline and is checked into source control. Consider the following Pipeline which implements a basic three-stage continuous delivery pipeline.
//jenkinsfile(Declarative Pipeline)
pipeline{
	agent any
stages(){
	stage('Build'){
		steps{
			echo 'Building..'
		}
	}
	stage('Test'){
		steps{
			echo "Testing.."
			}
	}
	stage('Deploy'){
		steps{
			echo 'Deploying..'
		}
	}
}
}
//jenkinsfile(Scripted Pipeline)
node {
	stage(){
		echo 'Testing..'
	}
	stage(){
		echo 'Building..'
	}
	stage(){
		echo 'Deploying..'
	}
}















What is a Garbage Collector in Java ??
https://www.javatpoint.com/Garbage-Collection
Garbage means unreferenced objects.
Garbage Collection is the process of reclaiming the runtime unused memory automatically. 
In other words, it is a way to destroy the unused objects.
To do so, we were using the free() function in C language and delete() in C++. 
But, in java it is performed automatically. So, java provides better memory management.

Advantage of Garbage Collection:
It makes java memory efficient because the garbage collector removes the unreferenced objects from heap memory.
It is automatically done by the garbage collector(a part of JVM) so we don't need to make extra efforts.

How can an object be unreferenced?
There are many ways:
By nulling the reference
By assigning a reference to another
By anonymous object etc.	

By nulling the reference:
Employee e1 = new Employee();
e1=null();

By assigning a reference to another:
Employee e1=new Employee();
Employee e2=new Employee();
e1=e2; // now the first object referred by e1 is available for GC

By anonymous object:
new Employee();

The finalize() method is invoked each time before the object is garbage collected. 
This method can be used to perform cleanup processing. This method is defined in Object class as:
protected void finalize(){}

The gc() method is used to invoke the garbage collector to perform cleanup processing. 
The gc() is found in System and Runtime classes.
public static void(){}

Example:
public class TestGarbage1{
 public void finalize(){System.out.println("object is garbage collected");}
 public static void main(String args[]){
  TestGarbage1 s1=new TestGarbage1();
  TestGarbage1 s2=new TestGarbage1();
  s1=null;
  s2=null;
  System.gc();
 }
}
O/P:
Compile by: javac TestGarbage1.java
Run by: java TestGarbage1
object is garbage collected
object is garbage collected

What happens if GC will not be added by Developers ?
It will work automatically even if we don’t define in Java
Free() in C
Delete() in C++



How is a service running on a VM different from Docker Containers ?
Services & Containers are related but both are different things.
A Service can be run by one or more containers.
With docker one can handle multiple containers.
With docker-compose one can handle multiple services.

For example:
Let's say that we have this docker-compose.yml file:

web:
  image: example/my_web_app:latest
  expose:
    - 80
  links:
    - db 

db:
  image: postgres:latest
This compose file defines two services, web and db.

When you run docker-compose up, Assuming that the project directory is test1 then compose will start 2 containers named test1_db_1 and test1_web_1.

$ docker ps -a
CONTAINER ID   IMAGE        COMMAND          ...      NAMES
1c1683e871dc   test1_web    "nginx -g"       ...      test1_web_1
a41360558f96   test1_db     "postgres -d"    ...      test1_db_1
So, in this point you have 2 services and 1 container for each.

But you could scale the service named web to use 5 containers.

$ docker-compose scale web=5
Creating and starting 2 ... done
Creating and starting 3 ... done
Creating and starting 4 ... done
Creating and starting 5 ... done
In this point you have 2 services and 6 containers

$ docker ps -a  
CONTAINER ID   IMAGE        COMMAND         ...      NAMES
1bf4c939263f   test1_web    "nginx -g"      ...      test1_web_3
d3033964a44b   test1_web    "nginx -g"      ...      test1_web_4
649bbda4d0b0   test1_web    "nginx -g"      ...      test1_web_5
a265ea406727   test1_web    "nginx -g"      ...      test1_web_2
1c1683e871dc   test1_web    "nginx -g"      ...      test1_web_1
a41360558f96   test1_db     "postgres -d'   ...      test1_db_1
Additionally, with docker-compose you can run subcommand against one or more services.

$docker-compose stop web
Difference between service and container in docker compose - Stack Overflow


How to limit the disk space when the docker container runs?
In the current Docker version, there is a default limitation on the Docker container storage of 10Gb.
As the BlazeMeter image is ~5 GB when the sample.jtl reaches ~5 GB, no more free storage will be left in the container. As there will be no more free storage, JMeter won't be able to continue writing samples to the sample.jtl and that can cause the report to be 'stuck'.
The solution is as follows:
Please run the next set of commands in all of your CentOS machines:
1. sudo service docker stop OR sudo systemctl stop docker
2. Create/edit the following file: 
/etc/docker/daemon.json
with the following content:
{
        "storage-driver": "devicemapper",
        "storage-opts": [
                "dm.basesize=40G"
        ]
}
3. sudo rm -rf /var/lib/docker
4. sudo service docker start OR sudo systemctl start docker
Reinstall the Agent using the regeneration method detailed in this article.
These changes will change the storage limitation in the container to 40 GB and after that, the test should run fine.
NOTE: You can also change the size to whatever you need (i.e. need 50 GB, enter 50G as the value for dm.basesize), as long as your system has the disk space for it. Also, you will not be able to reduce the size once set, so if you make a mistake, you will need to reinstall Docker and our on-premise Agent.
Overcoming Container Storage Limitation – BlazeMeter


How to check the read-write frequency when the container runs ?


Shell Scripting to Ping and Test all IP present in /etc/hosts file ?
https://unix.stackexchange.com/questions/450734/i-need-to-ping-a-list-of-ip-addresses-from-a-file-and-log-the-status-as-up-or
f=open("/etc/hosts","r"):
for line in f:
ping -c 1 "output" >> /dev/null
if [$? -eq 0 ]; then 
echo "IP is UP"
else echo "IP is down"
fi
done


How to see the memory in Linux ?


How to see if the port is enabled or not ?


How to see the space in Linux ?


What does this say: sed -i 's/\\/\//g' some.txt
\\ to \/ replace by it to all inside the file 


Reg Ex: How to search the digits ?
[0-9]


Reg Ex: How to search the alphabets ?
[a-z][A-Z]


How to see the remote port ?
iptables
ufw
netstat -ntlp



Difference between traceroute and tcproute ?
https://linux.die.net/man/1/tcptraceroute
tcproute
traceroute


How to download files in Python ?
https://stackabuse.com/download-files-with-python/
urllib module


SQL to count the no of people from USA ?
https://dba.stackexchange.com/questions/148657/select-countries-and-counts-of-people-per-country
"table: employees
|country|department|quantity|
|India|QA|100|
|India|IT|30|
|India|HR|5|
|USA|QA|50|
|USA|IT|10|"
select usa.country as user_count from country usa


Git Life Cycle whenever some change happened ?
Some file changes how you can add in git ?
git status
git add .
git status
git commit -m "COMMENTS"
git branch 
git push origin <branch_name>
git fetch & git pull


Explain the below Ansible Plybook ?
- name: Playbook
    hosts: webservers
    become: yes
    tasks:
      - name: task1
        yum:
          name: httpd
          state: latest
      - name: task2
        service:
          name: httpd
          state: started


What is Jenkins' file ?


How Master and Slave works and info do you have in Jenkins ?


What is stored in /etc/hosts file 


Ansible Forks ?


How Ansible behaves when 100 nodes are present in Inventory ?


Recent Ansible Playbook you have written & explain ?


Difference between git fetch and git pull ?


No Exposure in Kubernetes ?


No Exposure in Prometeus ?


What exactly you are monitoring through Kibana tool ?


How can give priority inside Ansible Playbook ?


What is swap memory in Linux ?


What happened when swap memory used in place of ram memory ?


How to build a Dockerfile ?

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@


Network ?
No of devices connected to each other over the physical medium
Ex: Internet


Node ?
Node in network called devices


Network topology ?
Physical structure of the network, 
How the computers or node are connected to each other.


Routers ?
It’s a device which is responsible for transferring the data from source to destinations over the computer network.


OSI Model ?
Stands for Open System Interconnection.
Reference Model, how different applications will communicate with each other via computer network.


Different Layers of OSI ?
Different Layers of TCP/IP Model ? (Top 3)
Application Layer: End user will interact with the Application Layer
Transport Layer: Transfer data from one to another
Network Layer: Transfer data from one to another
Physical Layer: Converts data bits into an electrical impulse
Datalink Layer: Converts data packet will be encoded and decoded into bits
Session Layer: Manage and Control signals between computers
Presentation Layer: transform layers into application layer format


Hub, Switch & Router ?
Hub: Broadcast all data to every port, common connection point to all devices
Switch: Create the dynamic connection, trace the requesting port
Router: device to forward data packets from source to destination


TCP/IP Model ?
TCP: Transmission Control Protocol
IP: Internet Protocol
How the data gets transmitted and routed from end to end communication.



HTTP ?
HyperText Transfer Protocol, Port: 80
This protocol is responsible for web application content


TCP & UDP ?
TCP: Transmission Control Protocol, TCP is connection-oriented protocol
UDP: User Datagram Protocol, UDP is connection less protocol


Firewall ?
Security System that protects your systems from unauthorized or cyber attack.
PAM, Security Group, Network Access Control Lists, Web Application Firewall etc..


DNS ?
Domain Name System
Map the internet address with the local name.


Proxy Server ?
Proxy Server basically prevents the attacks from any external or unauthorized user over to private network.


Classes of Network ?
Classes of IPV4 are of 5 types:
Class A: 0.0.0.0 to 127.255.255.255
Class B: 128.0.0.0 to 191.255.255.255
Class C: 192.0.0.0 to 223.255.255.255
Class D: 224.0.0.0 to 239.255.255.255
Class E: 240.0.0.0. To 247.255.255.255


NIC?
NIC: Network Interface Card
It’s an adapter needs to install on computer, with NIC only computer interact with network


Types of mode available in the network ?
Simplex
Half-Duplex
Full-Duplex


SLIP Protocol ?
Single Line Interface Protocol
Sending IP datagram over a network in a single line


Key Elements of Protocol ?
Syntax
Semantics
Timings

Decoder ?
A program converts the encrypted data into its actual format


Difference between Threat, Vulnerability & Risk:
Threat:
Serious damage to system networks/internet
Virus attack is viewed as a threat
Hackers attempt to make use of weak network
Vulnerability:
Weakness in computer network/device/equipment
Devices refers to routers/modems/wireless-access-points/switches etc
Every device has one or more vulnerabilities that need to measure and fixed before it hacks
Risk:
Attacks usually launched either though programs, scripts and take control over network to steal the data by unauthorized users or hackers
Attacks made on network devices such as access points, servers or desktop computers


DDos Attack ?
Distributed-Denial-Of-Service attack 
Continuous flooding of a Central Server with frequent data requests
Objective is to disrupt target system and business


Types of DDos attacks ?
Application attacks
Volume Based attacks
Protocol attacks


Ransomware ?
Variant of malicious software, also referred to as malware.
Involves encryption of the targets data and demand of a ransom for providing access.
Payments for such is generally demanded through cryptocurrency.


Phishing ?
Unethical process of sending fraudulent messages and communications, 
It shows the request is coming from a reputable source and tricks the user to disclose sensitive information.
Generally attacks through emails or other communications methods.


VPN ?
Virtual Private Network
Ensures encryption of connection from an endpoint to a network, generally over the internet.
VPN utilizes SSL or IPSec for authenticating communication between network and device.


Intrusion Prevention System ?
It’s a specifically tailored system for scanning network traffic to block attacks actively


@@@@@@@@@@@@@@@@@@@@@@@

Indiamart.com (1 hr)

Tools and tech, using in your project ?
Git, Jenkins, Ansible, Docker, Docker Swarm, Kibana, AWS Etc
	

Which tools used to connect the AWS Console ?
AWS Command Line Interface (AWS CLI), SDK, or AWS CloudFormation.
After it is created, the connection is in a pending state. 
You complete the process by using the console Setup pending connection option. 
The console prompts you to create an installation or use an existing installation for the connection. 
You then use the console to complete the handshake and move the connection to an available state by choosing Complete connection on the console.


Which tools used to connect the S3 Bucket in Cloud ?
Create an AWS Identity and Access Management (IAM) profile role that grants access to Amazon S3.
Attach the IAM instance profile to the instance.
Validate permissions on your S3 bucket.


How can you create an AMI through automation ?
AWS AMI creation Python code
GitHub Link: https://gist.github.com/ashokarun/04a226db39b453f5e640cf4e3f697569


How can you create an AMI through automation ?
https://www.edureka.co/community/56521/how-to-create-ami-from-running-instance-using-ansible
Solution:
---
- hosts: localhost
  connection: local
  become: yes
  gather_facts: no
  vars:
    region: us-east-1
    ins_name: Sample
    ami_name: Sample
  tasks:
    - name: To Get Instance Id
      command: "aws ec2 describe-instances
                --filters Name=tag:Name,Values={{ ins_name }}
                --query 'Reservations[0].Instances[0].InstanceId'
                --output text"
      register: instanceid

    - name: To Create AMI
      ec2_ami:
	  

How many types of ELBs present in AWS and what is the difference between them ?
Elastic Load Balancing supports three types of load balancers:
Application Load Balancer,
Network Load Balancer and
Classic Load Balancers

Classic Load Balancer
basic load balancing across multiple EC2 instances
built within the EC2-Classic network.
simple load balancing of traffic across multiple EC2 instances.

Application Load Balancer
for microservices or container-based architectures 
need to route traffic to multiple services or load balance across multiple ports on the same EC2
operates at the request level (layer 7), 
advanced load balancing of HTTP and HTTPS traffic, 
and provides advanced request routing targeted at delivery of modern application architectures, 
including microservices and container-based applications.
simplifies and improves the security of the application, 
by ensuring that the latest SSL/TLS ciphers and protocols are used at all times.

Network Load Balancer
operates at the connection level (Layer 4), 
routing connections to targets – EC2 instances, microservices, and containers – within VPC based on IP protocol data.
ideal for load balancing of both TCP and UDP traffic,
is capable of handling millions of requests per second while maintaining ultra-low latencies.
is optimized to handle sudden and volatile traffic patterns while using a single static IP address per AZ
is integrated with other popular AWS services such as Auto Scaling, ECS, CloudFormation and AWS Certificate Manager (ACM).

Note: 
AWS recommends using Application Load Balancer for Layer 7 and Network Load Balancer for Layer 4 when using VPC.

https://jayendrapatil.com/tag/elb-vs-alb-vs-nlb/


How can restrict to IAM User to delete the S3 bucket but able to view and create in S3 ?
Follow the principle of least privilege. 
Restrict access to your S3 buckets or objects by: 
Writing AWS Identity and Access Management (IAM) user policies that specify the users that can access specific buckets and objects. 
IAM policies provide a programmatic way to manage Amazon S3 permissions for multiple users


How can I grant a user Amazon S3 console access to only a certain bucket?
Open the IAM console.
From the console, open the IAM user or role that should have access to only a certain bucket.
In the Permissions tab of the IAM user or role, expand each policy to view its JSON policy document.


How can you play with different regions of S3 bucket ?
Step 1: Creating multiple Buckets in S3
Step 2: Creating an IAM User and Define Roles 
Step 3: Configuring the Bucket Policy in S3 
Step 4: Initializing Cross Region Replication in S3
https://hevodata.com/learn/setting-up-s3-cross-region-replication/
https://medium.com/swlh/setting-up-a-s3-bucket-with-cross-region-replication-6516690501cc


AWS Complete Videos:
https://www.youtube.com/channel/UC6NHkcszEZXqQsu4F08C7lw/videos


AWS Lambda: 
Once you create Lambda functions, you can configure them to respond to events from variety of resources.
Try sending a mobile notifications, streaming data to lambda, or placing a photo in S3 bucket.
How to create a Lambda Function:
Create a functions
Use a blueprint
Search: hello-world-python
Click on configure: Populate all the required fields
Function Name: hello-world
Execution Role: Create a new role with basic lambda permissions
Cross verify the lambda function code
Click on "Create Function"
Create an Event and Test multiple times 
Lambda Function Link with Cloud Watch Logs
Click on "Manage these permissions" and play
UT: https://www.youtube.com/watch?v=seaBeltaKhw

UT: https://www.youtube.com/c/CloudYeti/search?query=cloud%20formation


git log
show all the commit history ?


git diff COMMIT_ID1 COMMIT_ID2
difference between two commit ids


git reset COMMIT_ID
reset all the previous changes


what is present at the top of "git log" ?
resent COMMIT_ID


Orchestration:
Orchestration and scheduling tools strive to eliminate silos, streamline processes and automate repetitive tasks so
that IT departments can move quickly and efficiently. While similar to automation, orchestration goes beyond the 
scope of automation by focusing on workflows or processes rather than simple tasks.
Complete DevOps CI and CD were called orchestration


What are backup and disaster recovery?
There’s an important distinction between backup and disaster recovery. 
Backup: is the process of making an extra copy (or multiple copies) of data. 
You back up data to protect it. You might need to restore backup data if you encounter an accidental deletion, 
database corruption, or problem with a software upgrade.
Disaster recovery: on the other hand, refers to the plan and processes for quickly reestablishing access to applications, 
data, and IT resources after an outage. That plan might involve switching over to a redundant set of servers and storage 
systems until your primary data center is functional again.


GoogleCloud Tutorials:
https://cloud.google.com/docs/tutorials/


Creating a VPC in AWS using Ansible:
https://www.infinitypp.com/ansible/create-vpc-ansible-aws/


Creating EC2 instance in AWS with CloudFormation
https://octopus.com/blog/aws-cloudformation-ec2-examples


What does an AMI Contains:
An Amazon Machine Image (AMI) is a template that contains:
software configuration (for example, an operating system, an application server, and applications). 
From an AMI, you launch an instance, which is a copy of the AMI running as a virtual server in the cloud.


CI/CD & DevOps:
https://octopus.com/blog/tag/DevOps


Can you copy the AMI between two different regions
YES
You can copy an Amazon Machine Image (AMI) within or across AWS Regions using the AWS Management Console, 
the AWS Command Line Interface or SDKs, or the Amazon EC2 API, all of which support the CopyImage action. 
You can copy both Amazon EBS-backed AMIs and instance-store-backed AMIs.


How to create a Random no ? 
import random; 
print(random.randint(0,9))


Have you ever done "SVN to GIT" migration and what are the Pre-Requisites ? 
Yes, we need branching details 


-------------------------------------------------------------------------------------------------------------------------------


Interview Question:9

JCPenny.com (45 min)


Updating your AWS Auto-Scaling AMI to a new version
Step 1: Create your new AMI. ...
Step 2: Test your AMI. ...
Step 3: Update the launch configuration to use the AMI. ...
Step 4: Update the Auto Scaling group.
Link: http://www.aschroder.com/2013/01/updating-your-aws-auto-scaling-ami-to-a-new-version/


Using a Makefile
Let’s say we have this Makefile that tracks the current version of our application


How version number is generated in Jenkins ?
It uses a tool called jx-release-version to figure out which is the next version to be released. 
In order to do that it checks what’s the currently released version in the repository looking at the released Git tags. 
It can also read this version from your pom.xml file, or your Makefile.
Link: https://blog.armesto.net/automatically-versioning-your-application-on-jenkins-x/


How Continuous Delivery is happening in your project ?
Though Git, Jenkins, Docker, Docker Swarm


How do you create VPC through CLI ??
Create a VPC with a 10.0. 0.0/16 CIDR block. aws ec2 create-vpc --cidr-block 10.0.0.0/16. ...
Using the VPC ID from the previous step, create a subnet with a 10.0. 1.0/24 CIDR block. ...
Create a second subnet in your VPC with a 10.0. 0.0/24 CIDR block.
Link: https://docs.aws.amazon.com/vpc/latest/userguide/vpc-subnets-commands-example.html


How to add the security groups in CF Template while creating a template for Stacks ?
Refer to "Cloud Formation Template"


What are the Pre-Requisite for CF Template while creating a Stacks ?
Cloudformation Template Contains 3 Main Things/Sections.
Parameters
Resources
Output
Parameter: As you are creating EC2 and you want to name your EC2 Server. 
So this parameter Section you will ask for input from the user who is executing this template.
Parameter:
 MyEC2Name:
  Description: "Enter the EC2 Name"	// Parameters
  Type: String

Resources: It is the section where you actually write code to create EC2
Resources:
 MyEC2:
 Type: AWS::EC2::Instance
 Properties:
  Tags:
    -Key: "Name"
     Value: !Ref MyEC2Name
     ....

Output: For example, you want to show something after the completion of your template. 
Maybe the Unique Id of EC2 or anything such as your name or any other info; you can pass it in Output Section
 Output:
  MyName:
  Value: "Bhavuk"
  
Link: https://stackoverflow.com/questions/66176837/what-are-the-prerequisites-for-cloudformation

  
  
List all the Security Level of AWS:

IAM: Identify & Access Mgmt 

KMS: Key Mgmt Service (H/W Security Modules)

ACM: AWS Certificate Manager (Handles the complexity of creating, storing, and renewing public & private SSL/TLS X.509

WAF: Web Application Firewall (Protect web apps or APIs against common web exploits and bots that may affect availability, compromise security, or consume excessive resources 

INSPECTOR: Amazon Inspector (Automated Security assessment service that helps improve the security 
and compliance of applications deployed on AWS)



On Demand Instance: Pay for compute capacity by the hour, with no long term commitments or upfront payments 
Spot Instance: 90% discount compared to On Demand Prices 

@@@@@@@@@@@@@@@@@@@@@@@

Ansible_Docker_Python:

Ansible Roles:
An Ansible role is a set of tasks to configure a host to serve a certain purpose like configuring a service. 
Roles are defined using YAML files with a predefined directory structure. A role directory structure contains directories: defaults, vars, tasks, files, templates, meta, handlers.


Shell Script to list the name of files in a certain path ?
#!/bin/sh
for i in `ls -lar *.*`
do
echo $i
done


Algorithm to use in Elastic Load Balancer ?
Application Load Balancers applies listener rules and assigns the (HTTP/HTTPS) request to a target group. 
It selects a target from that target group using the round robin routing algorithm.
Network Load Balancers node that receives the connection, selects a target from its target group using a flow hash routing algorithm.
Classic Load Balancers uses a round robin routing algorithm for TCP listeners and least outstanding requests routing algorithm for HTTP and HTTPS listeners.


How Autoscaling is configured ?
Create Launch Configuration -> Choose AMI, InstanceType, Configure Details, Security Groups and KeyPair => Launch it
aws autoscaling create-launch-configuration --launch-configuration-name my-launch-config --placement-tenancy dedicated --image-id ...
aws autoscaling describe-launch-configurations --launch-configuration-names my-launch-config
aws autoscaling create-launch-configuration --launch-configuration-name classiclink-config --image-id ami_id --instance-type instance_type \
--classic-link-vpc-id vpc_id --classic-link-vpc-security-groups group_id
aws autoscaling update-auto-scaling-group --auto-scaling-group-name my-asg --launch-configuration-name classiclink-config


Read the whole Autoscaling Documentation ?


Have you ever Hosted any WebApplication in AWS or Normal
Yes Through Git-> Jenkins-> Docker-> Docker Swarm 


Algorithm used in Auto Scaling ?
autoscaler_task_interval 60000;
min_app_instances  1;
server_startup_delay 180000;
max_requests_per_second   5;
rounds_to_average       2;
alarming_upper_rate 0.7;
alarming_lower_rate 0.2;
scale_down_factor 0.25;


Which language comes in the output of Ansible
JSON


What is Port Forwarding and how it works ?
Port forwarding is the process of configuring a router to make a computer or other network device that is connected to it 
accessible to other computers and network devices from outside of the local network. 
Port forwarding uses an IP address plus port number to route network requests to specific.


How does DNS resolution work ?
https://www.rosehosting.com/blog/what-is-dns-and-how-does-it-work/
1. The user enters the website’s domain in the address bar
2. The browser and OS check their local cache
3. The Resolver checks the local cache
4. The root server checks the local cache
5. The root server forwards the resolver to the TLD server
6. Receiving the answer


Ansible Roles Architecture ?

An Ansible role is a set of tasks to configure a host to serve a certain purpose like configuring a service. 
Roles are defined using YAML files with a predefined directory structure. 
A role directory structure contains directories: defaults, vars, tasks, files, templates, meta, handlers.
Link: https://medium.com/@mitesh_shamra/ansible-roles-1d1954f9932a#:~:text=Ansible%20role%20is%20a%20set,%2C%20templates%2C%20meta%2C%20handlers.



Ansible Roles

Ansible Architecture:

Ansible Best Tutorials: 
https://www.educba.com/ansible-architecture/

How Ansible Works:
Ansible works by connecting to your nodes and pushing out small programs, called "Ansible modules" to them. ... Ansible then executes these modules (over SSH by default), and removes them when finished. Your library of modules can reside on any machine, and there are no servers, daemons, or databases required.

Difference between SRE & DevOps:
SRE engineers are responsible for the stability of the production environment, 
but at the same time are committed to new features and operational improvement.
Google decided its SRE teams should be composed of 50 percent software engineers and 50 percent system administrators. 
such as Dropbox, Netflix and Github, are well-known for being at the forefront of technology leadership.

DevOps is a more recent movement, designed to help organizations’ IT departments move in agile and performant ways.
It builds a healthy working relationship between the Operations staff and Dev team, 
allowing each to see how their work influences and affects the other. 
By combining knowledge and effort, DevOps should produce a more robust, reliable, agile product.


While DevOps raise problems and dispatch them to Dev to solve, 
the SRE approach is to find problems and solve some of them themselves. 

While DevOps teams would usually choose the more conservative approach, leaving the production environment untouched unless absolutely necessary, 
SREs are more confident in their ability to maintain a stable production environment and push for rapid changes and software updates. 

Not unlike the DevOps team, SREs also thrive on a stable production environment, 
but one of the SRE team’s goals is to improve performance and operational efficiency.
Link: https://devops.com/sre-vs-devops-false-distinction/#:~:text=Both%20SRE%20and%20DevOps%20are,solve%20some%20of%20them%20themselves.


Jenkins Plugin used to deploy the war/ear file in tomcat web server:
"deploy to container" plugin


Have you ever worked on nginx Servers ?
No, I worked in Tomcat Servers in AWS


How to handle multiple yml playbooks ? 
include module


How to put condition in Ansible ?
Through “when” module


List of modules which you have worked on ?
Copy; handlers; with_items; yum; service, lineinfile etc


How to check Docker Container is up or down ?
$ docker ps -a
$ docker container status


List the Values in ascending order and keys in any order in Python ?
https://www.geeksforgeeks.org/python-sort-python-dictionaries-by-key-or-value/


Fetch the string from a list only without list comprehension ? 
a = [1,"one",2] => one


How does SNS work in AWS and how have you configured it in your Project ?
SNS attached with Application Server in 3-Tier Architecture, it is used for any notification 


What is the maximum number of nodes which you have configured in Ansible Playbook ?
5


Ansible or Puppet which one is better and why ?
I like Ansible because it is easy to write and manage; 
No Ansible installation required an agents; 
1,000s of modules present while writing playbooks 


Directory structure for Ansible ?
ansible.cfg
hosts
Roles


Have you created any Docker files on your own ?
Yes, I used FROM, RUN, CMD, ENTRYPOINT, SHELL, WORKDIR, LABEL, 


Which mandatory module you have to implement in REST Python API ?
https://realpython.com/api-integration-in-python/


Which module you need to implement to interact with the AWS Services or for AWS Automation ? 
boto or boto3


Structure for copy module in Ansible while copying multiple files from local to remote machine ?
Copy module, we need src and destination 
https://www.javatpoint.com/ansible-copy




Why and how have you implemented the Cloud Watch Monitoring ?
Manually implemented
https://www.youtube.com/watch?v=_Tqce6pGb44


Why do we use the handlers module in Ansible ?
Sometimes you want a task to run only when a change is made on a machine. For example, you may want to restart a service if a task updates the configuration of that service, but not if the configuration is unchanged. Ansible uses handlers to address this use case. Handlers are tasks that only run when notified.
https://docs.ansible.com/ansible/latest/user_guide/playbooks_handlers.html#:~:text=Sometimes%20you%20want%20a%20task,that%20only%20run%20when%20notified.



What is the data type for class in Python ?
List
Tuple 
String
Set &
Dictionary 
Int, float & complex classes in Python


Have you worked on Ansible with Docker ?
Yes, while implementing pipeline through Jenkins


Command to install Docker in OS ? 
Mac => sudo easy_install docker 
Prerequisites to install Docker => Python would be must


Difference between List and Tuple ?
List is Mutable whereas
Tuple is ImMutable
https://www.javatpoint.com/python-list-vs-tuple


Where have you used list and tuple in your project ?
While implementing jenkins pipeline I have written a Python code



How to fetch the unique elements in Python ? 
Set
https://www.javatpoint.com/python-set


Is string is mutable to immutable ? 
immutable 
https://stackoverflow.com/questions/9097994/arent-python-strings-immutable-then-why-does-a-b-work


In Dictionary, will the data be printed the way you insert ?
Yes


Which Algorithm used at the backend of Dictionary in Python ?
Key Value Pair
May be Round Robin Algorithm 


How Elastic Search work and where you have used ? => Kibana


List comprehension in Python and give me the type of string ?
>>> squares = [x**2 for x in range(10)]
>>> [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]


How iterator works in Python ?
To iterate elements one by one
>>> x = iter([1, 2, 3])
>>> x
<listiterator object at 0x1004ca850>
>>> next(x)
1
>>> next(x)
2
>>> next(x)
3
>>> next(x)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration


What is SLA and in which algorithm it worked at the backend ?
Service Level Agreement 

Have you ever created any certificate ?
Yes, openssl command
https://www.digicert.com/csr-creation-ssl-installation-mac-osx-el-capitan.htm


What is the demerits and merits while creating a certificate by our own ?


What is ca-certificates  and in which Algorithm it worked ?


Have you worked in hadoop ??
No

Are you good in SQL Queries ?
Yes

How Ansible worked, let me know its Architecture ?
Yes,
Ansible.cfg: Configuration file
Hosts: Default Inventory file
Roles: To configure a service, directory structure ( tasks, handlers, meta, etc)


What sequence followed by Ansible while executing the playbook ?
Syntax Check


Have you ever worked on Dynamic Playbook ?
No


Have you ever worked on Dynamic Docker File ?
No


@@@@@@@@@@@@@@@@@@@@@@@

HDFC Mumbai:

What is the difference between Classic Load Balancer and Application Load Balancer ?


Difference between Health check and Cool down in Auto Scaling ?
Cool Down Period: when AS don’t create or terminate any instances…..
https://stackoverflow.com/questions/55442279/difference-between-auto-scaling-cooldown-period-and-health-check-grace-period


How you can configure the Zero down time in Jenkins?
Great To Learn
Plugins:
JOB DSL Plugin; 
Email Extension Plugin; 
Docker Plugin; 
Script Security Plugin; 
Workspace Cleanup; 
GitHub Plugin
https://pchaturvedi19989.medium.com/continuous-deployment-of-a-webserver-with-zero-downtime-using-jenkins-kubernetes-and-docker-with-14afd5e87186


Parameters required in JSON Template ?
Parameters
Resources 
Output

In docker where do you run your container ?
In server and push the image into docker hub for backup & latest 

How to see the logs in Docker ?
$ docker logs

How to troubleshoot if one container fails to work ?
$ docker inspect <id>

@@@@@@@@@@@@@@@@@@@@@@@

Questions:

Is string is mutable to immutable ? mutable
In Dictionary, will the data will print the way you insert ? Need to verify
Which Algorithm used at the backend of Dictionary in Python ? Hashmap Techniques
How Elastic Search work and where you have used ? => Kibana and Splunk i have used
List comprehension in Python and give me the type of string ?
A = [ print(i) for i in range(10) ]
Print(A)
How iterator works in Python ? Iterator used to iterate the array elements
# define a list
my_list = [4, 7, 0, 3]
# get an iterator using iter()
my_iter = iter(my_list)
## iterate through it using next()
#prints 4
print(next(my_iter))
#prints 7
print(next(my_iter))
## next(obj) is same as obj.__next__()
#prints 0
print(my_iter.__next__())
#prints 3
print(my_iter.__next__())
## This will raise error, no items left
next(my_iter)


What is SLA ?
A service-level agreement (SLA) is a document describing the level of service expected by a customer from a supplier, laying out the metrics by which that service is ... However, it's recommended that the client and the outsourcing company work together during the SLA contract negotiation to eliminate any ...


Which algorithm worked at the backend of SLA ?
Interleaved Polling Algorithm


Have you ever created any certificate ? 
Yes, through openssl command
The commands below can be used to view the certificate fingerprint/thumbprint.
• SHA-256: openssl x509 -noout -fingerprint -sha256 -inform pem -in [certificate-file.crt]
• SHA-1: openssl x509 -noout -fingerprint -sha1 -inform pem -in [certificate-file.crt]
• MD5: openssl x509 -noout -fingerprint -md5 -inform pem -in [certificate-file.crt]

What are the demerits and merits while creating a certificate of our own ?

Advantages
1. No PKI (Public Key Infrastructure) is needed.
2. Automatic deployment (Usually Self-signed certificates created automatic during the installation process of the server side applications).

Disadvantages
1. The certificates aren’t trusted by other applications/operating systems. This may lead to authentications errors etc.
Note: To overcome this limitation, some IT staff add the self-signed certificates to the Trusted Roots Certificate Authorities. However, using this workaround may to additional time that needed for management and troubleshooting.
2. Self-signed certificates life time is usually 1 years. Before the year is ended, the certificate may need to renew/replace.
3. Self-signed certificates may use low hash and cipher technologies. Due this, the security level that implemented by self-signed certificates may not satisfy the current Security Policy etc. .
4. No support for advanced PKI (Public Key Infrastructure) functions (e.g. Online checking of the revocation list etc.).
5. Most of the advanced feathers of the server side applications required to impended a PKI (Public Key Infrastructure). By this, self-signed certificates advantages can't be used.
What is ca-certificates  and in which Algorithm it worked ?
CA certificates can also be used to establish trust relationships between CAs in two different public key infrastructure (PKI) hierarchies.
Root CA Certificate
 Issuing CA Certificate
  User Certificate
The following are some of the trust scenarios that can be enabled by properly configured CA certificates:
 • Simple trust within an enterprise PKI
 • Cross trust between two enterprise CAs (restricted)
 • Bridge trust for multiple enterprise PKIs (unrestricted)
 • Certificate trust continuity when the certificate policy changes


Have you worked in hadoop and Are you good at SQL Queries ? 
Yes


How Ansible worked, let me know its Architecture ?




What sequence followed by Ansible while executing the playbook ?
INVENTORY (LIST OF ALL WEB SERVERS), PLAYBOOK (MENTION ALL INVENTORIES) -> THROUGH SSH IT CONNECTS WITH REMOTE NODES AND DO THE DEPLOYMENT


Have you ever worked on Dynamic Playbook ?


Have you ever worked on Dynamic Docker File ?


Installation of Ansible ?
Install packages below on server machines
$ sudo apt-get install python-yaml python-jinja2 python-paramiko python-crypto python-keyczar ansible
Install packages below on client machines
$ sudo apt-get install python-crypto python-keyczar


How to read the last word of a file ?
awk 'NF {print $NF; exit}'
OR

# Python Code to read the first and last word of a file
f = open("file_name.ext","r")
for line in f:
 words = line.split()
 print(words[-1])
OR

f = open("file_name.ext","r") # open the file in read mode only
line = []  # create an empty list to store the lines of a file
for i in f:
 line.append(i)  # loop over the line in the file and store them in the list
for i in line:
 words_in_line=i.split()  # creates a list of the words in each line
 print(words_in_line[0],words_in_line[-1])  # print out the first and last word of each line

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Panda Module: Machine Learning
Three Data Structures:
Series; Data Frame; Panel
Ex_1:
import pandas as pd
import quandl
df = quandl.get('WIKI/GOOGLE')
print(df.head)
Note:
Series: 1D (Homogeneous data; Size Immutable; Data Mutable)
Data Frame: 2D (Heterogeneous data; Size Mutable; Data Mutable)
Panel: 3D (Heterogeneous data; Size Mutable; Data Mutable)
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Where do we implement Auto Scaling “Instance Level or ELB Level” ?
Instance level


What kind of Ansible Playbook you wrote ?
Monitoring Tool Kibana Implementation
Other Configuration as per the requirement


Rename all files contents as "xyz" using Shell Scripting ?
https://stackoverflow.com/questions/4488670/how-to-rename-all-file-name-which-contain-specific-word-to-another-word-in-a-fol/4488835
To rename files:
for fname in *_XYZ; 
do newname=`echo "$fname" | sed 's/_XYZ/_ABC/g'` 
echo "$fname" "$newname" 
done
After testing replace echo $fname... to mv $fname....
To rename tiles and replace files content:
for fname in *_XYZ; 
	do newname=`echo “$fname” | sed ‘s/_XYZ/_ABC/g’`
	Sed ‘s/XYZ/ABC/g’ “$fname” > “$newname” 
done



What kind of automations have you done in Python ?
https://www.activestate.com/blog/top-10-tasks-to-automate-with-python/#:~:text=The%20tasks%20you%20can%20automate,online%20forms%2C%20and%20much%20more.
https://github.com/vincepower/python-scripts
https://www.pythonforbeginners.com/code-snippets-source-code/google-command-line-script


Difference between Git and SVN ?


What does it indicate when the checkout happened and meanwhile a new file would be created in SVN ?


Why did we use JSON ?


--------------------------------------------------------------------------------------------

NetCracker: 05/07/2021

Recent Issue faced and how did you fixed it ?


Shell Scripting to Ping and Test all IP present in /etc/hosts file ?
https://unix.stackexchange.com/questions/450734/i-need-to-ping-a-list-of-ip-addresses-from-a-file-and-log-the-status-as-up-or
f=open("/etc/hosts","r"):
for line in f:
ping -c 1 "output" >> /dev/null
if [$? -eq 0 ]; then 
echo "IP is UP"
else echo "IP is down"
fi
done


How to see the memory in Linux ?


How to see if the port is enabled or not ?


How to see the space in Linux ?


What does this say: sed -i 's/\\/\//g' some.txt
\\ to \/ replace by it to all inside the file 


Reg Ex: How to search the digits ?
[0-9]


Reg Ex: How to search the alphabets ?
[a-z][A-Z]


How to see the remote port ?
iptables
ufw
netstat -ntlp



Difference between traceroute and tcproute ?
https://linux.die.net/man/1/tcptraceroute
tcproute
traceroute


How to download files in Python ?
https://stackabuse.com/download-files-with-python/
urllib module

SQL to count the no of people from USA ?
https://dba.stackexchange.com/questions/148657/select-countries-and-counts-of-people-per-country
"table: employees
|country|department|quantity|
|India|QA|100|
|India|IT|30|
|India|HR|5|
|USA|QA|50|
|USA|IT|10|"
select usa.country as user_count from country usa


Git Life Cycle whenever some change happened ?
Some file changes how you can add in git ?
git status
git add .
git status
git commit -m "COMMENTS"
git branch 
git push origin <branch_name>
git fetch & git pull


Explain the below Ansible Plybook ?
- name: Playbook
    hosts: webservers
    become: yes
    tasks:
      - name: task1
        yum:
          name: httpd
          state: latest
      - name: task2
        service:
          name: httpd
          state: started


What are Ansible Forks ?


What is Jenkins' file ?


How Master and Slave works and info do you have in Jenkins ?


What is stored in /etc/hosts file 


Ansible Forks ?
Ansible behaves when 100 nodes are present in Inventory ?
Recent Ansible Playbook you have written and explain ?


Difference between git fetch and git pull ?

No Exposure in Kubernetes ?

No Exposure in Prometeus ?


What exactly you are monitoring through Kibana tool ?


How can give priority inside Ansible Playbook ?




######

What happens when /boot or /root volume shows 100% ?


Can we release cache memory and how ?
sync; echo 3 > /proc/sys/vm/drop_caches


Difference between jar war and ear files in java ?
In J2EE application, modules are packaged as EAR, JAR and WAR based on their functionality
JAR: EJB modules which contain enterprise java beans (class files) and EJB deployment descriptor are packed as JAR files with .jar extenstion
WAR: Web modules which contain Servlet class files, JSP Files, supporting files, GIF and HTML files are packaged as JAR file with .war (web archive) extension
EAR: All above files (.jar and .war) are packaged as JAR file with .ear (enterprise archive) extension and deployed into Application Server.


How to create a 0 downtime deploy manually using Jenkins ?


Difference between .rb and .erb ?
erb is the extension of the template engine used to interpret the file. ... erb is the file extension for eRuby documents, which is a way of embedding Ruby into a text document. Similar to how PHP works. rb is the file extension for ruby
Ansible Vault ?
ansible-playbook site.yml --ask-vault-pass
From <http://docs.ansible.com/ansible/latest/playbooks_vault.html>
ansible-playbook site.yml --vault-password-file ~/.vault_pass.txt
ansible-playbook site.yml --vault-password-file ~/.vault_pass.py


How to list the variables in Ansible ?


How to fetch the environment variables in Ansible ?


Difference between Ansible and Chef ?


How Ansible used for Provisioning ?


How Multithreading inherited in Python ?


Key features of Python ?


How Auto Scaling works in AWS ?


What you have implemented in AWS Lambda ?
Yes, a small function 


Which is most recent script you worked upon ?
PowerShell 

Git stash command ?
To push a new stash onto your stack, run the git stash command. Now, your working directory is clean and all the changes are saved on a stack. Let us verify it with the git status command. Now you can safely switch the branch and work elsewhere.

Git list the commit changes  ?


Git revert the changes ?


Git difference command ?


Difference between Git and SVN ?


Difference between Pull and Push in GIT ?


@@@@@@@@@@@@@@@@@@@@@@@

Interview Questions:

Quantify Research:

JSON Template how to restrict the user to create and deny the Buckets ?


JSON Template how to stop and start the instances in Stack ?


How many types of S3 ?


How you can Automate the backups from S3 to Glacier ?


JSON Template to create two instances with password less ?


Suppose developers commit the code in GIT and with Jenkins how you can deploy the code in 7 Production Server ?


Difference between Lists and Tuple ?


Which one is fast accessing List or Tuple ?


Which modules of Python you have worked ?


@@@@@@@@@@@@@@@@@@@@@@@

Apple 🍎 DevOps:

Key Qualifications
5+ YEARS VALIDATED EXPERIENCE IN DEVOPS
Authoritative knowledge and experience with software version control systems: SVN, GIT (GitHub/Gitlab), etc
Knowledge of Java build systems and tools including: Gradle, Maven, Ant, SBT, etc.
HANDS-ON IN SCRIPTING LANGUAGES, JAVA AND RDBMS (ORACLE/MYSQL) SKILLS
Working knowledge of containerisation (Docker), and supporting technologies
Experience with Orchestration tools like Kubernetes, Swarm, Mesos
KNOWLEDGE OF VIRTUALISATION TECHNOLOGIES LIKE VMWARE ESXI, VAGRANT, KVM
Knowledge of webServers and load Balancers Apache HTTP Server, Apache Traffic Server, NGINX, Proxy
Experience working with server clusters consisting of 100s-1000s of machines, and deploying changing with zero downtime
EXPERIENCE MAINTAINING AUTOMATED BUILD SYSTEMS SUCH AS JENKINS, BAMBOO
A desire to write tools and applications to automate work rather than do things manually
Familiarity with Splunk for investigating or monitoring problems on systems.
Experience maintaining large clusters using configuration tools such as: Ansible, Puppet, Chef, Salt
UNIX and Linux system administration experience: ssh, monitoring processes, attaching storage, cleaning disk space, tailing logs, etc.
Experience implementing Continuous Integration and Delivery processes in large engineering teams
Ability to use and create web applications using REST, JSON, or similar protocols.
Experience in test frameworks such as JUnit, TestNG and integrating test automation into Devops pipeline
Knowledge of Java code coverage Tools: Jacoco, Sonar, or Clover
Experience implementing Java server applications using tools such as: Jersey, Jetty, ZooKeeper, JDBC, using cloud deployment tools

@@@@@@@@@@@@@@@@@@@@@@@

Interview epam

#reverse the string 
a = “how are you”
b = a.split()
b = ‘ ‘.join(reversed(b)
print(b)

# git rebase/merge
git init
Git branch	# QA
Git checkout -b devops	# created a new branch devops
touch x
Git commit -m “added one empty file”
Git stash		# to save your local changes
Git checkout QA	# switched to QA without commit
Git status
Git checkout devops
Git merge QA
Git push origin devops

# git stash		# described above

# Difference between run and cmd in Dockerfile ?
RUN: to execute the normal linux command
CMD: it actually execute once container start
RUN instruction actually runs the command and commits it, whereas the CMD instructions is not executed during build time.


How the request travels when you hit the browser ??
https://stackoverflow.com/questions/2092527/what-happens-when-you-type-in-a-url-in-browser


@@@@@@@@@@@@@@@@@@@@@@@

Interview Gaian:

DNS Error while browsing the application hosted in AWS ?

How to copy one content from one containerisation to another containerisation in Docker ?
Ansible or any configuration management tool 

To maintain high availability for incoming external connections on a single IP (e.g. a website),  I assume you need to use a load balancer that points to all of the worker and manager IP addresses. Is that right? What happens in the case of a leader going down? 
I read somewhere that it uses “Raft consensus” to elect a new leader. Is this also right?﻿

Yes,Raft consensus is used.If the leader fails then manual intervention would be required to remove the leader, and the remaining nodes would be restarted in “bootstrap” mode. 

@@@@@@@@@@@@@@@@@@@@@@@

Microsoft:

Tell me ur practical stuff

Find the median of two unsorted array

Find the second largest No from an array

Draw the architecture which consists of one DB, Front end apps and Back end apps

Need to work on Azure customer tickets

Suppose your site is responding bit late then how you will troubleshoot ??
https://www.dreamhost.com/blog/how-to-fix-slow-website/
Render-Blocking JS is delaying page loads
There are three solutions for dealing with render-blocking JavaScript:
Remove external JavaScript files, and use inline JavaScript instead.
Use asynchronous loading so JavaScript can load separately from the rest of the page.
Defer JavaScript loading until the rest of the page is visible to the user.
Not using CDN: Content Delivery Network
Excessive overhead in Database
Your site CSS isn’t optimised 
OPcache is not enabled
Cache issues are preventing optimised page loading
Large Media files are increasing loading times
Poorly written scripts are conflicting with other site elements
Your sites code is too bulky
Missing files are causing errors
Plugins are weighing your site down
Internet users are hurting specific user performance


You are unable to login to any server then what the possible steps you will take and how you will cross verify ??

I faced these 2 questions many times in interview.I know few of the reasons.

1) what can be the reasons if I'm unable to connect to a server remotely?
ANS.There could be many reason that you may not be able to take remote connection to server.
1.It could be that sufficient Permission are not give to have access to the server remotely.
2If the permission are given then it could be connectivity issue,firewall blocking the required.
3.It Could be due to Group policy to deny the remote connection and many more....

2)User is unable to login to domain- what could be the reasons?
ANS.There could be many reasons as below.
1.Connectivity issue with DC due to dns misconfig.
2.Account lockout or in disable state.
3.DC unreachable due physical connectivity issue.
4.Domain PC secure channel  broken with DC.
5.Cleint PC n/w cable unplugged
6.User account deleted from AD and many more...

@@@@@@@@@@@@@@@@@@@@@@@

Pro Karma:

Suppose two stacks among 10 fails in production, what would be your root cause analysis ?

How to create instances in different AZs ?
Ans: 
During instance creation I will the different AZs

—————————————————————

Troubleshoot if SSH will not work ?
Issues:
Hostname resolution
Connection timeout
Connection refused
Solution:

Check the firewall	
	$ iptables -nL
	$ firewall-cmd —list-services
	$ dhcpv6-client http ssh
	$ ufw status

Checking the ssh service status
	$ service ssh status
	$ ssh start/running, PID x
	$ ssh stop/waiting
	$ systemctl status sshd 

Checking the ssh service port
	$ grep Port /etc/ssh/sshd_config
	$ netstat -ntlp
	$ ss -ntlp
—————————————————————
			
When you hit www.prokarma.com tell me the end to end flow how request traverse and fetches the result ?
Attention: this is an extremely rough and oversimplified sketch, assuming the simplest possible HTTP request (no HTTPS, no HTTP2, no extras), simplest possible DNS, no proxies, single-stack IPv4, one HTTP request only, a simple HTTP server on the other end, and no problems in any step. This is, for most contemporary intents and purposes, an unrealistic scenario; all of these are far more complex in actual use, and the tech stack has become an order of magnitude more complicated since this was written. With this in mind, the following timeline is still somewhat valid:
	1.	browser checks cache; if requested object is in cache and is fresh, skip to #9
	2.	browser asks OS for server's IP address
	3.	OS makes a DNS lookup and replies the IP address to the browser
	4.	browser opens a TCP connection to server (this step is much more complex with HTTPS)
	5.	browser sends the HTTP request through TCP connection
	6.	browser receives HTTP response and may close the TCP connection, or reuse it for another request
	7.	browser checks if the response is a redirect or a conditional response (3xx result status codes), authorization request (401), error (4xx and 5xx), etc.; these are handled differently from normal responses (2xx)
	8.	if cacheable, response is stored in cache
	9.	browser decodes response (e.g. if it's gzipped)
	10.	browser determines what to do with response (e.g. is it a HTML page, is it an image, is it a sound clip?)
	11.	browser renders response, or offers a download dialog for unrecognized types
Again, discussion of each of these points have filled countless pages; take this only as a summary, abridged for the sake of clarity. Also, there are many other things happening in parallel to this (processing typed-in address, speculative prefetching, adding page to browser history, displaying progress to user, notifying plugins and extensions, rendering the page while it's downloading, pipelining, connection tracking for keep-alive, cookie management, checking for malicious content etc.) - and the whole operation gets an order of magnitude more complex with HTTPS (certificates and ciphers and pinning, oh my!).

—————————————————————

Git stash ?
Solution:
git init
Git branch	# QA
Git checkout -b devops	# created a new branch devops
touch x
Git commit -m “added one empty file”
Git stash		# to save your local changes
Git checkout QA	# switched to QA without commit
Git status
Git checkout devops
Git merge QA
Git push origin devops
—————————————————————

How to resolve the git conflicts ?
https://stackoverflow.com/questions/161813/how-to-resolve-merge-conflicts-in-git

$ git mergetool

—————————————————————

What is tag in Git ?
$ git tag -a v1.4 -m "my version 1.4"
$ git tag
v0.1
v1.3
v1.4

—————————————————————

How to configure the push concept in Ansible so to push the recent changes every after 30 mins to agent nodes ?
Solution:
- name: set hostname with file lookup
  ops_template:
    src: ./hostname.json
    backup: yes
    remote_user: admin
    become: yes

- name: set hostname with var
  ops_template:
    src: "{{ config }}"
    remote_user: admin
    become: yes

NOte: config module does all things
The OpenSwitch platform provides a library for pushing JSON structured configuration files into the current running-config. This module will read the current configuration from OpenSwitch and compare it against a provided candidate configuration. If there are changes, the candidate configuration is merged with the current configuration and pushed into OpenSwitch

—————————————————————

What exactly presents inside the SSL Certificate ?
Solutions:
Root Certificates and Chain Certificates

—————————————————————

What is Elastic Search in AWS ?
Amazon Elasticsearch Service (Amazon ES) is a managed service that makes it easy to deploy, operate, and scale Elasticsearch clusters in the AWS Cloud. Elasticsearch is a popular open-source search and analytics engine for use cases such as log analytics, real-time application monitoring, and clickstream analytics. With Amazon ES, you get direct access to the Elasticsearch APIs so that existing code and applications work seamlessly with the service.
Amazon ES provisions all the resources for your Elasticsearch cluster and launches the cluster. It also automatically detects and replaces failed Elasticsearch nodes, reducing the overhead associated with self-managed infrastructures. You can scale your cluster with a single API call or a few clicks in the console.
To get started using the service, you create an Amazon ES domain. An Amazon ES domain is an Elasticsearch cluster in the AWS Cloud that has the compute and storage resources that you specify. For example, you can specify the number of instances, instance types, and storage options.

Additionally, Amazon ES offers the following benefits of a managed service:
	•	Cluster scaling options
	•	Self-healing clusters
	•	Replication for data durability
	•	Enhanced security
	•	Node monitoring

—————————————————————

Write any Ansible playbook and explain ?
Solutions:
—
	⁃	Hosts: WEB
	⁃	Name: Copy the infinity files from host to windows machine
	⁃	win_get_url:
	⁃	Src: ftp://<username>:<password>@<ip>/x/y/z/<file_name>.txt
	⁃	Dest: C:\Desktop\ftp\<file_name>.txt

—————————————————————

What $? In shell Scripting ? 
Solution:
Current execution result which we generally used during script

—————————————————————

What is $$ in shell Scripting ?
Solution:
there is a script I evolved with it, it has line of command like below :
mytemp=`echo ${sourcedir}|awk -F/ '{printf "/%s/tmp",$2}'`/`basename $0`-$1.$$
at the last of the command we see $$ that produces a number. when I use echo $$ in bash I also see a number like bellow:
 #echo $$
 23019
$$ is the process ID of the current shell instance. So in your case the number, 23019, is the PID of that instance of bash.
The following should give you a better idea:
ps -p $$

—————————————————————

How do you rate yourself in python ?
2/5

—————————————————————

Suppose Artifactory servers where you taking the build backup filled then how you will manage ?
Solution:
Remove the old builds 

—————————————————————

Write a script to take the Jenkins build backup to Artifactory ?
Solution:
I will try to create a Jenkins Job and put under Poll SCM

Why access key and secret is required for AWS ??
To Login an Instance


Tell me the CLI command to create an instance and Snapshot creation ?
AWS EC2 create instance —instance-id <xxxx>


What is VPC and all components and how they are functioning ?
Virtual Private Cloud
Components are:
AZs; Region, IG, NAT Instance, NAT Gateway, Route Table, Router, DHCP, VPN, CG, Internet, VPC Peering, etc


Have you ever worked on Route53 ?
Yes, it is used to filter the Static & Dynamic incoming user requests


How many types of ELBs are and the differences ?
Classic Load Balancer: Old one handle simple LB
Network Load Balancer: Layer4, Can handle millions of requests per milliseconds, 
Application Load Balancer: Layer 7; Works on HTTP/HTTPS request; 

Similarities between SVN and GIT ?
Git is a distributed VCS; SVN is a non-distributed VCS. Git has a centralized server and repository; SVN does not have a centralized server or repository. The content in Git is stored as metadata; SVN stores files of content. ... Git does not have t

What is your recent script and in which language and what exactly it’s purpose ?
Powershell & Explain it


Why Docker is best ?


Difference between VPC and VPN ?


Have you configured VPN ?


What is the difference between NAT Instance and NAT Gateway ?


What exactly consists under SSL Certificate ?


What is One Click Deployment ? 
One click automation of a process of building image from Dockerfile, pushing it on DockerHub and immediately triggering a Jenkins deployment job based on the pushed Docker image.


Difference between Continuous Integration and Continuous Delivery ?

@@@@@@@@@@@@@@@@@@@@@@@

Interview Questions:

HCL Hyderabad

	1.	How to change the AMI in Cloud Formation Template without downtime ?

	2.	How to see the Roles and Policy attach to any instance manually ?

	3.	Can EC2 and RDS connect if they reside in two different availability zones and how  ? Ans: No

	4.	CLI to create an Instance ?

	5.	Automatically triggered the Jenkins Build Job ? Poll SCM

	6.	Difference between ALB and ELB ?

	7.	How can you deploy the code in Cloud Formation Stacks through Jenkins ?

	8.	How to configure Security Groups  in AWS ?

	9.	Describe the Architecture for a Single Web Application ?

	10.	Lambda support which language ? Java, Python, NodeJS

	11.	How you have designed S3 and what exactly it stores ?


How you have implemented HA Proxy ?
No

@@@@@@@@@@@@@@@@@@@@@@@

Pramati:

Explain VPC and it’s components ?

What is template, group_vars and roles in Ansible ?
https://www.skillpedia.co/ansible-tutorial-roles-tasks-and-templates/


How to use git stash ?

VPC peering ?

How you have configured HA Proxy ?

Tell me a small python script with boto3 ?

@@@@@@@@@@@@@@@@@@@@@@@

Innominds:

How will you troubleshoot if a container killed ?

How you will delete a file if an owner himself can’t delete the file with Saudi as well ?

Python script to delete the previous 3 Days builds ?

How hotfix handled in GIT ?

In Autoscaling during Configuration if max=20 servers & min= 1 serves provided but it unable to manage the requests then what plan you will going to propose ??

Why are you writing a Pipeline Groovy script ?

Have you written any python scripts and for what purpose ?

What are the parameters in cron Job ?

How you will schedule a job to execute after 80 mins with the help of cron Job ?

How you can protect your infrastructure in AWS ?

Where you have used Ansible ?

How comfortable are you in S3 ?

Difference between S3 and EBS ?

@@@@@@@@@@@@@@@@@@@@@@@

GOOGLE INTERVIEW QUESTIONS:

Install Anaconda for Mac: https://www.anaconda.com/download/#macos

	1.	FIRST RECURRING:

>>> def first_recurring(given_string):
...     counts = {}
...     for char in given_string:
...             if char in counts:
...                     return char
...             counts[char] = 1
... 
>>> first_recurring('ABCDA')
'A'
>>> 
>>> first_recurring('ABCBA')
'B'
>>> 

@@@@@@@@@@@@@@@@@@@@@@@

Verizon Media Hyderabad:

Have you written any CF Template from scratch ?

No

*********************************************************************************************

How to create an ec2 instance from Terraform ?

# Create a new instance of the latest Ubuntu 14.04 on an
# t2.micro node with an AWS Tag naming it "HelloWorld"
provider "aws" {
  region = "us-west-2"
}

data "aws_ami" "ubuntu" {
  most_recent = true

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-trusty-14.04-amd64-server-*"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  owners = ["099720109477"] # Canonical
}

resource "aws_instance" "web" {
  ami           = "${data.aws_ami.ubuntu.id}"
  instance_type = "t2.micro"

  tags = {
    Name = "HelloWorld"
  }
}

*********************************************************************************************

How do you troubleshoot if ec2 instance restarted automatically ?

grep -i error /var/log/syslog
/var/log/boot
/var/log/boot.log

*********************************************************************************************

Write an Ansible Playbook which does all three activities ?

Install packages like nginx: apt-package

https://code-maven.com/install-and-configure-nginx-using-ansible

	1.	---
	2.	- hosts: all
	3.	  tasks:
	4.	    - name: ensure nginx is at the latest version
	5.	      apt: name=nginx state=latest
	6.	    - name: start nginx
	7.	      service:
	8.	          name: nginx
	9.	          state: started


Copy some file from one machine to another: template module

- name: Copy file with owner and permissions
  copy:
    src: /srv/myfiles/foo.conf
    dest: /etc/foo.conf
    owner: foo
    group: foo
    mode: '0644'

- name: Copy file with owner and permission, using symbolic representation
  copy:
    src: /srv/myfiles/foo.conf
    dest: /etc/foo.conf
    owner: foo
    group: foo
    mode: u=rw,g=r,o=r

- name: Another symbolic mode example, adding some permissions and removing others
  copy:
    src: /srv/myfiles/foo.conf
    dest: /etc/foo.conf
    owner: foo
    group: foo
    mode: u+rw,g-wx,o-rwx

- name: Copy a new "ntp.conf file into place, backing up the original if it differs from the copied version
  copy:
    src: /mine/ntp.conf
    dest: /etc/ntp.conf
    owner: root
    group: root
    mode: '0644'
    backup: yes

- name: Copy a new "sudoers" file into place, after passing validation with visudo
  copy:
    src: /mine/sudoers
    dest: /etc/sudoers
    validate: /usr/sbin/visudo -csf %s

- name: Copy a "sudoers" file on the remote machine for editing
  copy:
    src: /etc/sudoers
    dest: /etc/sudoers.edit
    remote_src: yes
    validate: /usr/sbin/visudo -csf %s

- name: Copy using inline content
  copy:
    content: '# This file was moved to /etc/other.conf'
    dest: /etc/mine.conf

- name: If follow=yes, /path/to/file will be overwritten by contents of foo.conf
  copy:
    src: /etc/foo.conf
    dest: /path/to/link  # link to /path/to/file
    follow: yes

- name: If follow=no, /path/to/link will become a file and be overwritten by contents of foo.conf
  copy:
    src: /etc/foo.conf
    dest: /path/to/link  # link to /path/to/file
    follow: no

Restart the nginx services: use handler module

https://code-maven.com/reboot-with-ansible

*********************************************************************************************

df -hT: it shows 30 GB consuming but 15 GB is free still you were not trying to create any file, share the root cause ?

https://support.hpe.com/hpesc/public/docDisplay?docLocale=en_US&docId=emr_na-sg2465en_us

*********************************************************************************************

Ansible playbook to create an ec2 instance ?

- name: Launch the new EC2 Instance
      ec2:
        aws_access_key: "{{ aws_access_key }}"
        aws_secret_key: "{{ aws_secret_key }}"
        group: "{{ security_group }}"
        instance_type: "{{ instance_type }}"
        image: "{{ image }}"
        wait: true 
        region: "{{ region }}"
        keypair: "{{ keypair }}"
        count: "{{count}}"
      register: ec2

Ref:
https://www.linuxschoolonline.com/use-ansible-to-build-and-manage-aws-ec2-instances/

*********************************************************************************************

Have you ever created Auto Scaling ?

Yes through CLI: Command Line Interface

aws autoscaling create-auto-scaling-group --auto-scaling-group-name my-asg --launch-configuration-name my-launch-config --min-size 1 --max-size 3 --vpc-zone-identifier "subnet-5ea0c127,subnet-6194ea3b,subnet-c934b782"

Ref:
Manual Steps:
https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg.html

*********************************************************************************************

How to change the instance type or upgrade the instance type ?

Select the Instance
Click On Actions
Click On Instance State
Click On Stop

Select the Instance
Click On Actions
Instance Settings
Change Instance Type

Select the Instance
Click On Actions
Click On Instance State
Click On Start

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-resize.html

*********************************************************************************************

If it’s not coming up after change the instance type how you will troubleshoot ?

Here was an extra disk (/dev/xvdf) in the m3.xlarge instance that was not listed in the EC2 console (may be instance store?) although it was included in its /etc/fstab. When changing instance to r3.xlarge the volume disappeared but still was trying to mount it because of fstab... just commented fstab line and voilà.

Ref:
https://stackoverflow.com/questions/30894782/ec2-instance-wont-connect-after-changing-instance-type

*********************************************************************************************

How many serves managed by you in your existing project ?
 
13 DC Prod Servers
13 DC Non-Prod Servers

*********************************************************************************************



@@@@@@@@@@@@@@@@@@@@@@@

COMPLETE INTERVIEW:

How will you troubleshoot if a container killed ?

$ docker container logs <container-id>
$ docker inspect <container-id>
$ docker exec -it <container-id> /bin/sh 

*********************************************************************************************How you will delete a file if an owner himself can’t delete the file with sudo as well ?
Sol:
[root@ .montepio]# lsattr -dsu--ia-A----- .
[root@ images]# chattr -d -suSiadAc .montepio[root@ images]# cd .montepio/[root@ .montepio]# lsattr -d------------- .[root@ images]# rm -rf .montepio[root@ images]#
*********************************************************************************************
Python script to delete the previous 3 Days builds ?How hot fix handled in GIT ?In Auto scaling during Configuration if max=20 servers & min= 1 serves provided but it unable to manage the requests then what plan you will going to propose ??Why are you writing a Pipeline Groovy script ?Have you written any python scripts and for what purpose ?What are the parameters in cron Job ?How you will schedule a job to execute after 80 mins with the help of cron Job ?How you can protect your infrastructure in AWS ?Where you have used Ansible ?How comfortable are you in S3 ?Difference between S3 and EBS ?
Pramati:Explain VPC and it’s components ?What is template, group_vars and roles in Ansible ?How to use git stash ?VPC peering ?How you have configured HA Proxy ?Tell me a small python script with boto3 ?
Interview Questions:HCL Hyderabad1. How to change the AMI in Cloud Formation Template without downtime ?2. How to see the Roles and Policy attach to any instance manually ?3. Can EC2 and RDS connect if they reside in two different availability zones and how  ? Ans: No4. CLI to create an Instance ?5. Automatically triggered the Jenkins Build Job ? Poll SCM6. Difference between ALB and ELB ?7. How can you deploy the code in Cloud Formation Stacks through Jenkins ?8. How to configure Security Groups  in AWS ?9. Describe the Architecture for a Single Web Application ?10. Lambda support which language ? Java, Python, NodeJS11. How you have designed S3 and what exactly it stores ?12. How you have implemented HA Proxy ?
Pro Karma:Suppose two stacks among 10 fails in production, what would be your root cause analysis ?How to create instances in different AZs ?Ans: During instance creation I will the different AZs—————————————————————Troubleshoot if SSH will not work ?Issues:Hostname resolutionConnection timeoutConnection refusedSolution:Check the firewall		$ iptables -nL	$ firewall-cmd —list-services	$ dhcpv6-client http ssh	$ ufw statusChecking the ssh service status	$ service ssh status	$ ssh start/running, PID x	$ ssh stop/waiting	$ systemctl status sshd Checking the ssh service port	$ grep Port /etc/ssh/sshd_config	$ netstat -ntlp	$ ss -ntlp—————————————————————			When you hit www.prokarma.com tell me the end to end flow how request traverse and fetches the result ?Attention: this is an extremely rough and oversimplified sketch, assuming the simplest possible HTTP request (no HTTPS, no HTTP2, no extras), simplest possible DNS, no proxies, single-stack IPv4, one HTTP request only, a simple HTTP server on the other end, and no problems in any step. This is, for most contemporary intents and purposes, an unrealistic scenario; all of these are far more complex in actual use, and the tech stack has become an order of magnitude more complicated since this was written. With this in mind, the following timeline is still somewhat valid:1. browser checks cache; if requested object is in cache and is fresh, skip to #92. browser asks OS for server's IP address3. OS makes a DNS lookup and replies the IP address to the browser4. browser opens a TCP connection to server (this step is much more complex with HTTPS)5. browser sends the HTTP request through TCP connection6. browser receives HTTP response and may close the TCP connection, or reuse it for another request7. browser checks if the response is a redirect or a conditional response (3xx result status codes), authorization request (401), error (4xx and 5xx), etc.; these are handled differently from normal responses (2xx)8. if cacheable, response is stored in cache9. browser decodes response (e.g. if it's gzipped)10. browser determines what to do with response (e.g. is it a HTML page, is it an image, is it a sound clip?)11. browser renders response, or offers a download dialog for unrecognized typesAgain, discussion of each of these points have filled countless pages; take this only as a summary, abridged for the sake of clarity. Also, there are many other things happening in parallel to this (processing typed-in address, speculative prefetching, adding page to browser history, displaying progress to user, notifying plugins and extensions, rendering the page while it's downloading, pipelining, connection tracking for keep-alive, cookie management, checking for malicious content etc.) - and the whole operation gets an order of magnitude more complex with HTTPS (certificates and ciphers and pinning, oh my!).—————————————————————Git stash ?Solution:git initGit branch	# QAGit checkout -b devops	# created a new branch devopstouch xGit commit -m “added one empty file”Git stash		# to save your local changesGit checkout QA	# switched to QA without commitGit statusGit checkout devopsGit merge QAGit push origin devops—————————————————————How to resolve the git conflicts ?https://stackoverflow.com/questions/161813/how-to-resolve-merge-conflicts-in-git—————————————————————What is tag in Git ?$ git tag -a v1.4 -m "my version 1.4"$ git tagv0.1v1.3v1.4—————————————————————How to configure the push concept in Ansible so to push the recent changes every after 30 mins to agent nodes ?Solution:- name: set hostname with file lookup  ops_template:    src: ./hostname.json    backup: yes    remote_user: admin    become: yes- name: set hostname with var  ops_template:    src: "{{ config }}"    remote_user: admin    become: yesNOte: config module does all thingsThe OpenSwitch platform provides a library for pushing JSON structured configuration files into the current running-config. This module will read the current configuration from OpenSwitch and compare it against a provided candidate configuration. If there are changes, the candidate configuration is merged with the current configuration and pushed into OpenSwitch—————————————————————What exactly presents inside the SSL Certificate ?Solutions:Root Certificates and Chain Certificates—————————————————————What is Elastic Search in AWS ?Amazon Elasticsearch Service (Amazon ES) is a managed service that makes it easy to deploy, operate, and scale Elasticsearch clusters in the AWS Cloud. Elasticsearch is a popular open-source search and analytics engine for use cases such as log analytics, real-time application monitoring, and clickstream analytics. With Amazon ES, you get direct access to the Elasticsearch APIs so that existing code and applications work seamlessly with the service.Amazon ES provisions all the resources for your Elasticsearch cluster and launches the cluster. It also automatically detects and replaces failed Elasticsearch nodes, reducing the overhead associated with self-managed infrastructures. You can scale your cluster with a single API call or a few clicks in the console.To get started using the service, you create an Amazon ES domain. An Amazon ES domain is an Elasticsearch cluster in the AWS Cloud that has the compute and storage resources that you specify. For example, you can specify the number of instances, instance types, and storage options.Additionally, Amazon ES offers the following benefits of a managed service:* Cluster scaling options* Self-healing clusters* Replication for data durability* Enhanced security* Node monitoring—————————————————————Write any Ansible playbook and explain ?Solutions:—- Hosts: WEB- Name: Copy the infinity files from host to windows machine- win_get_url:    - Src: ftp://<username>:<password>@<ip>/x/y/z/<file_name>.txt    - Dest: C:\Desktop\ftp\<file_name>.txt—————————————————————What $? In shell Scripting ? Solution:Current execution result which we generally used during script—————————————————————What is $$ in shell Scripting ?Solution:there is a script I evolved with it, it has line of command like below :mytemp=`echo ${sourcedir}|awk -F/ '{printf "/%s/tmp",$2}'`/`basename $0`-$1.$$at the last of the command we see $$ that produces a number. when I use echo $$ in bash I also see a number like bellow: #echo $$ 23019$$ is the process ID of the current shell instance. So in your case the number, 23019, is the PID of that instance of bash.The following should give you a better idea:ps -p $$—————————————————————How do you rate yourself in python ?2/5—————————————————————Suppose Artifactory servers where you taking the build backup filled then how you will manage ?Solution:Remove the old builds —————————————————————Write a script to take the Jenkins build backup to Artifactory ?Solution:I will try to create a Jenkins Job and put under Poll SCM1. Why access key and secret is required for AWS ?2. 3. Tell me the CLI command to create an instance and Snapshot creation ?4. 5. What is VPC and all components and how they are functioning ?6. 7. Have you ever worked on Route53 ?8. 9. How many types of ELBs are there and the differences ?10. 11. 12. Similarities between SVN and GIT ?Git is a distributed VCS; SVN is a non-distributed VCS. Git has a centralized server and repository; SVN does not have a centralized server or repository. The content in Git is stored as metadata; SVN stores files of content. ... Git does not have t1. What is your recent script and in which language and what exactly it’s purpose ?2. 3. Why Docker is best ?4. 5. Difference between VPC and VPN ?6. 7. Have you configured VPN ?8. 9. What is the difference between NAT Instance and NAT Gateway ?10. 11. What exactly consists under SSL Certificate ?12. 13. What is One Click Deployment ? One click automation of a process of building image from Dockerfile, pushing it on DockerHub and immediately triggering a Jenkins deployment job based on the pushed Docker image.14. 15. Difference between Continuous Integration and Continuous Delivery ?
Microsoft:1. Tell me ur practical stuff2. Find the median of two unsorted array3. Find the second largest No from an array4. Draw the architecture which consists of one DB, Front end apps and Back end apps5. Need to work on Azure customer tickets6. Suppose your site is responding bit late then how you will troubleshoot ??7. You are unable to login to any server then what the possible steps you will take and how you will cross verify ??8. Profile mismatch 

Interview Gaian:DNS Error while browsing the application hosted in AWS ?How to copy one content from one containerisation to another containerisation in Docker ?Ansible or any configuration management tool To maintain high availability for incoming external connections on a single IP (e.g. a website),  I assume you need to use a load balancer that points to all of the worker and manager IP addresses. Is that right? What happens in the case of a leader going down? I read somewhere that it uses Raft consensus to elect a new leader. Is this also right?﻿Yes,Raft consensus is used.If the leader fails then manual intervention would be required to remove the leader, and the remaining nodes would be restarted in bootstrap mode. 

Interview epam#reverse the string a = “how are you”b = a.split()b = ‘ ‘.join(reversed(b)print(b)# git rebase/mergegit initGit branch	# QAGit checkout -b devops	# created a new branch devopstouch xGit commit -m “added one empty file”Git stash		# to save your local changesGit checkout QA	# switched to QA without commitGit statusGit checkout devopsGit merge QAGit push origin devops# git stash		# described above# Difference between run and cmd in Dockerfile ?RUN: to execute the normal linux commandCMD: it actually execute once container startRUN instruction actually runs the command and commits it, whereas the CMD instructions is not executed during build time.How the request travels when you hit the browser ??https://stackoverflow.com/questions/2092527/what-happens-when-you-type-in-a-url-in-browser
Interview Questions:Quantify Research:1. JSON Template how to restrict the user to create and deny the Buckets ?2. JSON Template how to stop and start the instances in Stack ?3. How many types of S3 ?4. How you can Automate the backups from S3 to Glacier ?5. JSON Template to create two instances with password less ?6. Suppose developers commit the code in GIT and with Jenkins how you can deploy the code in 7 Production Server ?7. Difference between Lists and Tuple ?8. Which one is fast accessing List or Tuple ?9. Which modules of Python you have worked ?
What is the data type for class in Python ?Have you worked on Ansible with Docker ? NoCommand to install Docker in OS ? Mac => sudo easy_install dockerPre-requisites to install Docker => Python would be mustDifference between List and Tuple ?List is Mutable and Tuple is ImmutableWhere have you used list and tuple in your project ?Useless questionHow to fetch the unique elements in Python ? => setIs string is a mutable to immutable ? mutableIn Dictionary, will the data will print the way you insert ? Need to verifyWhich Algorithm used at the backend of Dictionary in Python ? Hashmap TechniquesHow Elastic Search work and where you have used ? => Kibana and Splunk i have usedList comprehension in Python and give me the type of string ?A = [ print(i) for i in range(10) ]Print(A)How iterator works in Python ? Iterator used to iterate the array elements# define a listmy_list = [4, 7, 0, 3]# get an iterator using iter()my_iter = iter(my_list)## iterate through it using next()#prints 4print(next(my_iter))#prints 7print(next(my_iter))## next(obj) is same as obj.__next__()#prints 0print(my_iter.__next__())#prints 3print(my_iter.__next__())## This will raise error, no items leftnext(my_iter)What is SLA ?A service-level agreement (SLA) is a document describing the level of service expected by a customer from a supplier, laying out the metrics by which that service is ... However, it's recommended that the client and the outsourcing company work together during the SLA contract negotiation to eliminate any ...Which algorithm it worked at the backend of SLA ?Interleaved Polling AlgorithmHave you ever created any certificate ? Yes, through openssl commandThe commands below can be used to view the certificate fingerprint/thumbprint.• SHA-256: openssl x509 -noout -fingerprint -sha256 -inform pem -in [certificate-file.crt]• SHA-1: openssl x509 -noout -fingerprint -sha1 -inform pem -in [certificate-file.crt]• MD5: openssl x509 -noout -fingerprint -md5 -inform pem -in [certificate-file.crt]What is the demerits and merits while creating a certificate by our own ?Advantages1. No PKI (Public Key Infrastructure) is needed.2. Automatic deployment (Usually Self-signed certificates created automatic during the installation process of the server side applications).Disadvantages1. The certificates aren’t trusted by other applications/operating systems. This may lead to authentications errors etc.Note: To overcome this limitation, some IT staff add the self-signed certificates to the Trusted Roots Certificate Authorities. However, using this workaround may to additional time that needed for management and troubleshooting.2. Self-signed certificates life time is usually 1 years. Before the year is ended, the certificate may need to renew/replace.3. Self-signed certificates may use low hash and cipher technologies. Due this, the security level that implemented by self-signed certificates may not satisfy the current Security Policy etc. .4. No support for advanced PKI (Public Key Infrastructure) functions (e.g. Online checking of the revocation list etc.).5. Most of the advanced feathers of the server side applications required to impended a PKI (Public Key Infrastructure). By this, self-signed certificates advantages can't be used.What is ca-certificates  and in which Algorithm it worked ?CA certificates can also be used to establish trust relationships between CAs in two different public key infrastructure (PKI) hierarchies.Root CA Certificate Issuing CA Certificate  User CertificateThe following are some of the trust scenarios that can be enabled by properly configured CA certificates: • Simple trust within an enterprise PKI • Cross trust between two enterprise CAs (restricted) • Bridge trust for multiple enterprise PKIs (unrestricted) • Certificate trust continuity when the certificate policy changesHave you worked in hadoop and Are you good in SQL Queries ? No, and YesHow Ansible worked, let me know its Architecture ?What sequence followed by Ansible while executing the playbook ?INVENTORY (LIST OF ALL WEBSERVERS), PLAYBOOK (MENTION ALL INVENTORIES) -> THROUGH SSH IT CONNECTS WITH REMOTE NODES AND DO THE DEPLOYMENTHave you ever worked on Dynamic Playbook ?Have you ever worked on Dynamic Docker File ?Installation of Ansible ?Install packages below on server machines$ sudo apt-get install python-yaml python-jinja2 python-paramiko python-crypto python-keyczar ansibleInstall packages below on client machines$ sudo apt-get install python-crypto python-keyczarHow to read the last word of a file ?awk 'NF {print $NF; exit}'OR# Python Code to read the first and last word of a filef = open("file_name.ext","r")for line in f: words = line.split() print(words[-1])ORf = open("file_name.ext","r") # open the file in read mode onlyline = []  # create an empty list to store the lines of a filefor i in f: line.append(i)  # loop over the line in the file and store them in the listfor i in line: words_in_line=i.split()  # creates a list of the words in each line print(words_in_line[0],words_in_line[-1])  # print out the first and last word of each line----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------Panda: Machine LearningThree Data Structures:Series; Data Frame; PanelEx_1:import pandas as pdimport quandldf = quandl.get('WIKI/GOOGL')print(df.head)Note:Series: 1D (Homogeneous data; Size Immutable; Data Mutable)Data Frame: 2D (Heterogeneous data; Size Mutable; Data Mutable)Panel: 3D (Heterogeneous data; Size Mutable; Data Mutable)--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------Where we implement Auto Scaling Instance Level or ELB Level ?Instance levelWhat kind of Ansible Playbook you wrote ?Rename all files contents as "xyz" using Shell Scripting ?What kind of automations you have done in Python ?Difference between Git and SVN ?What it indicates when checkout happened and meanwhile a new file would created in SVN ?Why we used JSON ?What happened when /boot or /root volume shows 100% ?Can we release cache memory and how ?sync; echo 3 > /proc/sys/vm/drop_cachesDifference between jar war and ear files in java ?In J2EE application, modules are packaged as EAR, JAR and WAR based on their functionalityJAR: EJB modules which contain enterprise java beans (class files) and EJB deployment descriptor are packed as JAR files with .jar extenstionWAR: Web modules which contain Servlet class files, JSP Files, supporting files, GIF and HTML files are packaged as JAR file with .war (web archive) extensionEAR: All above files (.jar and .war) are packaged as JAR file with .ear (enterprise archive) extension and deployed into Application Server.How to create a 0 downtime deploy manually using Jenkins ?Difference between .rb and .erb ?erb is the extension of the template engine used to interpret the file. ... erb is the file extension for eRuby documents, which is a way of embedding Ruby into a text document. Similar to how PHP works. rb is the file extension for rubyAnsible Vault ?ansible-playbook site.yml --ask-vault-passFrom <http://docs.ansible.com/ansible/latest/playbooks_vault.html>ansible-playbook site.yml --vault-password-file ~/.vault_pass.txtansible-playbook site.yml --vault-password-file ~/.vault_pass.pyHow to list the variables in Ansible ?How to fetch the environment variables in Ansible ?Difference between Ansible and Chef ?How Ansible used for Provisioning ?Difference between List and Tuple ?How Multithreading inherited in Python ?Key features of Python ?How Auto Scaling works in AWS ?What you have implemented in AWS Lambda ?Which is most recent script you worked upon ?Git stash command ?Git list the commit changes  ?Git revert the changes ?Git difference command ?Difference between Git and SVN ?Difference between Pull and Push in GIT ?

Modak_Analytics:Shell Script to list the name of files in a certain path ?#!/bin/shfor i in `ls -lar *.*`doecho $idoneAlgorithm to use in Elastic Load Balanacer ?Application Load Balancers applies listener rules and assigns the (HTTP/HTTPS) request to a target group. It selects a target from that target group using the round robin routing algorithm.Network Load Balancers node that receives the connection, selects a target from its target group using a flow hash routing algorithm.Classic Load Balancers uses round robin routing algorithm for TCP listeners and least outstanding requests routing algorithm for HTTP and HTTPS listeners.How Autoscaling is configured ?Create Launch Configuration -> Choose AMI, InstanceType, Configure Details, Security Groups and KeyPair => Launch itaws autoscaling create-launch-configuration --launch-configuration-name my-launch-config --placement-tenancy dedicated --image-id ...aws autoscaling describe-launch-configurations --launch-configuration-names my-launch-configaws autoscaling create-launch-configuration --launch-configuration-name classiclink-config --image-id ami_id --instance-type instance_type \--classic-link-vpc-id vpc_id --classic-link-vpc-security-groups group_idaws autoscaling update-auto-scaling-group --auto-scaling-group-name my-asg --launch-configuration-name classiclink-configRead the whole Auto Scaling Documentation ?Have you ever Hosted any WebApplication in AWS or Normal ? => Through Docker onlyAlogorithm used in Auto Scaling ?autoscaler_task_interval 60000;min_app_instances  1;server_startup_delay 180000;max_requests_per_second   5;rounds_to_average       2;alarming_upper_rate 0.7;alarming_lower_rate 0.2;scale_down_factor 0.25;Which language comes in the output of Ansible ? => JSONWhat is Port Forwarding and how it works ?Port forwarding is the process of configuring a router to make a computer or other network device that is connected to it accessible to other computers and network devices from outside of the local network. Port forwarding uses an IP address plus port number to route network requests to specific.How DNS resolution work ?https://www.rosehosting.com/blog/what-is-dns-and-how-does-it-work/1. The user enters the website’s domain in the address bar2. The browser and OS check their local cache3. The Resolver checks the local cache4. The root server checks the local cache5. The root server forwards the resolver to the TLD server6. Receiving the answerAnsible Roles Architecture ?Have you ever worked on nginx Servers ?How to handle multiple yml playbooks ? include moduleHow to put condition in Ansible ?List of modules which you have worked ?How to check Docker Container is up or down ?List the Values in ascending order and keys in any order in Python ?Fetch the string from a list only without list comprehension ? a = [1,"one",2] => oneHow SNS work in AWS and how you have configured in your Project ?What is the maximum no of nodes which you have configured in Ansible Playbook ?Ansible or Puppet which one is better and why ?Directory structure for Roles in Ansible ?Have you created any Docker file by your own elaborate it ?Which madatory module you have to implement in REST Python API ?Which module you need to implement to interact the AWS Services or for AWS Automation ? boto or boto3Structure for copy module in Ansible while copying multiple files from local to remote machine ?Why and how you have implemented the Cloud Watch Monitoring ?Why we use handlers module in Ansible ?What is the data type for class in Python ?Have you worked on Ansible with Docker ?Command to install Docker in OS ? Mac => sudo easy_install docker Pre-requisites to install Docker => Python would be mustDifference between List and Tuple ?Where have you used list and tuple in your project ?How to fetch the unique elements in Python ? => setIs string is a mutable to immutable ? mutable In Dictionary, will the data will print the way you insert ?Which Alogorithm used at the backend of Dictionary in Python ?How Elastic Search work and where you have used ? => Kibana and Splunk i have used List comprehension in Python and give me the type of string ?How iterator works in Python ?What is SLA and in which algorithm it worked at the backend ?Have you ever created any certificate ? Yes, openssl commandWhat is the demerits and merits while creating a certificate by our own ?What is ca-certificates  and in which Algorithm it worked ?Have you worked in hadoop and Are you good in SQL Queries ?How Ansible worked, let me know its Architecture ?What sequence followed by Ansible while executing the playbook ?Have you ever worked on Dynamic Playbook ?Have you ever worked on Dynamic Docker File ?

HDFC Mumbai:What is the difference between Classic Load Balancer and Application Load Balancer ?Difference between Health check and Cool down in Auto Scaling ?How you can configure the Zero down time in Jenkins ?Parameters required in JSON Template ?In docker where do you run your container ?How to see the logs in Docker ?How to troubleshoot if one container fails to work ?


Ansible_Docker_Python:Shell Script to list the name of files in a certain path ?#!/bin/shfor i in `ls -lar *.*`doecho $idoneAlgorithm to use in Elastic Load Balanacer ?Application Load Balancers applies listener rules and assigns the (HTTP/HTTPS) request to a target group. It selects a target from that target group using the round robin routing algorithm.Network Load Balancers node that receives the connection, selects a target from its target group using a flow hash routing algorithm.Classic Load Balancers uses round robin routing algorithm for TCP listeners and least outstanding requests routing algorithm for HTTP and HTTPS listeners.How Autoscaling is configured ?Create Launch Configuration -> Choose AMI, InstanceType, Configure Details, Security Groups and KeyPair => Launch itaws autoscaling create-launch-configuration --launch-configuration-name my-launch-config --placement-tenancy dedicated --image-id ...aws autoscaling describe-launch-configurations --launch-configuration-names my-launch-configaws autoscaling create-launch-configuration --launch-configuration-name classiclink-config --image-id ami_id --instance-type instance_type \--classic-link-vpc-id vpc_id --classic-link-vpc-security-groups group_idaws autoscaling update-auto-scaling-group --auto-scaling-group-name my-asg --launch-configuration-name classiclink-configRead the whole Auto Scaling Documentation ?Have you ever Hosted any WebApplication in AWS or Normal ? => Through Docker onlyAlogorithm used in Auto Scaling ?autoscaler_task_interval 60000;min_app_instances  1;server_startup_delay 180000;max_requests_per_second   5;rounds_to_average       2;alarming_upper_rate 0.7;alarming_lower_rate 0.2;scale_down_factor 0.25;Which language comes in the output of Ansible ? => JSONWhat is Port Forwarding and how it works ?Port forwarding is the process of configuring a router to make a computer or other network device that is connected to it accessible to other computers and network devices from outside of the local network. Port forwarding uses an IP address plus port number to route network requests to specific.How DNS resolution work ?https://www.rosehosting.com/blog/what-is-dns-and-how-does-it-work/1. The user enters the website’s domain in the address bar2. The browser and OS check their local cache3. The Resolver checks the local cache4. The root server checks the local cache5. The root server forwards the resolver to the TLD server6. Receiving the answerAnsible Roles Architecture ?Have you ever worked on nginx Servers ?How to handle multiple yml playbooks ? include moduleHow to put condition in Ansible ?List of modules which you have worked ?How to check Docker Container is up or down ?List the Values in ascending order and keys in any order in Python ?Fetch the string from a list only without list comprehension ? a = [1,"one",2] => oneHow SNS work in AWS and how you have configured in your Project ?What is the maximum no of nodes which ou have configured in Ansible Playbook ?Ansible or Puppet which one is better and why ?Directory structure for Roles in Ansible ?Have you created any Docker file by your own elaborate it ?Which mandatory module you have to implement in REST Python API ?Which module you need to implement to interact the AWS Services or for AWS Automation ? boto or boto3Structure for copy module in Ansible while copying multiple files from local to remote machine ?Why and how you have implemented the Cloud Watch Monitoring ?Why we use handlers module in Ansible ?What is the data type for class in Python ?Have you worked on Ansible with Docker ?Command to install Docker in OS ? Mac => sudo easy_install docker Pre-requisites to install Docker => Python would be mustDifference between List and Tuple ?Where have you used list and tuple in your project ?How to fetch the unique elements in Python ? => setIs string is a mutable to immutable ? mutable In Dictionary, will the data will print the way you insert ?Which Algorithm used at the backend of Dictionary in Python ?How Elastic Search work and where you have used ? => Kibana and Splunk i have used List comprehension in Python and give me the type of string ?How iterator works in Python ?What is SLA and in which algorithm it worked at the backend ?Have you ever created any certificate ? Yes, openssl commandhttps://www.digicert.com/csr-creation-ssl-installation-mac-osx-el-capitan.htmWhat is the demerits and merits while creating a certificate by our own ?What is ca-certificates  and in which Algorithm it worked ?Have you worked in hadoop and Are you good in SQL Queries ?How Ansible worked, let me know its Architecture ?What sequence followed by Ansible while executing the playbook ?Have you ever worked on Dynamic Playbook ?Have you ever worked on Dynamic Docker File ?

Interview Question:JCPenny.com (45 min)1. Tell me about your self, Daily Works, Tools andTechnologies ?NA2. How to update the AMI when Auto Scaling is running ?3. How version number is generating in Jenkins ?4. How Continuous Delivery is happening in your project ?5. How do you create VPC through CLI or Manually ?Both6. How to add the security groups in CF Template while craeting a template for Stacks ?7. What are the Pre-requisite for CF Template while creating a Stacks ?8. Do you have Linux Visibility or not like Installation of Softwares ?Yes9. Lots of question on AutoScaling and CloudFormation Template ?10. Exposure on Ansible and Docker ?Yes11. List all the Security Level of AWS like Security Groups, NACL, WAF ?Np12. Few question on VPC as well ?Np

Interview Question:Indiamart.com (1 hr)1. Tell me the tools and tech, using in your project ?2. Which tools used to connect the AWS Console ?I connect through url only3. Which tools used to connect the S3 Bucket in Cloud ?4. Indiamart using ther own cload as well other vnedors ?Ok5. How can you create an AMI through automation ?Can use Python, Ansible, CF template etc...6. How many types of ELBs present in AWS and what is the difference between them ?Elastic Load Balancer and Application Load Balancer 7. How one can rstrict to IAM User to delete the S3 bucket but can able to view and create in S3 ?Through Roles and Policies8. How can you play with different regions of S3 bucket ???9. How can you take the backup of EC2 Instances ?We generally don’t take backup of EC2 but yeah Volume Snapshot is required10. git log => show all the commit history ?11. git diff COMMIT_ID1 COMMIT_ID2 => difference between two commit ids12. git reset COMMIT_ID => reset all the previous changes13. what is present at the top of "git log" => resent COMMIT_ID14. They are not working on orchestration concept ?Complete DevOps CI and CD were called orchestration15. Discussed about DR backups and all ?We do implement DR to avoid any unwanted disaster from natural calamities 16. How to create instance with conditions thorugh CF Template ???17. What exactly an AMI contains ? Property and Configuration 18. Can you copy the AMI between two different regions ? => YES18. Are you using Docker ?? Upto now we have used images from Docker hub and basic Docker file19. Only working on Shell-Scripting and Perl Scripting ?NA20. How to create a Random no ? import random; print(random.randint(0,9))21. Have you ever done "SVN to GIT" migration and what are the Pre-Requisites ? Yes, we need branching details 22. Why most of the companies are doing Migration ? Because of multiple reasons



@@@@@@@@@@@@@@@@@@@@@@@

Interview:

Questions from GIT, Jenkins, Ansible, Dockers & Containers, Kubernetes, OpenShift, AWS, CI/CD, Scripting(Shell/Python), Linux (RHEL), Monitoring

GIT
###########
* What is GIT ?
* What is difference between GIT & Github ?
* Why we use GIT ?
* What is SCM & VCS ?
* What are the process of pushing the code to Github Repository ?
* Why do we commit ?
* What are the commands of GIT to push the code ?
* How you can merge a git repository with another ? 
* What is branching in git ?
* Different types of branching in GIT ?
* What is merge conflict in git ?
* How you can resolve merge conflict if you are merging same 
  project and in the same branch ?  

Jenkins
##########
* What is Jenkins ?
* Why we use Jenkins ?
* What are the other tools/technologies present in market other than 
  Jenkins for CI/CD ?
* How to move Jenkins from one server to another ?  
* How to create Jenkins backup ? 
* What are plugins in Jenkins ?
* What are the default plugins installed in Jenkins ?
* How to schedule builds in Jenkins ? 
* Difference between Ant, Maven, Gradle ?  
* Difference between Jenkins, Teamcity and Bamboo ?
* How to configure a cloud access in Jenkins ?
* What is Jenkins slaves ?
* How to run a groovy script in Jenkins ?
* What is Jenkins Pipeline ?
* What are different types of Jenkins Pipeline ?
* What is Declarative pipeline in Jenkins ?
* Is Jenkins a CI tool or both CI/CD ?
* How to install Jenkins with non root access in Linux ?
* If you have 200 employees in your company, how you can assign Jenkins 
  access to these employee how you can give permission in Jenkins ?
Jenkins Task
##############
Task 1
Write the Jenkins pipeline code for Java & Php application
Task 2
Write the Jenkinsfile code to build a Java application with Maven with error handling
Task 3
Complete the following tasks: 
1. Jenkins setup on linux 
2. Setup app server with apache to deploy an app.
3. create three jobs on jenkins
4. Pull the code from git repo
5. Build the application
6. deploy an app on apache using ansible.
7. app deploy should work with single trigger hit(git pull job -> build app -> deploy on apache server) 
8. job should get triggered on git push on git repo

Ansible
##########
* What is Ansible ?
* What is Configuration Management ?
* Is Ansible only a tool for Configuration Management ?
* What are the components of Ansible ?
* How Ansible works ?
* What are the other tools in market other than Ansible ?
* How Ansible is different from Chef & Puppet ?
* What is Inventory in Ansible ?
* What are the types of Inventories ?
* What is play & playbook ?
* Difference between hosts & groups ? 
* What is Roles ?
* How to install a Role ?
* How to install multiple roles ?
* How to create roles ?
* What is Dynamic Inventory & when we use it & for what ?
* Where is the Ansible Configuration file located ?
* What are the different ways other than SSH by which Ansible 
  can connect to remote hosts ?
* What is variable in Ansible ?
* What are different types of variables ?
* How to assign variables in group vars & hosts vars ?
* Difference between File & Template directory in Roles ?
* Difference between default & vars directory in Roles ?
* What is Jinja 2 template ?
* What is modules in Ansible ?
* Difference between COPY & FILE modules ?
* Difference between SHELL & COMMAND modules ?
* What is Setup module ? what it does ?
* What is register & debug in Ansible ?
* What is changed_when in Ansible ?
* Can we disable automatic facts gathering in Ansible ?
* How error handling can be done in Ansible ?
* How to ignore failed commands in Ansible ?
* What is handlers ? Why we use Handlers in Ansible ?
* What is Privilege Escalation in Ansible ?
* Task to connect(SSH) Ansible to remote host using another user & 
  run the playbook to the remote host using with another user ?
* What is Ansible vault ?
* How to decrypt a vault file ?
* How to encrypt a string in Ansible using Ansible Vault ?
* If a string is encrypted in a file with a password then how to pass 
  the password using parameter while decrypting ?
* If a file is encrypted using password & password is stored in a file 
  how to pass the file to decrypt the file ?
* If a file is encrypted using password & password is also encrypted 
  then how to provide the password while decrypting the file ?
* What is Ansible galaxy ?
* What is Tags in Ansible ? Why it is used ?
* What is lookup in Ansible playbook ?
* How to control the command failure in Ansible ?
* How to debug your playbook ?
* What is diff mode ?
* What is Dry Run in Ansible & how to do that ?
* What is pre task & post task ?
* How you can run your all tasks at once ? 
* What is block in Ansible ?
* What are different variable scopes ?
* How variable precedence takes place ?
* Difference between include & import ?
* How to include custom modules in Ansible ?
* Describe the role directory structure ?
Ansible Task
#############
Task 1
Part 1. Write Ansible playbook to automate Jenkins deployment
Part 2. Write Ansible role to install Docker & setup Kubernetes cluster 
Automate the pipeline creation in Jenkins to create docker container & deploy on Kubernetes cluster
Task 2
Write ansible playbook for below tasks:
1. Install apache server and deploy sample html application
2. Create /var/www/example.com
3. deploy a sample application to the above directory
4. create a virtual host for deploy application and set it as default virtualhost

Dockers & Containers
######################
* Whats is docker ? 
* Difference between container & VMs ?
* Difference between Docker & Virtualization ?
* Difference between container and image ?
* How image builds ?
* What are image layers ?
* How image layers work ?
* What is overlayfs ?
* Where the image layes can be found in which directory ?
* How can we check the content of each layer ?
* How to check the layers stacked with image ?
* What is Union Mount & AUFS ?
* Why use Union mount system for Docker ?
* What are the 3 different directories in /var/lib/docker/aufs ?
* How to run an image ?
* How to tag an image ?
* How to Link one container with another ?
* How do you sequence the containers? A first then B should execute after that ?
* How to create a volume in docker container to store data ?
* How to mount a local directory into a container ?
* How to expose a port no to access container ?
* What is entrypoint in docker ?
* What is dockerfile ?
* Difference between ADD & COPY parameters in dockerfile ?
* How to create a bridge in container ?
* How a container gets an internal IP ?
* Can we check the process of a container inside as well as outside the container ?
* Can we check the container process on docker host ?
* How kernel isolates to run the container and how resources managed by the kernel ?
* What is namespace and cgroups ?
* What is docker-compose and docker-swarm ?
* How you can give different network IP to the container ?
* What are the parameters of dockerfile ?
* Is there any windows container also available ?
* How to stop a container ?
* How to run a container in background ?
* How to go inside a container if container is running in background ?
* How to check running containers ?
* How to remove an image ?
* How to run an image which is in tar format ?
* Command to check the process of a container ?
* How to check resource utilisation of a container ?
* How to create an image ?
* How to save changes of a container ?
* What are registries ?
* Can we reduce the image size while building ? If yes how ?
* What is multi-stage build ?
* Difference between docker commands: up, run & start ?
* Can we run more than one process in a container ?
Docker Task
#############
Part 1. Write a Docker file to create a Docker image which should have Wordpress installed
Part 2. Write a Docker file to create a Docker image for database
Now, use Docker compose to bring up the above Docker images as containers. Database container should mount the local host's “/etc/mysql” volume into it's (containers) /etc/mysql directory.

Kubernetes
##############
* What is Kubernetes ?
* What are Kubernetes Components ?
* What is etcd ?
* What is master & minion ?
* How to make quorum of cluster?
* What is Replication controller & what it does ?
* What is ingress ?
* Difference between Kubernetes & Docker Swarm ?
* How can you rollbck the previous version of application in Kuberntes?
* Scenario: There are 2 tables, emp, empsal if there schema changes, 
  How does that deployment happens into containers/POD automatically?
* How does container know that application is getting failure ?
* Difference between nodeport, clusterIP, load balancer & ingress ?
* What is kubectl & kubelet ?
* What is the use of Kube-controller manager ?
* What is pod ?
* How many containers can run in a pod ?
* How many containers can be launched in a node ?
* What is the role of Kube-Scheduler ?
* How the 2 pods communicate with each other ?
* How 2 containers inside a pod communicate with each other ?
* What is Flannel & why we use it ?
* Difference between Flannel & Calico ?

OpenShift
###########
* What is Openshift ?
* Difference between Openshift & Kubernetes ?
* What is Services Layer ?
* How to expose a service in Openshift ?
* What are the 3 components of any created project ?
* What is router in default or in any project while creating project ?
* How to go inside a docker container, which command we need to use.
* What is the key benefits docker container provides, why industry moving towards it.
* How to deploy a war archive into docker container runtime from scratch.
* What types of nodes we have in Openshift.
* What is the role of Master, Infra and Worker nodes in Openshift.
* What is Secret and ConfigMap in Openshift.
* How to check if all nodes configured in openshift cluster is healthy.
* How to list all Pods belongs to a specific project.
* What All pods we have in default project.
* How many types of network plugin we have in openshift by default.
* What is the difference between ovs-subnet and ovs-multitenant network policy plugin.
* How the network packet flow between pod - to - pod communication.
* What all SSL termination supported in openshift.
* What is ETCD in openshift, why we need to install it in odd numbers.
* Steps to backup openshift etcd metadata.
* How to Install, Highly available multi dc openshift cluster.
* What is Horizontal Pod Autoscaling in openshift.
* What all services running in master and Infra nodes.
* What do you mean by identity provider in Openshift?
* What is Horizontal Pod Autoscaling in openshift.
* What is replication controller in openshift.
* What is deamonset in openshift.
* How to increase the pod count , scale up the pod replicas in openshift.
* What is pod crashloopback status in openshift, how to troubleshoot.
* How do you create a New user identity ?
* Where is the user identity located ?
* What is project in Openshift ?
* What are the types of permissions/role bindings in Openshift ?
* How to check the permission of user ?
* How to describe anything in Openshift ?
* How to check no of projects ?
* How to assign a role/permission to a user ?
* What is clusterrolebinding in openshift ?
* What is the process/working of POD creation ? 
* What is Builder POD ?
* What is deployer POD ?
* How to create a New application POD ?
* How to check logs of POD ?
* What is Deployment Configuration & why we need DC ?
* What is SVC & why we need SVC ?
* What is RC (Replication Controller) ?
* How to check DC of POD & how to edit DC ?
* How to create route ?
* How to expose svc ?
* How to do rollout ?
* How to increase replica ?
* What is Source to Image in Openshift ?
* What is builder image ?
* What are the process to create source to image ?
* How to give the Cluster role/permission to the user ?
* How to create secure route ?
* What is PV & PVC ?
* What are access modes in PV ?
* What is node selector ?
* What is wildcard in OpenShift ?
* What are the two regions in projects ?
* Difference between template & Deployment Configuration ?
* How to migrate whole cluster to another ?
* How to manually migrate container ?
* What type of build strategies are used in OpenShift ?
* How you upgrade OpenShift ?
* What are the different upgrading strategies available ? 
* What are stateful pods ?
* What are the identity providers in OpenShift ?
* What is port binding ?
* What are labels in OpenShift ?
* Where you keep etcd in production ?
* What are infra nodes ?
* What is service account ?
* How you create project in OpenShift ?
* What is ImageStream and build configs ?

AWS
###########
* What is Amazon RDS ?
* What is EC2, S3, EBS ?
* What is VPC & why we require to create VPC ?
* Is is possible to scale an Ec2 Instance vertically ?
* How is Amazon RDS, Redshift & DynamoDB different ?
* How is a spot Instance different from an On-demand Instance ?
* How Infrastructure As Code processed & executes in AWS ?
* If your Linux-build server getting slow down, what will you do to check ?
* Types of EBS storage ? 
* How to backup a running instance ? 
* How to secure s3 bucket ?
* What are the security available for users to access S3 ?
* How to create AMI ? 
* What are the main components of CloudFormation ?
* What is mapping in cloudformation template ? 
* How is YAML different from JSON ? 
* Different types of ELB ? 
* What is autoscaling group ?
* Which type of ELB is good for application load ?
* What is difference between application load balancer & classic load balancer ?
* What is metrics in cloudwatch ?
* Is it possible to recover your lost private key ?
* How can you connect your EC2 Instance if you lost your key ?
* While connecting to your EC2 instances, what are the possible connection issues one might face ? 
* What is Subnet & how many subnets are there in a VPC ? 
* Why do we make subnets ?
* What is routing table ? 
* How you can connect a private subnet with a public subnet ?
* Can VPC peering possible in two different region ?
AWS Task
#############
Task 1
Write a script which will based on “Number of requests” metric of the ALB/ELB scale up webapp EC2 instances under the Load Balancer, increase AWS Elasticsearch Nodes count, and change the instance size of a MongoDB EC2 instance from m4.large to m4.xlarge. (without using ASG).
Task 2
Architecture Diagram for a PHP/JAVA/Python based application to be hosted on AWS with all mentions like VPC, AWS/any other cloud platform services, well defined network segregation.

Scripting (SHELL/Python)
#######################
Shell Task
#############
Task1
Bash script to setup a whole LAMP stack, PHP app can be Wordpress and DB can be MySQL. This script should install all components needed for a Wordpress website.
We should be able to run this script on a local machine or server and after execution of the script it should have Wordpress Running via Nginx/Apache.
DB user for Wordpress should also be made automatically from within the script and same should be set in Wordpress conf file.
Task 2
Bash script to setup a whole JAVA application stack on a server.
This script should install all components needed for a Java/Grails application.
Once the script is run it should have the java application running and being served via Nginx on local machine or server. Sample java application can be simply a tomcat war etc


CI/CD
#########
* What is CI & CD ?
* What is CI/CD pipeline ?
* Difference between Continuous Delivery & Deployment ?
* List the important tools & technologies used in Devops ?


Linux (RHEL)
############
* What is Linux ?
* What are Linux OS Flavors ?
* Difference between Debian & RPM based OS ?
* What is Kernel ?
* Explain the boot process of Linux OS ?
* How is RHEL different from CentOS ?
* What is the Latest version of RHEL ?
* What is Grub ?
* Difference between Grub & Grub2 ?
* What is boot loader ?
* Do you think the boot process in RHEL 7 is faster than RHEL 6 ? If yes, How ?
* What is .rpm & .deb ?
* What is RPM ?
* What is YUM ?
* Different methods to install the rpm based packages ?
* What is Bash ?
* What is SHell ?
* How many types of SHells are there ? * Explain the daily used basic commands like cp, mv, rm ?
* What is the significance of touch command ?
* In how many ways you can create a file ?
* How to delete the content from a file ?
* Explain the process/work behind hitting the google.com ? how you access google.com ?
* How many types of permissions are there ? What is chmod ?
* What is sticky bit  ?
* What is ACLs ?
* What is SetGID, SetUID & Stickybit ?
* Location where all the user information are stored ?
* File where user password are stored ?
* What is the default permission of a file ?
* What is the significance of -rvf ?
* What is PV, VG & LV ?
* What are the types of file system ?
* What is XFS ?
* Can we reduce XFS file system ?
* How can we extend LV ?
* Command to check running process ?
* Command to check RAM usage ?
* Command to check Disk usage ?
* Difference between ps -aux & top command ?
* What are the ways to check CPU usage ?
* How to check CPU details ?
* Explain the steps to create a partition & how to format with file system ?
* Explain the steps to create LV ?
* Explain steps to reduce XFS & EXT files systems ?
* Significance of .bashrc file ?
* How you check the kernel version ?
* How you check the Red hat release version ?
* Significance of resolv.conf file ?
* What is DNS ? How you resolve DNS ? Types of DNS records ?
* Difference between Nginx & HTTP Server ?
* Port no of HTTP, FTP, SSH, HTTPS ?
* What is SSH ?  How you generate SSH-keys ?
* What is Private & public key ? How they authenticate ?
* Configuration file of SSH ?
* Configuration file of HTTP ?
* What is Virtual Hosting ? How you configure virtual hosting ? 
* Explain ifconfig command ?
* Difference between IPv4 & IPv6 ?
* What is MAC address ? can we change the physical address ?
* How to check system uptime ?
* How to check memory information ?
* What is SWAP ?
* What is the exact memory free in your system ?
* What is cache memory ?
* What if you can do rm -rvf / ?
* Kinds of permission in Linux ?
* What is vim & vi ?
* What is pipe | ?
* What is grep command ?
* What Find command does ?
* How to redirect commands output ?
* What is systemd in Linux ?
* What does systemctl do ?
* If you run a command like nautilus in terminal, whether it will block your terminal or not ?
* If yes, whats the solution of this to not to unblock the terminal without closing the command application?
* What is rsyslog ?
* What is SSH-tunnel ?
* How to set history size ?
* How to extend VG ?
* What are logical & extended partitions ?
* Explain the steps to reset root password at boot time ?
* What are run-levels ? How many types of run levels are there ?
* How we change the run level ?
* How to check the logs ?
* Difference between Journalctl & tail command ?
* What does the subscription-manager do ?
* How to archive a file ?
* What is umask ?
* How to kill a process ?
* How to assign IP address manually ?
* How to assign static IP address to a system ?
* Explain the different types of Linux process states ?
* What is a Zombie process ?
* What is KVM ?
* What is hypervisor ?
* Difference between MBR & GPT ?
* How you can mount a file system permanently ?
* What is cron ? How to setup a cron job ?
* What is Kickstart ?
* How to create a network bridge in Linux ?
* Difference between iptables & firewalld
* What is SElinux ?
* What is ISCSI & targetcli ?
* Difference between NFS & SAMBA ?
* What is nfsnobody ?
* What is SSHFS ?
* What is Kerberos ?
* How to secure NFS with Kerberos ?
* What is the difference between telnet & SSH ?
* What is DHCP ?
* What is Kickstart file ?
* What is NTP Server ? How to configure NTP ?

Monitoring
############
* Why we use monitoring ? 
* What are the different tools & technologies for monitoring ?
* How we monitor our applications & servers differently  ?
* What is Prometheus ? How is different from other monitoring tools ?
* What is ELK stack ?
* Why we use Grafana ?
* How we query different outputs in Prometheus ?
* What type of graph can be implemented in Grafana ?

@@@@@@@@@@@@@@@@@@@@@@@

Python Interview Questions:

https://github.com/zhiwehu/Python-programming-exercises/blob/master/100%2B%20Python%20challenging%20programming%20exercises.txt

Quest-1:

List1 contains any no of employees and having an ages > 30 
List2 contains any no of employees and having an ages < 60 in the same organization

Fetch out the no of employees having an ages between 30 to 60 ??

Ques-2:
 
A folder will be the runtime argument and you need to traverse the folder and list all the files and folders, at some path there would be some scripts and you need to check weather the script is having the executable permission or not as well executing or not ??

Ques-3:

Two random inputs are there one is List and another is count.
List1 contains some random no of elements and inside count you need to pass any no of arguments say 2,

Suppose you passed count(2) so it will pick only two items from List and give the sum of two list elements which should be minimum of any two elements
Suppose you passed count(2) so it does the same operation but in this case it will give the maximum of any two elements.


https://checkcoverage.apple.com/us/en/

# Python code to reverse each word individually 
# Function to reverse words
def revWord(Sentence):
    # All in one line 
    return ‘ ‘.join(words[::-1] for words in Sentence.split(“ “)
# Drivers Code
Sentence = “ geeks for geeks”
Print (revWord(Sentence))

@@@@@@@@@@@@@@@@@@@@@@@

20-25 Interview Questions
Paytm + Nagarro + Verizon Media


Groovy Tutorial Finish
https://www.youtube.com/watch?v=4vMyswKt6YQ&list=PLhW3qG5bs-L8T6v6DgsZo93DgYDmOF9u4&index=1


Shell Scripting Finish
https://www.youtube.com/watch?v=Zzd9tarN3Lg&list=PL2qzCKTbjutJRM7K_hhNyvf8sfGCLklXw


Prometeus Finish 
https://www.youtube.com/watch?v=yq3GEs_nV0s&list=PLoVvAgF6geYNy12sJwYbNYdzNc6gkf8yf


Python Interview:
https://github.com/zhiwehu/Python-programming-exercises/blob/master/100%2B%20Python%20challenging%20programming%20exercises.txt

@@@@@@@@@@@@@@@@@@@@@@@

Amazon:

Thank you for your interest in an opportunity with AWS, please find attached JD, Leadership Principles and interview preparation links.

Request you to go through the below mentioned topics and prepare well for the interview.

We will conduct the interview on 21st February 2020 @ Hyderabad, will share the venue details with you shortly.  

Do reach out to me for any queries.
1.       This is a technical support role where you are expected to provide support to AWS Customers [via email, chat & phone] on services described in the following link: https://aws.amazon.com/devops/
2.       AWS will not interview you on any AWS services, unless you have experience in them.
3.       AWS will interview you on your past experiences: we would like to understand your knowledge in certain subjects, your approach when put in a specific situation and your strengths.
4.       There will be a total of 4 to 5 interview rounds, out of which two rounds will be technical: DevOps and Linux OS + Networking.

NOTE: The material provided below is to help you with your preparations for the interviews. Do not depend on it entirely.

—————————————————————————————————————————————————————————————————
Operating System [Linux]:

	•	Intro: https://www.studytonight.com/operating-system/introduction-operating-systems
	•	Virtual Memory: https://searchstorage.techtarget.com/definition/virtual-memory
	•	Process Scheduling: https://www.studytonight.com/operating-system/process-scheduling
	•	Linux boot process: https://www.thegeekstuff.com/2011/02/linux-boot-process
	•	Windows boot process: http://sansbound.com/blog/2012/08/10/understanding-the-boot-process-charles-joseph/
	•	File permissions: https://www.guru9.com/file-permissions.html
	•	Linux: https://linuxjourney.com/
	•	Basic Commands: https://maker.pro/linux/tutorial/basic-linux-commands-for-beginners

Networking :
	•	Make sure you have a big picture understanding of how networks work - https://www.youtube.com/watch?v=9BGWrLiT9qs
	•	TCP/IP - 3-way handshake - https://support.microsoft.com/en-in/help/172983/explanation-of-the-three-way-handshake-via-tcpT-ip
	•	HTTP - https://hpbn.co/
	•	SSL/TLS - https://blog.cloudflare.com/keyless-ssl-the-nitty-gritty-technical-details/ ; https://www.ssl.com/article/ssl-tls-handshake-overview/
	•	IP addressing: https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html ; https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379547(v=ws.10)
	•	NAT: https://www.slashroot.in/linux-nat-network-address-translation-router-explained ; https://netfilter.org/documentation/HOWTO/NAT-HOWTO.html#toc6.1
	•	SNAT: https://netfilter.org/documentation/HOWTO/NAT-HOWTO-6.html#ss6.2
	•	DNS: https://www.verisign.com/en_US/website-presence/online/how-dns-works/index.xhtml ; https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197427(v=ws.10)
	•	DHCP: https://www.youtube.com/watch?v=0Dp7YoR0SLE ; https://vinitpandey.com/2015/06/17/dora-process-of-dhcp/
	•	ARP: https://networklessons.com/cisco/ccnp-route/arp-address-resolution-protocol-explained
	•	MSS/MTU: https://www.imperva.com/blog/mtu-mss-explained/

Devops:

Docker:
	•	Containerizing applications: https://docs.docker.com/engine/examples/
	•	Customizing docker daemon: https://docs.docker.com/config/daemon/
	•	Logging drivers: https://docs.docker.com/config/containers/logging/configure/
	•	Storage drivers: https://docs.docker.com/storage/storagedriver/select-storage-driver/
	•	Networking modes: https://docs.docker.com/network/
	•	Troubleshooting: https://docs.docker.com/toolbox/faqs/troubleshoot/

Container References:
	•	https://training.play-with-docker.com/
	•	https://www.katacoda.com/
	•	https://docker-curriculum.com/

Kubernetes:
	•	K8's architecture and components of master and worker nodes: https://www.tutorialspoint.com/kubernetes/kubernetes_architecture.htm ; https://x-team.com/blog/introduction-kubernetes-architecture/
	•	Troubleshooting: https://kubernetes.io/docs/tasks/debug-application-cluster/troubleshooting/

CI/CD:
	•	Concept: https://medium.com/@nirespire/what-is-cicd-concepts-in-continuous-integration-and-deployment-4fe3f6625007
	•	CICD Tools overview: https://www.digitalocean.com/community/tutorials/ci-cd-tools-comparison-jenkins-gitlab-ci-buildbot-drone-and-concourse
	•	Troubeshooting: https://openedx.atlassian.net/wiki/spaces/TE/pages/102367626/Troubleshooting+Jenkins+Builds
	•	Overview of Build and release: https://wiki.cdot.senecacollege.ca/wiki/Overview_of_the_Build_and_Release_Process

Configuration Management:
	•	Introduction to Ansible: https://www.tutorialspoint.com/ansible/ansible_introduction
	•	Chef overview: https://docs.chef.io/chef_overview.html
	•	Troubleshooting Cookbooks: https://docs.chef.io/errors.html

Infra as code:
	•	Terraform introduction: https://wiki.cdot.senecacollege.ca/wiki/Overview_of_the_Build_and_Release_Process

 
￼
 
 
 

@@@@@@@@@@@@@@@@@@@@@@@

Elastic Search:

1. What Is Elasticsearch?
2. Why Elasticsearch?
3. Elasticsearch Advantages
4. Elasticsearch Installation
5. API Conventions
6. Elasticsearch Query DSL
7. Mapping
8. Analysis
9 Modules

—————————————————————————————————————————————————————————————————————————————

https://stackify.com/elasticsearch-tutorial/

https://logz.io/blog/elasticsearch-tutorial/

https://www.tutorialspoint.com/elasticsearch/index.

@@@@@@@@@@@@@@@@@@@@@@@

Airtel:

Difference between SCP and Rsync command in Linux?
https://stackoverflow.com/questions/20244585/how-does-scp-differ-from-rsync

How DR is handling ?
How AS configured ?

Add multiple users from a file and add into server ? Use of Shell Scripting
https://www.2daygeek.com/linux-bulk-users-creation-useradd-newusers/

How do you tag the project ?
In which branch you tag the project ?
How do you handle the AWS CLI Or Manual ?
How you are connecting the Database Server?
Default ALLOW or DENY present in AWS ??
Port 22 default enable or disable in EC2 ?
How to manage the same version in Artifactory? We don’t want overwrite the same version ? How you will handle ?
How Sonarqube plugin use in Jenkins ?
How Maven plugin and why it used ?
How to upgrade the Jenkins ?
What is workspace in Jenkins ?
Which folder is used to take the Jenkins backup ?
Why & How git revert used in git ?
In which branch you freeze the code ?
In which stage Sonarqube resides if we implement in groovy pipeline ?
Have you created RDS Instance ?

How you can take the backup of Jenkins jobs ??
https://devops.stackexchange.com/questions/21/how-do-you-back-up-jenkins-jobs-master-configs

@@@@@@@@@@@@@@@@@@@@@@@

Polland:

Java:

JConsole in Java ?

JVM in Java ?


————————————————————————————————————————————————————————————————————————————

Linux:

What is /proc and definition ?
proc file system in Linux. Proc file system (procfs) is virtual file system created on fly when system boots and is dissolved at time of system shut down. It contains the useful information about the processes that are currently running, it is regarded as control and information centre for kernel.

traceroute in linux ?
https://www.google.co.in/amp/s/www.geeksforgeeks.org/traceroute-command-in-linux-with-examples/amp/


How to list the inodes no of file in linux ?

How to see the load average and what is it ?

How to kill the zobie process and what is it ?

————————————————————————————————————————————————————————————————————————————

ansible:

How to check the ansible playbook ?
$ ansible-playbook —syntax-check

What is blocks in ansible ?

————————————————————————————————————————————————————————————————————————————

docker:

How to minimise the docker image size ?

How to handle container dependency ? 

How container manages framework ?

Docker Compose ? 
To check the containers to another container is up or down 

Secrets in Docker ?

————————————————————————————————————————————————————————————————————————————

Jenkins:

How to publish a html page in Jenkins ?

Jenkins backup => Shell Scripting script 

————————————————————————————————————————————————————————————————————————————

Git & SVN:

key difference between git and svn

light clone ? Not $ git clone URL

————————————————————————————————————————————————————————————————————————————

kibana:

Difference between logstash and filebeat

What is Elastic Search ? How do you use ??

@@@@@@@@@@@@@@@@@@@@@@@

Aptitude Questions:

https://www.ambitionbox.com/topics/aptitude/questions-and-answers

@@@@@@@@@@@@@@@@@@@@@@@

Nagaro Interview Questions:

Explain Git Branching Model, How you will propose the Model to Client ?

https://www.youtube.com/watch?v=fCNX8yLcw2Q

￼

￼

￼
￼
￼
￼
￼

More Branching Strategy:

￼

*********************************************************************************************

What kind of Network do you use in Docker Swarm ?

When you initialize a swarm or join a Docker host to an existing swarm, two new networks are created on that Docker host: an overlay network called ingress , which handles control and data traffic related to swarm services.

*********************************************************************************************

Docker Cheat Sheet ?

Ref:
https://www.docker.com/sites/default/files/d8/2019-09/docker-cheat-sheet.pdf

*********************************************************************************************

Suppose 3 servers are running ? One is Master and Two Slaves and if one fails then how you will migrate ?



*********************************************************************************************

What is the importance of Min, Max and Desired in AS in AWS ?

Min: This is the minimum number of instances that have to be there in your Autoscaling Group at all times. ... 
Your autoscaling will never increase the number of instances more than the specified Max number. 
Desired: The desired amount represents the "current amount" of instances in your autoscaling group.

*********************************************************************************************

Why Sonarqube used in Jenkins ?

Ref:
https://aspiresoftware.in/blog/intergrating-sonarqube-and-jenkins/
https://www.youtube.com/watch?v=jh7utASgKj4

*********************************************************************************************

Working as Sr DevOps Engineer
Currently handling all Prod & Non-Prod related server and specially Production Releases 
Next Release is 20.1
Git, Jenkins, Maven, Shell Scripting, Python, Powershell, Ansible, Kibana, Jira, SNOW, CF Template
Automation:
	During CI CD Pipeline
	Ansible automation
	Kibana Automation through ansible
	CF Template Automation
	Shell Scripting automation as per requirement
	
*********************************************************************************************

Kubernetes Cheat Sheet:

# Create multiple YAML objects from stdin
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: busybox-sleep
spec:
  containers:
  - name: busybox
    image: busybox
    args:
    - sleep
    - "1000000"
---

Ref:
https://kubernetes.io/docs/reference/kubectl/cheatsheet/

*********************************************************************************************

Draw the AWS infrastructure

￼

*********************************************************************************************

Waterfall vs Agile, with pros and cons.

Waterfall is a Liner Sequential Life Cycle Model whereas Agile is a continuous iteration of development and testing in the software development process. ... Agile allows changes in project development requirement whereas Waterfall has no scope of changing the requirements once the project development starts.

*********************************************************************************************

Draw the K8s setup

￼

https://www.aquasec.com/wiki/display/containers/Kubernetes+Architecture+101

*********************************************************************************************

Explain the K8s components

Master Components:
	•	etcd cluster - 
	•	a simple key value storage 
	•	store the Kubernetes cluster data (such as number of pods, their state, namespace, etc), 
	•	etcd enables notifications to the cluster about configuration changes with the help of watchers. 

	•	kube-apiserver - 
	•	Kubernetes API server is the central management 
	•	that receives all REST requests for modifications (to pods, services, replication sets/controllers and others), 
	•	serving as frontend to the cluster. Also, 
	•	only component that communicates with the etcd cluster, 
	•	making sure data is stored in etcd and is in agreement with the service details of the deployed pods.
	•	kube-controller-manager - 
	•	runs a number of distinct controller processes in the background
	•	 (for example, replication controller controls number of replicas in a pod, endpoints controller populates endpoint objects like services and pods, and others) 
	•	When a change in a service configuration occurs (for example, replacing the image from which the pods are running, or changing parameters in the configuration yaml file), 
	•	the controller spots the change and starts working towards the new desired state.

	•	cloud-controller-manager - 
	•	is responsible for managing controller processes 
	•	For example, when a controller needs to check if a node was terminated or set up routes, load balancers or volumes in the cloud infrastructure, 

	•	kube-scheduler - 
	•	helps schedule the pods (a co-located group of containers inside which our application processes are running) 
	•	For example, if the application needs 1GB of memory and 2 CPU cores, then the pods for that application will be scheduled on a node with at least those resources. 
	•	The scheduler runs each time there is a need to schedule pods. The scheduler must know the total resources available as well as resources allocated to existing workloads on each node.
Worker Components:
	•	kubelet - 
	•	the main service on a node, 
	•	regularly taking in new or modified pod specifications (primarily through the kube-apiserver)
	•	ensuring that pods and their containers are healthy and running in the desired state. 
	•	This component also reports to the master on the health of the host where it is running.

	•	kube-proxy - 
	•	a proxy service that runs on each worker node to deal with individual host subnetting and expose services to the external world. 
	•	It performs request forwarding to the correct pods/containers across the various isolated networks in a cluster.


https://www.aquasec.com/wiki/display/containers/Kubernetes+Architecture+101

*********************************************************************************************

Explain difference between ALB,NLB,ELB

NLB: 
	network load balancer just forward requests 
ALB: 
	application load balancer examines the contents of the HTTP request header to determine where to route the request. 
	application load balancer is performing content based routing.
	HTTP, HTTPS
	EC2-VPC
	Load balancer generated
ELB:
	automatically distributes incoming application traffic across multiple applications, microservices, and containers hosted on Amazon EC2 instances.
CLB:
	Classic Load Balancer
	HTTP, HTTPS, TCP, SSL
	YES (you can provide your own application cookie)

Ref:
https://cloudacademy.com/blog/application-load-balancer-vs-classic-load-balancer/

*********************************************************************************************

Write a simple Dockerfile

FROM ubuntu

ADD . /app

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y nodejs ssh mysql
RUN cd /app && npm install

# This should start three process, mysql, ssh in the backgorund 
# And node app in foreground

CMD mysql & sshd & npm start

Execution:

$ docker build -t <tag-name> <path-of-dockerfile>

Example to create own image:

$ docker build latest:npm Dockerfile .
$ docker build -t wtf .

*********************************************************************************************

Difference between RUN and CMD in Dockerfile

RUN:
	executes command(s) in a new layer and creates a new image.
	E.g., it is often used for installing software packages.
	RUN apt-get update && apt-get install -y \
	bzr \
  	cvs \
  	git \
  	mercurial \
  	subversion

CMD:
	sets default command and/or parameters, which can be overwritten from command line when docker container runs.
	CMD ["/bin/echo", "Hello world"]
	
Entrypoint:
	configures a container that will run as an executable.
	Example:
	ENV name John Dow
	ENTRYPOINT ["/bin/bash", "-c", "echo Hello, $name"]
	$ docker run -it <image>
	Hello, John Dow	# Output
	
Difference between ENTRYPOINT & CMD:
	CMD is executed only if ENTRYPOINT is between brackets.
	If ENTRYPOINT is between brackets, the file existence is checked with stats
	Behaves differently of RUN
	CMD/ENTRYPOINT are designed to accept only a single command	

Difference between RUN & CMD:
	RUN and CMD are both Dockerfile instructions. 
	RUN lets you execute commands inside of your Docker image.
	CMD lets you define a default command to run when your container starts. 
	CMD is a Docker run-time operation, meaning it's not something that gets executed at build time.

*********************************************************************************************

How we create K8s cluster


Ref:
https://www.gremlin.com/community/tutorials/how-to-create-a-kubernetes-cluster-on-ubuntu-16-04-with-kubeadm-and-weave-net/

*********************************************************************************************

Explain Jenkinsfile

A Jenkinsfile is a text file that contains the definition of a Jenkins Pipeline and is checked into source control. 
Jenkins Pipeline which implements a basic three-stage continuous delivery pipeline.

Example:
// Suppose you wanna to execute a project:
// Clone a Project	- Clone
// Versioning 	- Version
// Build Part	- Build & Package
// Docker Images	- DocImages
// Delete the Docker Images		- DocDeleteImages

node() {
    cleanWs()
    
    stage('Cloning'){
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: ‘yruiwfjfk-ahefsnf-fjskjfkjkjf’, url: 'https://github.com/xavyaly/game-of-life.git']]])
    }
}

   stage(‘Versioning’) {
	VERSION_NUM = VersionNumber([projectStartDate: '2017-11-20’, versionNumberString: ‘1.0.1_${2018, XXX}’, versionPrefix: 'v'])
	    //VERSION_NUM = VersionNumber([projectStartDate: '2017-11-20', versionNumberString: '${2018, XX}', versionPrefix: 'v']);

    //}

*********************************************************************************************

Kind of Deployment Strategy

	•	Recreate: Version A is terminated then version B is rolled out.
	•	Ramped (also known as rolling-update or incremental): Version B is slowly rolled out and replacing version A.
	•	Blue/Green: Version B is released alongside version A, then the traffic is switched to version B.
	•	Canary: Version B is released to a subset of users, then proceed to a full rollout.
	•	A/B testing: Version B is released to a subset of users under specific condition.
	•	Shadow: Version B receives real-world traffic alongside version A and doesn’t impact the response.

Ref:
https://thenewstack.io/deployment-strategies/
https://dev.to/mostlyjason/intro-to-deployment-strategies-blue-green-canary-and-more-3a3

*********************************************************************************************

Docker Swarm Cheat Sheet:

docker swarm init --advertise-addr <ip>   # Set up master
docker swarm init --force-new-cluster -advertise-addr <ip>   # Force manager on broken cluster

docker swarm join-token worker            # Get token to join workers
docker swarm join-token manager           # Get token to join new manager

docker swarm join <server> worker         # Join host as a worker

docker swarm leave	

docker swarm unlock                       # Unlock a manager host after docker 
                                          # daemon restart when autolock is on

docker swarm unlock-key                   # Print key needed for 'unlock'

docker node ls                            # Print swarm node list
docker node rm <node id>
docker node inspect --pretty <node id>

docker node promote <node id>             # Promote node to manager
docker node demote <node id>

*********************************************************************************************

Working as an independent contributor in DevOps within a large product team. Handling day to day queries and task of different projects in tech stacks like Node.js , Angular , Java , .net , Oracle , PostgresDB including containerisation and micro-services architecture. Also designing AWS network diagram for new and fork-lifted projects. Working in all aspects of DevOps with different tools like IAC , Automation end to end cycle, Monitoring, Source Control Management, Automation testing,Configuration Management, Security, Database Automation and Management.

Amazon SQS (Simple Queue Service) is a message passing mechanism that is used for communication between different connectors that are connected with each other. It also acts as a communicator between <a href="https://asha24.com/aws-certification-training"> various components of Amazon.</a>

*********************************************************************************************

Nagarro Aptitude Questions:

https://www.wisdomjobs.com/e-university/nagarro-aptitude-interview-questions.html

*********************************************************************************************

Difference between git reset and git revert:

$ git reset:
	git reset will reset the state of the branch to a previous state by dropping all the changes post the desired commit
	$ git reset --hard a0fvf8

$ git revert 
	git revert will reset to a previous state by creating new reverting commits and keep the original commits.
	git revert OLDER_COMMIT^..NEWER_COMMIT

Note:
	It's recommended to use git revert instead of git reset in enterprise environment. 

Ref:
https://www.pixelstech.net/article/1549115148-git-reset-vs-git-revert

*********************************************************************************************

Difference between Build Periodically and Poll SCM:

Poll SCM 
	periodically polls the SCM to check whether changes were made (i.e. new commits) and 
	builds the project if new commits where pushed since the last build, 
whereas 
Build periodically builds the project periodically even if nothing has changed.

MINUTE: Minutes within the hour (0-59)
HOUR: The hour of the day (0-23)
DOM: The day of the month (1-31)
MONTH: The month (1-12)
DOW: The day of the week (0-7) where 0 and 7 are Sunday.

*********************************************************************************************





@@@@@@@@@@@@@@@@@@@@@@@

General Interview Questions:

Shell Script to list the name of files in a certain path ?
#!/bin/sh
for i in `ls -lar *.*`
do
echo $i
done

Algorithm to use in Elastic Load Balanacer ?

How Autoscaling is configured and alogorithm used at the backend ?

How Autoscaling is configured ?
Create Launch Configuration -> Choose AMI, InstanceType, Configure Details, Security Groups and KeyPair => Launch it
aws autoscaling create-launch-configuration --launch-configuration-name my-launch-config --placement-tenancy dedicated --image-id ...
aws autoscaling describe-launch-configurations --launch-configuration-names my-launch-config
aws autoscaling create-launch-configuration --launch-configuration-name classiclink-config --image-id ami_id --instance-type instance_type \
--classic-link-vpc-id vpc_id --classic-link-vpc-security-groups group_id
aws autoscaling update-auto-scaling-group --auto-scaling-group-name my-asg --launch-configuration-name classiclink-config

Read the whole Auto Scaling Documentation ?

Have you ever Hosted any WebApplication in AWS or Normal ? => Through Docker only

Alogorithm used in Auto Scaling ?
autoscaler_task_interval 60000;
min_app_instances  1;
server_startup_delay 180000;
max_requests_per_second   5;
rounds_to_average       2;
alarming_upper_rate 0.7;
alarming_lower_rate 0.2;
scale_down_factor 0.25;

Which language comes in the output of Ansible ? => JSON

How DNS resolution work ?

Ansible Roles Architecture ?

How to handle multiple yml playbooks ? Include module

How to put condition in Ansible ? When
tasks:
  - name: "shut down Debian flavored systems"
    command: /sbin/shutdown -t now
    when: ansible_os_family == "Debian"

List of modules which you have worked ? Need to go in depth
when, yum, command, become, tasks, accelerate, 

How to check Docker Container is up or down ? $ docker ps -a -q

List the Values in ascending order and keys in any order in Python ?

Fetch the string from a list only without list comprehension ? a = [1,"one",2] => one

How SNS work in AWS and how you have configured in your Project ? Read SNS AWS Article

What is the maximum no of nodes which you have configured in Ansible Playbook ? 20+

Ansible or Puppet which one is better and why ? Ansible because no Master and Agent concept, Pull Concept, Less time 

Directory structure for Roles in Ansible ?
site.yml
webservers.yml
fooservers.yml
roles/
   common/
     tasks/
     handlers/
     files/
     templates/
     vars/
     defaults/
     meta/
   webservers/
     tasks/
     defaults/
     meta/

Have you created any Docker file by your own elaborate it ? Yes, for Jenkins and MySQL

Which mandatory module you have to implement in REST Python API ? 
Import os
pip install py-rest-client

Which module you need to implement to interact the AWS Services or for AWS Automation ? boto or boto3

Structure for copy module in Ansible while copying multiple files from local to remote machine ?
- copy:
    src: /srv/myfiles/foo.conf
    dest: /etc/foo.conf
    owner: foo
    group: foo
    mode: 0644

Why and how you have implemented the Cloud Watch Monitoring ? Read AWS Cloud Watch Monitoring
To enable all actions for an alarm => aws cloudwatch enable-alarm-actions --alarm-names myalarm

Why we use handlers module in Ansible ? To restart any service
---
- hosts: webservers
  vars:
    http_port: 80
    max_clients: 200
  remote_user: root
  tasks:
  - name: ensure apache is at the latest version
    yum: name=httpd state=latest
  - name: write the apache config file
    template: src=/srv/httpd.j2 dest=/etc/httpd.conf
    notify:
    - restart apache
  - name: ensure apache is running (and enable it at boot)
    service: name=httpd state=started enabled=yes
  handlers:
    - name: restart apache
      service: name=httpd state=restarted

What is the data type for class in Python ?

Have you worked on Ansible with Docker ? No

Command to install Docker in OS ? Mac => sudo easy_install docker 

Pre-requisites to install Docker => Python would be must

Difference between List and Tuple ?
List is Mutable and Tuple is Immutable

Where have you used list and tuple in your project ?
Useless question

How to fetch the unique elements in Python ? => set

Is string is a mutable to immutable ? mutable 

In Dictionary, will the data will print the way you insert ? Need to verify 

Which Algorithm used at the backend of Dictionary in Python ? Hashmap Techniques

How Elastic Search work and where you have used ? => Kibana and Splunk i have used 

List comprehension in Python and give me the type of string ? 
A = [ print(i) for i in range(10) ]
Print(A)

How iterator works in Python ? Iterator used to iterate the array elements
# define a list
my_list = [4, 7, 0, 3]
# get an iterator using iter()
my_iter = iter(my_list)
## iterate through it using next() 
#prints 4
print(next(my_iter))
#prints 7
print(next(my_iter))
## next(obj) is same as obj.__next__()
#prints 0
print(my_iter.__next__())
#prints 3
print(my_iter.__next__())
## This will raise error, no items left
next(my_iter)

What is SLA ? 
A service-level agreement (SLA) is a document describing the level of service expected by a customer from a supplier, laying out the metrics by which that service is ... However, it's recommended that the client and the outsourcing company work together during the SLA contract negotiation to eliminate any ...

Which algorithm it worked at the backend of SLA ?
Interleaved Polling Algorithm

Have you ever created any certificate ? Yes, through openssl command
The commands below can be used to view the certificate fingerprint/thumbprint.
• SHA-256: openssl x509 -noout -fingerprint -sha256 -inform pem -in [certificate-file.crt] 
• SHA-1: openssl x509 -noout -fingerprint -sha1 -inform pem -in [certificate-file.crt]
• MD5: openssl x509 -noout -fingerprint -md5 -inform pem -in [certificate-file.crt] 

What is the demerits and merits while creating a certificate by our own ?
Advantages
1. No PKI (Public Key Infrastructure) is needed.
2. Automatic deployment (Usually Self-signed certificates created automatic during the installation process of the server side applications).
Disadvantages
1. The certificates aren’t trusted by other applications/operating systems. This may lead to authentications errors etc.
Note: To overcome this limitation, some IT staff add the self-signed certificates to the Trusted Roots Certificate Authorities. However, using this workaround may to additional time that needed for management and troubleshooting.
2. Self-signed certificates life time is usually 1 years. Before the year is ended, the certificate may need to renew/replace.
3. Self-signed certificates may use low hash and cipher technologies. Due this, the security level that implemented by self-signed certificates may not satisfy the current Security Policy etc. .
4. No support for advanced PKI (Public Key Infrastructure) functions (e.g. Online checking of the revocation list etc.).
5. Most of the advanced feathers of the server side applications required to impended a PKI (Public Key Infrastructure). By this, self-signed certificates advantages can't be used.

What is ca-certificates  and in which Algorithm it worked ?
CA certificates can also be used to establish trust relationships between CAs in two different public key infrastructure (PKI) hierarchies.
Root CA Certificate 
	Issuing CA Certificate
		User Certificate
The following are some of the trust scenarios that can be enabled by properly configured CA certificates:
	• Simple trust within an enterprise PKI
	• Cross trust between two enterprise CAs (restricted)
	• Bridge trust for multiple enterprise PKIs (unrestricted)
	• Certificate trust continuity when the certificate policy changes

Have you worked in hadoop and Are you good in SQL Queries ? No, and Yes

How Ansible worked, let me know its Architecture ?


What sequence followed by Ansible while executing the playbook ?
INVENTORY (LIST OF ALL WEBSERVERS), PLAYBOOK (MENTION ALL INVENTORIES) -> THROUGH SSH IT CONNECTS WITH REMOTE NODES AND DO THE DEPLOYMENT

Have you ever worked on Dynamic Playbook ?

Have you ever worked on Dynamic Docker File ?

Installation of Ansible ?
Install packages below on server machines
$ sudo apt-get install python-yaml python-jinja2 python-paramiko python-crypto python-keyczar ansible
Install packages below on client machines
$ sudo apt-get install python-crypto python-keyczar

How to read the last word of a file ?
awk 'NF {print $NF; exit}'
OR
# Python Code to read the first and last word of a file
f = open("file_name.ext","r")
for line in f:
	words = line.split()
	print(words[-1])
OR
f = open("file_name.ext","r")	# open the file in read mode only
line = []  # create an empty list to store the lines of a file
for i in f:
	line.append(i)  # loop over the line in the file and store them in the list
for i in line:
	words_in_line=i.split()  # creates a list of the words in each line
	print(words_in_line[0],words_in_line[-1])  # print out the first and last word of each line

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Panda: Machine Learning

Three Data Structures:
Series; Data Frame; Panel

Ex_1:
import pandas as pd
import quandl 
df = quandl.get('WIKI/GOOGL')
print(df.head)

Note: 
Series: 1D (Homogeneous data; Size Immutable; Data Mutable)
Data Frame: 2D (Heterogeneous data; Size Mutable; Data Mutable)
Panel: 3D (Heterogeneous data; Size Mutable; Data Mutable)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Where we implement Auto Scaling Instance Level or ELB Level ?
Instance level

What kind of Ansible Playbook you wrote ?

Rename all files contents as "xyz" using Shell Scripting ?

What kind of automations you have done in Python ?

Difference between Git and SVN ?

What it indicates when checkout happened and meanwhile a new file would created in SVN ?

Why we used JSON ?

What happened when /boot or /root volume shows 100% ?

Can we release cache memory and how ?
sync; echo 3 > /proc/sys/vm/drop_caches

Difference between jar war and ear files in java ?
In J2EE application, modules are packaged as EAR, JAR and WAR based on their functionality
JAR: EJB modules which contain enterprise java beans (class files) and EJB deployment descriptor are packed as JAR files with .jar extenstion
WAR: Web modules which contain Servlet class files, JSP Files, supporting files, GIF and HTML files are packaged as JAR file with .war (web archive) extension
EAR: All above files (.jar and .war) are packaged as JAR file with .ear (enterprise archive) extension and deployed into Application Server.

How to create a 0 downtime deploy manually using Jenkins ?

Difference between .rb and .erb ?
erb is the extension of the template engine used to interpret the file. ... erb is the file extension for eRuby documents, which is a way of embedding Ruby into a text document. Similar to how PHP works. rb is the file extension for ruby 



Ansible Vault ?
ansible-playbook site.yml --ask-vault-pass
From <http://docs.ansible.com/ansible/latest/playbooks_vault.html> 
ansible-playbook site.yml --vault-password-file ~/.vault_pass.txt
ansible-playbook site.yml --vault-password-file ~/.vault_pass.py

How to list the variables in Ansible ?
How to fetch the environment variables in Ansible ?
Difference between Ansible and Chef ?
How Ansible used for Provisioning ?
Difference between List and Tuple ?
How Multithreading inherited in Python ?
Key features of Python ?
How Auto Scaling works in AWS ?
What you have implemented in AWS Lambda ?
Which is most recent script you worked upon ?
Git stash command ?
Git list the commit changes  ?
Git revert the changes ?
Git difference command ?
Difference between Git and SVN ?
Difference between Pull and Push in GIT ?




Javeds-MacBook-Air:DevOps-Interview-Questions javedalam$ 


@@@@@@@@@@@@@@@@@@@@@@@

AWS Questionnaires:
------------
1) Create an SQS queue.  This SQS queue should take s3 bucket names as an input.  Maybe it should also take the region of the s3 bucket as well?  You might want to have it take a JSON object {"bucketname": "this_is_my_bucket", "region": "us-west-2"}

2)  Have a lambda subscribe to the SQS queue.  It takes the bucketname that it gets from the queue, and iterates over each object in that bucket and changes the objects from private to public if necessary.  It should not make any change to the ACL if the object is not public.  Also, if the bucket is tagged isPublic = True, then it should not do anything to the object ACLs, even if they are public.

3) Once we've tested step 1 and 2, we can create a lambda that lists all of the buckets, and then for each bucket, sends a message to the SQS queue for each bucket it sees.  This will allow us to have multiple lambdas running at once, each looking at a different bucket.

@@@@@@@@@@@@@@@@@@@@@@@

What do the HTTP status codes, such as 403, 404, 500, mean?
Web Hosting Basic knowledge
For every request from a webbrowser the server responds with a status code. If there was a error, you can get additional information about the error. You can find the most frequent error codes and a brief description in the list below.
#
HTTP Error 400 - Bad Request
The server can't process the request due to clientside errors.
#
HTTP Error 401 - Unauthorized
The 401 status code indicates that the HTTP request has not been applied because it lacks valid authentication credentials (usually username and password) for the target resource.
If the request included authentication credentials, the 401 response indicates that authorization has been refused for those credentials. Please check if your username and password are correct.
#
HTTP status 403 - Forbidden
This is a permissions issue. You often encounter this error when no index file (.htm, .html or .php) is present and the directory listing is off for a folder in the Web space (Line "Options -Indexes" in a .htaccess file).
Sometimes user authentication was provided, but the authenticated user is not permitted to view the content of the folder or file. Other times the operation is forbidden to all users. Sometimes this error occurs if there are too many connections at the same time. The easyname support team can explain you this issue in depth.
#
HTTP status 404 - Not Found
This error message is shown when a site or folder on a server are requested but cannot be found at the given URL. Please check your input.
Please note that this error can also appear if there is no start file (index.php or index.html).
#
HTTP Error 408 - Request Timeout
The server took longer than it's allocated timeout window. In this case the server terminates the connection.
#
HTTP status 429 - Too Many Requests
The HTTP 429 Too Many Requests response status code indicates the user has sent too many requests in a given amount of time.
A Retry-After header might be included to this response indicating how long to wait before making a new request. For example if more than 50 requests are received from the same IP address (cumulative hits) within the same second, our server will block that IP for the next 10 minutes as a security measure.
#
HTTP status 500 - Internal Server Error
This is a "catch all" status for unexpected errors. The server side error message is commonly caused by eg. misconfigured .htaccess files or PHP errors, which you you can check in the file php_error.log on your Webhost.
You can find the php_error.log file in the /log/ directory - this directory can be found on the same level as your /html/ directory
#
HTTP status 502 - Bad Gateway
This HTTP status code indicates, that under the specified URL there's no content to be displayed.
#
HTTP status 503 - Service unavailable
This means, that the server is currently unavailable or the server is overallocated. You can check the file php_error.log as described for the status code 500.
Should you not find helpful error messages in the logfile, please try changing the session_cache to the option filesystem, you can do this in the easyname control panel if you navigate to [Web Hosting] → [PHP settings] and click the link "Settings".
Please note that this change will take up to 15 minutes to take effect, so please try waiting 15 minutes before trying to call up your site and refresh it.
#
HTTP status 504 - Gateway timeout
This means, that the server has not responded within the specified time period.

@@@@@@@@@@@@@@@@@@@@@@@

Paytm:

Importance of Elastic Search
VPC Architecture 
Shell Scripting: remove the duplicate word from a file.
Ansible:
Check nginx service (test)
Installed if it’s not present nginx 
Copy the configuration file 
Check the nginx syntax 
If ok then proceed else stopped 
Difference between ALB and ELB/CLB
Docker: 
Can we use CMD and ENTRYPOINT both and how it is useful
Boto3 modules 
How can 2 services interacting each other inside AWS

Prometheus monitoring tool
Suppose, I don’t want to kill the parent process ID but I want to kill all the child process recursively, Shell script/python 
Ansible dynamic inventory file
Update resume 

—————————————————————————————————————————————————————————————————

Scripted Vs Declarative Pipeline:

￼
￼

—————————————————————————————————————————————————————————————————

What kind of monitoring / Alerting you are using in your current organisation ?

FILEBEAT -> LOGSTASH -> ELASTIC SEARCH -> KIBANA

Filebeat: Installed on client servers that will send their logs to logstash, 
Filebeat acts as a log shipping agent that utilizes the lumberjack networking protocol to communicate with Logstash

Logstash: server component that processes incoming logs

Elasticsearch: stores all the logs

Kibana: web interface for searching and visualizing logs, which will be proxied through Nginx

Filebeat: Installed on client servers that will send their logs to logstash, 
Filebeat acts as a log shipping agent that utilizes the lumberjack networking protocol to communicate with Logstash



Prometheus?

—————————————————————————————————————————————————————————————————

Static Ansible Inventory File:

$ cat inventory.txt 

[web]
server1.company.com ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Linux$Password
server2.company.com ansible_host=server2.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Linux$Password

[cq]
server3.company.com ansible_host=server3.company.com ansible_connection=ssh ansible_user=admin
server4.company.com ansible_host=server4.company.com ansible_connection=ssh ansible_user=admin

[db]
server5.company.com ansible_host=server5.company.com ansible_connection=ssh ansible_user=admin

[mail]
server6.company.com ansible_host=server6.company.com ansible_connection=winrm ansible_user=root ansible_password=Win$Password
server7.company.com ansible_host=server7.company.com ansible_connection=winrm ansible_user=root

[jenkins]
server8.company.com ansible_host=server8.company.com ansible_connection=ssh ansible_user=admin

#CREATE GROUPS
[web-db-groups]
web
db

[db-jenkins-server]
db
jenkins

[all_servers:children]
web
cq
db
mail
jenkins

[group1]
server9.company.com ansible_host=server9.company.com ansible_connection=winrm ansible_user=root

[group2]
server1.company.com ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Linux$Password
server5.company.com ansible_host=server5.company.com ansible_connection=ssh ansible_user=admin

#INFORMATION OF LOCALHOST
localhost ansible_connection=localhost
Javeds-MacBook-Air:Lab-1 javedalam$ 

$ sensible all -i <path-of-inventory> <path-of-yml-file>
—————————————————————————————————————————————————————————————————

Explain dynamic inventory and its use cases in ansible ?

Ansible Static Inventory File:
https://www.linuxtechi.com/manage-ansible-static-and-dynamic-host-inventory/

Ansible Dynamic Inventory File:
https://www.jeffgeerling.com/blog/creating-custom-dynamic-inventories-ansible

Ansible Dynamic Inventory Scripts:
https://github.com/ansible/ansible/tree/devel/contrib/inventory

—————————————————————————————————————————————————————————————————

What are ansible facts , can we customise them , how to use them ? COMPLETE THIS

https://www.paulinomreyes.com/?p=39

￼

—————————————————————————————————————————————————————————————————

AWS Lambda:

https://www.paulinomreyes.com/?cat=38

—————————————————————————————————————————————————————————————————

How we use modules in terraform & what is the benefit of modules in terraform ?

Solution:
https://medium.com/@mitesh_shamra/module-in-terraform-920257136228

Modules can’t inherit or reference parent resources, we need to pass them to the module explicitly as input variables. Modules are self-contained packages which can be shared across teams for different projects.

Example:
https://registry.terraform.io/modules/terraform-aws-modules/vpc/aws/2.24.0

module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "2.24.0"
  # insert the 8 required variables here
}

To run this:
$ terraform init
$ terraform plan
$ terraform apply
—————————————————————————————————————————————————————————————————

Scripting questions to automate day to day tasks (cloud watch, cost scripts)

Automate Cloud Watch Monitoring:
I have several dashboards in CloudWatch that represent a view of my infrastructure: Number of instances from an autoscaling-group that are currently running, the CPU/Disk usage per instance, etc. However, when I update an autoscaling-group, I have to manually update the dashboards (autoscaling-group ID) to include its EC2 instances in the display. I'm looking for some kind of metric/dimension that can filter autoscaling-groups by tag. Is it possible, if yes then how? if no, how can I make it differently?

You can build lambda function to do this job.
Configure lambda function to trigger every few minutes and check the autoscaling group for addition/removal of instances and update the cloudwatch dashboard accordingly
1 . Create a lambda function to check the instance present in the ASG and update the CW dashboard based on the instances present in the dashboard.
2 . Create a cloudwatch rule to trigger the lambda function every 5/10 minutes

Automate Cost Scripts:
https://www.helpsystems.com/blog/how-build-automation-scripts-without-code



—————————————————————————————————————————————————————————————————

Design Pure CI/CD Designs:

Solution:
Declarative Pipeline By Me:
Git > Jenkins > Maven + Sonarqube + JFrog Artifactory > Docker > Docker Swarm

—————————————————————————————————————————————————————————————————

Design Pure CI/CD Designs:

https://www.purestorage.com/content/dam/pdf/en/white-papers/wp-a-modern-ci-cd-pipeline.pdf

￼

—————————————————————————————————————————————————————————————————

Design Pure CI/CD Designs:


https://semaphoreci.com/cicd

￼



—————————————————————————————————————————————————————————————————

Section: Linux Concepts

What is the sequence of steps that occur when a Linux computer is powered up ?

Solution:
https://www.thegeekstuff.com/2011/02/linux-boot-process/
￼

—————————————————————————————————————————————————————————————————

How do you check if your filesystems are running out of space ? 

Solution:
https://www.tecmint.com/how-to-check-disk-space-in-linux/

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df
Filesystem    512-blocks      Used Available Capacity iused               ifree %iused  Mounted on
/dev/disk1s1   236568496 158715936  66035488    71% 1473064 9223372036853302743    0%   /
devfs                379       379         0   100%     656                   0  100%   /dev
/dev/disk1s4   236568496  10485976  66035488    14%       5 9223372036854775802    0%   /private/var/vm
map -hosts             0         0         0   100%       0                   0  100%   /net
map auto_home          0         0         0   100%       0                   0  100%   /home

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df # fs disk space
Filesystem    512-blocks      Used Available Capacity iused               ifree %iused  Mounted on
/dev/disk1s1   236568496 158706752  66044672    71% 1473064 9223372036853302743    0%   /
devfs                379       379         0   100%     656                   0  100%   /dev
/dev/disk1s4   236568496  10485976  66044672    14%       5 9223372036854775802    0%   /private/var/vm
map -hosts             0         0         0   100%       0                   0  100%   /net
map auto_home          0         0         0   100%       0                   0  100%   /home

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -a # all file disk space
Filesystem    512-blocks      Used Available Capacity iused               ifree %iused  Mounted on
/dev/disk1s1   236568496 158707480  66043944    71% 1473065 9223372036853302742    0%   /
devfs                379       379         0   100%     656                   0  100%   /dev
/dev/disk1s4   236568496  10485976  66043944    14%       5 9223372036854775802    0%   /private/var/vm
map -hosts             0         0         0   100%       0                   0  100%   /net
map auto_home          0         0         0   100%       0                   0  100%   /home

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -h # space usage in human readable format
Filesystem      Size   Used  Avail Capacity iused               ifree %iused  Mounted on
/dev/disk1s1   113Gi   76Gi   31Gi    71% 1473065 9223372036853302742    0%   /
devfs          190Ki  190Ki    0Bi   100%     656                   0  100%   /dev
/dev/disk1s4   113Gi  5.0Gi   31Gi    14%       5 9223372036854775802    0%   /private/var/vm
map -hosts       0Bi    0Bi    0Bi   100%       0                   0  100%   /net
map auto_home    0Bi    0Bi    0Bi   100%       0                   0  100%   /home

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -hT # /home/file system
df: option requires an argument -- T
usage: df [-b | -H | -h | -k | -m | -g | -P] [-ailn] [-T type] [-t] [filesystem ...]
Javeds-MacBook-Air:iPhone Software Updates javedalam$ 

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -k # in bytes
Filesystem    1024-blocks     Used Available Capacity iused               ifree %iused  Mounted on
/dev/disk1s1    118284248 79355292  33020420    71% 1473066 9223372036853302741    0%   /
devfs                 189      189         0   100%     656                   0  100%   /dev
/dev/disk1s4    118284248  5242988  33020420    14%       5 9223372036854775802    0%   /private/var/vm
map -hosts              0        0         0   100%       0                   0  100%   /net
map auto_home           0        0         0   100%       0                   0  100%   /home

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -m # fs in mb
Filesystem    1M-blocks  Used Available Capacity iused               ifree %iused  Mounted on
/dev/disk1s1     115511 77495     32246    71% 1473070 9223372036853302737    0%   /
devfs                 0     0         0   100%     656                   0  100%   /dev
/dev/disk1s4     115511  5120     32246    14%       5 9223372036854775802    0%   /private/var/vm
map -hosts            0     0         0   100%       0                   0  100%   /net
map auto_home         0     0         0   100%       0                   0  100%   /home

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -g # fs in gb
Filesystem    1G-blocks Used Available Capacity iused               ifree %iused  Mounted on
/dev/disk1s1        112   75        31    71% 1473070 9223372036853302737    0%   /
devfs                 0    0         0   100%     656                   0  100%   /dev
/dev/disk1s4        112    5        31    14%       5 9223372036854775802    0%   /private/var/vm
map -hosts            0    0         0   100%       0                   0  100%   /net
map auto_home         0    0         0   100%       0                   0  100%   /home

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -i # fs in Inodes
Filesystem    512-blocks      Used Available Capacity iused               ifree %iused  Mounted on
/dev/disk1s1   236568496 158704784  66046640    71% 1473070 9223372036853302737    0%   /
devfs                379       379         0   100%     656                   0  100%   /dev
/dev/disk1s4   236568496  10485976  66046640    14%       5 9223372036854775802    0%   /private/var/vm
map -hosts             0         0         0   100%       0                   0  100%   /net
map auto_home          0         0         0   100%       0                   0  100%   /home

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -T # fs type
df: option requires an argument -- T
usage: df [-b | -H | -h | -k | -m | -g | -P] [-ailn] [-T type] [-t] [filesystem ...]
Javeds-MacBook-Air:iPhone Software Updates javedalam$ 

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -t /etx

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -t ext3
Javeds-MacBook-Air:iPhone Software Updates javedalam$ 

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -t /dev/disk1s1
df: /dev/disk1s1: Raw devices not supported

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df -x ext3
df: illegal option -- x
usage: df [-b | -H | -h | -k | -m | -g | -P] [-ailn] [-T type] [-t] [filesystem ...]

Javeds-MacBook-Air:iPhone Software Updates javedalam$ df --help
df: illegal option -- -
usage: df [-b | -H | -h | -k | -m | -g | -P] [-ailn] [-T type] [-t] [filesystem ...]
Javeds-MacBook-Air:iPhone Software Updates javedalam$ 

—————————————————————————————————————————————————————————————————

How do you print a list of the largest files? 

Solution:
http://go2linux.garron.me/linux/2010/11/how-list-or-find-largest-files-and-directories-folders-linux-free-disk-space-850/

$ du -hs */ | sort -nr | head		# biggest top folders in your disk

$ du -sm * | sort -nr | head -40	# biggest top 40 folders in your disk

$ ls -lS | head 				# biggest file inside folders

$ find -type f -ls | sort -k 7 -r -n | head -5		# biggest files in any folder

$ find / -type f -ls | sort -k 7 -r -n | head -5	# biggest files in any folder

$ find . -type f -mtime +3 -name “*.txt” -exec rm {}\;				# used to fetch the files older than 3 days

$ find . -type f -mtime +3 -name “*[0-9][a-z][A-Z]” -exec rm {}\;		# used to fetch the files older than 3 days

—————————————————————————————————————————————————————————————————

How do you delete all .mov files larger than 1 GB?

Solution:

https://unix.stackexchange.com/questions/287629/find-and-remove-files-bigger-than-a-specific-size-and-type/287633

$ find ./ -size +1M | xargs rm

$ find / type f \( -name “*zip” -o -name “*.tar” -name “*gz” \) -delete

$ find / type f \( -name “*zip” -o -name “*tar” -name “*gz” \) -size +1M -delete

$ find / type f \( -name “*zip” -o -name “*tar” -name “*gz” \) -size +1M -exec rm {}\;	# if delete does not support

$ find . type f ! -name “*.mp3” ! -name “*.mp4” -size +1M -delete		# exclude mp3, mp4 files

$ find . type f ! -name “*.mp3” ! -name “*.mp4” -size +1M -exec rm {}\;	# if delete does not support

—————————————————————————————————————————————————————————————————

What is swappiness in Linux ?

Solution:
https://www.howtogeek.com/449691/what-is-swapiness-on-linux-and-how-to-change-it/

Swapping is a technique where data in Random Access Memory (RAM) is written to a special location on your hard disk—either a swap partition or a swap file—to free up RAM.

—————————————————————————————————————————————————————————————————

Section: Debugging (Junior to Mid Level Engineer)

What happens when you type google.com into your browser that causes a web page to return to you? 

Solution:
https://www.youtube.com/watch?v=PyzBe6cUgNI

https://dev.to/antonfrattaroli/what-happens-when-you-type-googlecom-into-a-browser-and-press-enter-39g8

“What happens when you type in a URL” is a deceptive question commonly asked in tech interviews. If you look online, there are many very detailed resources but few concise explanations of how a web browser, a server, and the general internet work together.

This is how I would explain it:
	1.	You enter a URL into a web browser
	2.	The browser looks up the IP address for the domain name via DNS
	3.	The browser sends a HTTP request to the server
	4.	The server sends back a HTTP response
	5.	The browser begins rendering the HTML
	6.	The browser sends requests for additional objects embedded in HTML (images, css, JavaScript) and repeats steps 3-5.
	7.	Once the page is loaded, the browser sends further async requests as needed.

That’s really it. Here’s a description in words for this site.
When you type “https://wsvincent.com” into your browser the first thing that happens is a Domain Name Server (DNS) matches “wsvincent.com” to an IP address. Then the browser sends an HTTP request to the server and the server sends back an HTTP response. The browser begins rendering the HTML on the page while also requesting any additional resources such as CSS, JavaScript, images, etc. Each subsequent request completes a request/response cycle and is rendered in turn by the browser. Then once the page is loaded some sites (though not mine) will make further asynchronous requests.
If I were asked to explain further I might start talking about how the server and browser connect via TCP. And we could discuss encryption via https, too.

—————————————————————————————————————————————————————————————————

DNS Explained:

https://www.youtube.com/watch?v=72snZctFFtA

—————————————————————————————————————————————————————————————————

What's the difference between a hard link and a soft link' ?

Solution:
https://medium.com/@krisbredemeier/the-difference-between-hard-links-and-soft-or-symbolic-links-780149244f7d

https://www.geeksforgeeks.org/soft-hard-links-unixlinux/

Soft Link or Symbolic links
1. Soft Links have different inodes numbers.
2. ls -l command shows all links with second column value 1 and the link points to the original file.
3. Soft Link contains the path for original file and not the contents.
4. Removing soft link doesn't affect anything but when the original file is removed, the link becomes a 'dangling' link that points to nonexistent file.
5. A Soft Link can link to a directory.
	•	Command to create a Soft link is:$ ln  -s [original filename] [link name] 
Hard Links
1. Hard Links have same inodes number.
2. ls -l command shows all the links with the link column showing the number of links.
3. Links have actual file contents
4. Removing any link, just reduces the link count but doesn't affect the other links.
5. You cannot create a Hard Link for a directory.
	•	Even if the original file is removed, the link will still show you the contents of the file.Command to create a hard link is:$ ln  [original filename] [link name] 

—————————————————————————————————————————————————————————————————

What if the web page doesn’t appear — how do you debug the problem ?

Solution:
	•	403 Forbidden: You’re not allowed to access this page. Check the address and try again.
	•	404 Page Not Found: The page you’re trying to access no longer exists. Check the address and try again. This could mean the webmaster has moved the page, or something has broken.
	•	500 Internal Server Error: There’s a problem with the server that hosts the website. This isn’t something you can resolve, so try again later.

https://serverfault.com/questions/233333/how-to-debug-website-that-isnt-loading

$ telnet your.server.name 80

$ telnet www.google.com 80
 Trying 74.125.95.103...
 Connected to www.l.google.com.
 Escape character is '^]'.

$ telnet fake.dns.entry 80
telnet: could not resolve fake.dns.entry/80: Name or service not known

$ telnet serverfault.com 99
Trying 64.34.119.12...
telnet: Unable to connect to remote host: Connection timed out

$ telnet 192.168.0.237
Trying 192.168.0.237...
telnet: Unable to connect to remote host: No route to host

Check the logs:
tail -f /var/log/nginx/access_log 
less /var/log/nginx/error_log

—————————————————————————————————————————————————————————————————

Given an Nginx/Apache web server log(s), how many requests are made per day?
View level of traffic with Apache access log

Solution:
https://www.inmotionhosting.com/support/uncategorized/view-level-of-traffic-with-apache-access-log/

 STEPS:
Login to your server via SSH

cd ~userna5/access-logs

Run the following command to view what Apache access logs are currently in the directory:
ls -lahtr
drwxr-xr-x 3 root at0m 4.0K Dec 31 16:47 .
drwx--x--x 9 root wheel 4.0K Jan 4 06:01 ..
-rw-r----- 2 root at0m 15K Jan 9 05:09 ftp.example.com-ftp_log
-rw-r----- 2 root at0m 3M Jan 23 13:10 example.com

	•	View Apache requests per day

awk '{print $4}' example.com | cut -d: -f1 | uniq -c		
You should get back something like this:
6095 [20/Jan/2013
7281 [21/Jan/2013
6517 [22/Jan/2013
5278 [23/Jan/2013
	•	View Apache requests per hour

grep "23/Jan" progolfdeal.com | cut -d[ -f2 | cut -d] -f1 | awk -F: '{print $2":00"}' | sort -n | uniq -c		
You should get back something like this:
200 00:00
417 01:00
244 02:00
242 03:00

	•	View Apache requests per minute

grep "23/Jan/2013:06" example.com | cut -d[ -f2 | cut -d] -f1 | awk -F: '{print $2":"$3}' | sort -nk1 -nk2 | uniq -c | awk '{ if ($1 > 10) print $0}'

Extra:
Features	NGINX	Apache
Access log location	/var/log/nginx/access.log	/var/log/apache/access.log
Error log location	/var/log/nginx/error.log	/var/log/apache/error.log
Can access log format be modified?	Yes	Yes
Can error log format be modified?	No	Yes

Conclusion
While NGINX and Apache are wildly different web servers, both of their logging approaches are relatively the same. The advantage to this is that there is no real inherent logging benefit to using one server over the other, which gives you the ability to change servers with minimal changes to your application monitoring infrastructure. Regardless of the similarities in logging approach, however, what’s important in the end is the value of the information provided, not the format it is presented in.

—————————————————————————————————————————————————————————————————

Create bash load monitoring script
https://www.inmotionhosting.com/support/website/server-usage/create-server-load-monitoring-bash-script/
#!/bin/bash 
trigger=4.00 
load=`cat /proc/loadavg | awk '{print $1}'` 
response=`echo | awk -v T=$trigger -v L=$load 'BEGIN {if ( L > T){ print "greater"}}'` 
if [[ $response = "greater" ]] then 
	sar -q | mail -s"High load on server - [ $load ]" recipient@example.com 
fi

—————————————————————————————————————————————————————————————————

Which IPs are the most frequent visitors ? Which pages are the most requested?

Solution:
I was wondering if it is possible to see the IP addresses of the most frequent site visitors? There are some competitors spying on my websites, and I wanted to block them from visiting (via .htaccess or other means). I wanted to find out if there is a way to see which IP visits my site the most, and frequently, and block the entire subnet.

You can install a independent visitor tracker like tracewatch that will tell you wich ip is very frequently visiting your site and wich pages they look at.
http://www.tracewatch.com/

—————————————————————————————————————————————————————————————————

Sample Log Format (delimited by whitespace)

$response_code $remote_ip $request_uri

—————————————————————————————————————————————————————————————————

Section : Data Structures & Algorithms

Find missing number in a sorted array of 1 to 100

Solution:
https://www.geeksforgeeks.org/find-the-missing-number/

# getMissingNo takes list as argument 
def getMissingNo(A): 
	n = len(A) 
	total = (n + 1)*(n + 2)/2
	sum_of_A = sum(A) 
	return total - sum_of_A 

# Driver program to test above function 
A = [1, 2, 4, 5, 6] 
miss = getMissingNo(A) 
print(miss) 
# This code is contributed by Pratik Chhajer 

OR

>>> def get_missing_no(A):
...     n = len(A)
...     total = (n+1)*(n+2)/2
...     sum_of_A = sum(A)
...     return total - sum_of_A
... 
>>> 
>>> A = [1,2,4,5,6]
>>> miss = get_missing_no(A)
>>> print(miss)
3.0
>>> print(int(miss))
3

—————————————————————————————————————————————————————————————————

Remove all duplicates from a list ?

Solution:
https://www.geeksforgeeks.org/python-remove-duplicates-list/

>>> 
>>> def remove(duplicate):
...     final_list = []
...     for num in duplicate:
...             if num not in final_list:
...                     final_list.append(num)
...     return final_list
... 
>>> remove([1,2,3,3])
[1, 2, 3]
>>> 
>>> duplicate = [1,2,3,3]
>>> remove(duplicate)
[1, 2, 3]
>>> 
>>> rd = remove(duplicate)
>>> rd
[1, 2, 3]
>>> print(rd)
[1, 2, 3]
>>> 

—————————————————————————————————————————————————————————————————

Write a function to find the two maximum response times in a log file?

Solution:
https://unix.stackexchange.com/questions/310606/need-to-find-a-response-time-which-takes-from-1-3-seconds-in-apache-logs

—————
I came up with below code using grep, sed and awk commands, which is printing average response time for each log file.

for file in *; do 
    if [ -f "$file" ]; then 
        cat $file | grep ".*Eligible programs received from program service for user .*" | sed -E -n "s/.*Eligible programs received from program service for user .* in (.*) ms.*/\\1/p" | awk '{ SUM += $1; COUNT += 1;} END { print SUM/COUNT }'
    fi 
done
—————

I need to find the API response time from an Apache log file. It's like a response time which is takes between 1 to 2 secound or 2 to 3 second. $6 is response time and values comes in microseconds.

I am trying with following command but the output is always the same:

$ grep 17/Sep/2016:10 /access.log | awk '{ print ($6 > 1000000 && 2000000 > $6) }' | wc -l

This question would be clearer if some lines of access.log were added as a sample. Anyway, the awk command prints a line regardless of the value of $6, so when you count the lines with wc -l you get an outcome that is determined by grep alone.
If you want to count the lines where is $6 is between two different values you can write

$ grep 17/Sep/2016:10 /access.log | awk '$6 > 1000000 && 2000000 > $6' | wc -l

However, this pipeline is a bit inefficient. It would almost always be preferable to combine it in a single awk command like this:

$ awk '/17\/Sep\/2016:10/ && $6 > 1000000 && 2000000 > $6 {c++} END{print c}' access.log

To include the boundaries one can do:

$ grep 18/Sep/2016:11 /access.log | awk ' $6>=1000000 && $6<=2000000' | wc -l

or equivalently

$ awk '/18\/Sep\/2016:11/ && $6>=1000000 && $6<=2000000 {c++} END{print c}' access.log

—————————————————————————————————————————————————————————————————

Explain the output of the top command in Linux?

Solution:

https://www.fastwebhost.in/blog/what-is-top-command-and-how-to-read-top-command/

￼


—————————————————————————————————————————————————————————————————

Difference between Network & Application load balancer ?

Solution:
ALB can only handle HTTP/HTTPS requests, unlike the NLB that can handle any type of TCP requests.
ALB is at layer 7 on the OSI model -- this means it exists at the application level -- and the NLB is at layer 4 which means it works at the transport level.

—————————————————————————————————————————————————————————————————

Write a shell/python code to print factorial for any given number.

Solution:
def factorial(n): 	

	return 1 if (n==1 or n==0) else n * factorial(n - 1); 

num = 5; 
print("Factorial of",num,"is", 
factorial(num)) 

—————————————————————————————————————————————————————————————————————————

Lambda Service:

https://aws.amazon.com/blogs/networking-and-content-delivery/using-static-ip-addresses-for-application-load-balancers/

—————————————————————————————————————————————————————————————————————————

Section: Design (Senior Candidates) & Scalability

Design Youtube (where one can upload videos and consume videos).
https://www.geeksforgeeks.org/design-video-sharing-system-like-youtube/

Design Whatsapp.
https://www.youtube.com/watch?time_continue=15&v=jN1pnBVIj7M&feature=emb_logo
https://codetiburon.com/create-chat-app-like-whatsapp/

Design Netflix:
https://www.youtube.com/watch?v=psQzyFfsUGU

—————————————————————————————————————————————————————————————————————————

Case Study or Assignment :

Describe the architecture to build & deploy a simple web application on AWS that will help
students of Delhi University computer science department in digitalization by developing secure, robust
and cloud hosted web portal.

Objective:

• 500 students from computing department will use this portal to submit 500 word weekly reports in PDF
format.
• Uploaded files must be automatically renamed to "<student_name>_<week>_<year>.pdf" based on the
students who uploaded the file and the week for which the report was meant.
• Existing documents with the same name may be replaced by newer uploads.
• Portal administration interface should support searching for documents based on file names and dates
of upload.
• The documents to be securely backed up automatically every day to their Campus NFS server.
• Please describe the architecture, technology stack, programming language you would use to build the
application and why you chose them.
Opportunity:
• The web portal should be secure, robust and hosted on cloud - AWS
• Adopt best practices of DevOps across application as well as IT infrastructure.

Note :-

• Application and Infrastructure completely hosted in "AWS Mumbai Region" or “Azure Central India”

—————————————————————————————————————————————————————————————————————————

text.txt
Displaying text.txt.

---

Interview Questions for Ansible, Docker and Python:

Shell Script to list the name of files in a certain path ?
#!/bin/sh
for i in `ls -lar *.*`
do
echo $i
done

Algorithm to use in Elastic Load Balanacer ?

How Autoscaling is configured and alogorithm used at the backend ?

How Autoscaling is configured ?
Create Launch Configuration -> Choose AMI, InstanceType, Configure Details, Security Groups and KeyPair => Launch it
aws autoscaling create-launch-configuration --launch-configuration-name my-launch-config --placement-tenancy dedicated --image-id ...
aws autoscaling describe-launch-configurations --launch-configuration-names my-launch-config
aws autoscaling create-launch-configuration --launch-configuration-name classiclink-config --image-id ami_id --instance-type instance_type \
--classic-link-vpc-id vpc_id --classic-link-vpc-security-groups group_id
aws autoscaling update-auto-scaling-group --auto-scaling-group-name my-asg --launch-configuration-name classiclink-config

Read the whole Auto Scaling Documentation ?

Have you ever Hosted any WebApplication in AWS or Normal ? => Through Docker only

Alogorithm used in Auto Scaling ?
autoscaler_task_interval 60000;
min_app_instances  1;
server_startup_delay 180000;
max_requests_per_second   5;
rounds_to_average       2;
alarming_upper_rate 0.7;
alarming_lower_rate 0.2;
scale_down_factor 0.25;

Which language comes in the output of Ansible ? => JSON

How DNS resolution work ?

Ansible Roles Architecture ?

How to handle multiple yml playbooks ? Include module

How to put condition in Ansible ? When
tasks:
  - name: "shut down Debian flavored systems"
    command: /sbin/shutdown -t now
    when: ansible_os_family == "Debian"

List of modules which you have worked ? Need to go in depth
when, yum, command, become, tasks, accelerate, 

How to check Docker Container is up or down ? $ docker ps -a -q

List the Values in ascending order and keys in any order in Python ?

Fetch the string from a list only without list comprehension ? a = [1,"one",2] => one

How SNS work in AWS and how you have configured in your Project ? Read SNS AWS Article

What is the maximum no of nodes which you have configured in Ansible Playbook ? 20+

Ansible or Puppet which one is better and why ? Ansible because no Master and Agent concept, Pull Concept, Less time 

Directory structure for Roles in Ansible ?
site.yml
webservers.yml
fooservers.yml
roles/
   common/
     tasks/
     handlers/
     files/
     templates/
     vars/
     defaults/
     meta/
   webservers/
     tasks/
     defaults/
     meta/

Have you created any Docker file by your own elaborate it ? Yes, for Jenkins and MySQL

Which mandatory module you have to implement in REST Python API ? 
Import os
pip install py-rest-client

Which module you need to implement to interact the AWS Services or for AWS Automation ? boto or boto3

Structure for copy module in Ansible while copying multiple files from local to remote machine ?
- copy:
    src: /srv/myfiles/foo.conf
    dest: /etc/foo.conf
    owner: foo
    group: foo
    mode: 0644

Why and how you have implemented the Cloud Watch Monitoring ? Read AWS Cloud Watch Monitoring
To enable all actions for an alarm => aws cloudwatch enable-alarm-actions --alarm-names myalarm

Why we use handlers module in Ansible ? To restart any service
---
- hosts: webservers
  vars:
    http_port: 80
    max_clients: 200
  remote_user: root
  tasks:
  - name: ensure apache is at the latest version
    yum: name=httpd state=latest
  - name: write the apache config file
    template: src=/srv/httpd.j2 dest=/etc/httpd.conf
    notify:
    - restart apache
  - name: ensure apache is running (and enable it at boot)
    service: name=httpd state=started enabled=yes
  handlers:
    - name: restart apache
      service: name=httpd state=restarted

What is the data type for class in Python ?

Have you worked on Ansible with Docker ? No

Command to install Docker in OS ? Mac => sudo easy_install docker 

Pre-requisites to install Docker => Python would be must

Difference between List and Tuple ?
List is Mutable and Tuple is Immutable

Where have you used list and tuple in your project ?
Useless question

How to fetch the unique elements in Python ? => set

Is string is a mutable to immutable ? mutable 

In Dictionary, will the data will print the way you insert ? Need to verify 

Which Algorithm used at the backend of Dictionary in Python ? Hashmap Techniques

How Elastic Search work and where you have used ? => Kibana and Splunk i have used 

List comprehension in Python and give me the type of string ? 
A = [ print(i) for i in range(10) ]
Print(A)

How iterator works in Python ? Iterator used to iterate the array elements
# define a list
my_list = [4, 7, 0, 3]
# get an iterator using iter()
my_iter = iter(my_list)
## iterate through it using next() 
#prints 4
print(next(my_iter))
#prints 7
print(next(my_iter))
## next(obj) is same as obj.__next__()
#prints 0
print(my_iter.__next__())
#prints 3
print(my_iter.__next__())
## This will raise error, no items left
next(my_iter)

What is SLA ? 
A service-level agreement (SLA) is a document describing the level of service expected by a customer from a supplier, laying out the metrics by which that service is ... However, it's recommended that the client and the outsourcing company work together during the SLA contract negotiation to eliminate any ...

Which algorithm it worked at the backend of SLA ?
Interleaved Polling Algorithm

Have you ever created any certificate ? Yes, through openssl command
The commands below can be used to view the certificate fingerprint/thumbprint.
• SHA-256: openssl x509 -noout -fingerprint -sha256 -inform pem -in [certificate-file.crt] 
• SHA-1: openssl x509 -noout -fingerprint -sha1 -inform pem -in [certificate-file.crt]
• MD5: openssl x509 -noout -fingerprint -md5 -inform pem -in [certificate-file.crt] 

What is the demerits and merits while creating a certificate by our own ?
Advantages
1. No PKI (Public Key Infrastructure) is needed.
2. Automatic deployment (Usually Self-signed certificates created automatic during the installation process of the server side applications).
Disadvantages
1. The certificates aren’t trusted by other applications/operating systems. This may lead to authentications errors etc.
Note: To overcome this limitation, some IT staff add the self-signed certificates to the Trusted Roots Certificate Authorities. However, using this workaround may to additional time that needed for management and troubleshooting.
2. Self-signed certificates life time is usually 1 years. Before the year is ended, the certificate may need to renew/replace.
3. Self-signed certificates may use low hash and cipher technologies. Due this, the security level that implemented by self-signed certificates may not satisfy the current Security Policy etc. .
4. No support for advanced PKI (Public Key Infrastructure) functions (e.g. Online checking of the revocation list etc.).
5. Most of the advanced feathers of the server side applications required to impended a PKI (Public Key Infrastructure). By this, self-signed certificates advantages can't be used.

What is ca-certificates  and in which Algorithm it worked ?
CA certificates can also be used to establish trust relationships between CAs in two different public key infrastructure (PKI) hierarchies.
Root CA Certificate 
	Issuing CA Certificate
		User Certificate
The following are some of the trust scenarios that can be enabled by properly configured CA certificates:
	• Simple trust within an enterprise PKI
	• Cross trust between two enterprise CAs (restricted)
	• Bridge trust for multiple enterprise PKIs (unrestricted)
	• Certificate trust continuity when the certificate policy changes

Have you worked in hadoop and Are you good in SQL Queries ? No, and Yes

How Ansible worked, let me know its Architecture ?


What sequence followed by Ansible while executing the playbook ?
INVENTORY (LIST OF ALL WEBSERVERS), PLAYBOOK (MENTION ALL INVENTORIES) -> THROUGH SSH IT CONNECTS WITH REMOTE NODES AND DO THE DEPLOYMENT

Have you ever worked on Dynamic Playbook ?

Have you ever worked on Dynamic Docker File ?

Installation of Ansible ?
Install packages below on server machines
$ sudo apt-get install python-yaml python-jinja2 python-paramiko python-crypto python-keyczar ansible
Install packages below on client machines
$ sudo apt-get install python-crypto python-keyczar

How to read the last word of a file ?
awk 'NF {print $NF; exit}'
OR
# Python Code to read the first and last word of a file
f = open("file_name.ext","r")
for line in f:
	words = line.split()
	print(words[-1])
OR
f = open("file_name.ext","r")	# open the file in read mode only
line = []  # create an empty list to store the lines of a file
for i in f:
	line.append(i)  # loop over the line in the file and store them in the list
for i in line:
	words_in_line=i.split()  # creates a list of the words in each line
	print(words_in_line[0],words_in_line[-1])  # print out the first and last word of each line

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Panda: Machine Learning

Three Data Structures:
Series; Data Frame; Panel

Ex_1:
import pandas as pd
import quandl 
df = quandl.get('WIKI/GOOGL')
print(df.head)

Note: 
Series: 1D (Homogeneous data; Size Immutable; Data Mutable)
Data Frame: 2D (Heterogeneous data; Size Mutable; Data Mutable)
Panel: 3D (Heterogeneous data; Size Mutable; Data Mutable)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Where we implement Auto Scaling Instance Level or ELB Level ?
Instance level

What kind of Ansible Playbook you wrote ?

Rename all files contents as "xyz" using Shell Scripting ?

What kind of automations you have done in Python ?

Difference between Git and SVN ?

What it indicates when checkout happened and meanwhile a new file would created in SVN ?

Why we used JSON ?

What happened when /boot or /root volume shows 100% ?

Can we release cache memory and how ?
sync; echo 3 > /proc/sys/vm/drop_caches

Difference between jar war and ear files in java ?
In J2EE application, modules are packaged as EAR, JAR and WAR based on their functionality
JAR: EJB modules which contain enterprise java beans (class files) and EJB deployment descriptor are packed as JAR files with .jar extenstion
WAR: Web modules which contain Servlet class files, JSP Files, supporting files, GIF and HTML files are packaged as JAR file with .war (web archive) extension
EAR: All above files (.jar and .war) are packaged as JAR file with .ear (enterprise archive) extension and deployed into Application Server.

How to create a 0 downtime deploy manually using Jenkins ?

Difference between .rb and .erb ?
erb is the extension of the template engine used to interpret the file. ... erb is the file extension for eRuby documents, which is a way of embedding Ruby into a text document. Similar to how PHP works. rb is the file extension for ruby 



Ansible Vault ?
ansible-playbook site.yml --ask-vault-pass
From <http://docs.ansible.com/ansible/latest/playbooks_vault.html> 
ansible-playbook site.yml --vault-password-file ~/.vault_pass.txt
ansible-playbook site.yml --vault-password-file ~/.vault_pass.py

How to list the variables in Ansible ?
How to fetch the environment variables in Ansible ?
Difference between Ansible and Chef ?
How Ansible used for Provisioning ?
Difference between List and Tuple ?
How Multithreading inherited in Python ?
Key features of Python ?
How Auto Scaling works in AWS ?
What you have implemented in AWS Lambda ?
Which is most recent script you worked upon ?
Git stash command ?
Git list the commit changes  ?
Git revert the changes ?
Git difference command ?
Difference between Git and SVN ?
Difference between Pull and Push in GIT ?

---
