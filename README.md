# 2420 assignment 2

## Step 1:
Create a DO infrastructure. This can be done be watching and following the steps done in the video called, As2 Infrastructure. 
[The Video is here](https://vimeo.com/775412708/4a219b37e7)
At the end of following these steps you should have:
- Atleast two Droplets
- A load balancer
- A firewall using the digitalOcean cloud firewall
- And a newly made VPC that is being used by both droplets.
- Make sure to use the "Web" tag while making your droplets.

## Step 2:
Next, create a new regular user on both of the new droplets that you have created. You have the option of using a different username and password for each account.. or you can use the same credentials.
These are the commands to use when making your new users, be sure to use the commands in order:
```
useradd -ms /bin/bash <name>
usermod -aG sudo <name>
rsync --archive --chown=<name>:<name> ~/.ssh /home/<name>
passwd <name>
*you will set the password for each user here*
exit

ssh -i .\.ssh\<key> <name>@<ip>
sudo vim /etc/ssh/sshd_config
SET PermitRootLogin no
*The setting you will need to change above inside the config file will not allow the root user to connect to the droplet. This is good practice.*
sudo systemctl restart ssh
exit
```
You will need to repeat that twice. Once for each droplet, in order to create a user for each droplet.

## Step 3:
Now, lets create a web server on both of the droplets. We can skip the configuration part for now.
These are the commands that you will need to run in both droplets. Must be done in order:
```
wget https://github.com/caddyserver/caddy/releases/download/v2.6.2/caddy_2.6.2_linux_amd64.tar.gz
^This command will download the .tar.gz file for the web server^

tar xvf https://github.com/caddyserver/caddy/releases/download/v2.6.2/caddy_2.6.2_linux_amd64.tar.gz
^This command will unarchive the file, which will allow you to see the executable caddy file.^

sudo chown root: caddy
^We will need to change the caddy's file owner and group to root^

sudo cp caddy /usr/bin/
^Make sure to copy the caddy file to the bin directory^
```
In the end, you directory should look something a little like this:
![image](https://user-images.githubusercontent.com/100608327/205430678-19347429-d50b-426d-b5cb-f9376341b8bd.png)
**Do not mind the red folder/file. It is the file we unarchived.**
**Also a reminder that we do not need to configure the web server just yet.**

## Step 4:
For this step, you will need to write the "web app". 
- On your local machine which is the WSL for the windows users...
- Create a directory, the directory can be called 2420-assign-two, or I used a2-2420.
- Inside of this directory, create two more directories named ***html*** and ***src***
- Inside of the ***html*** directory, create a new index.html file.
- Create a simple although, a complete html file. (Everything that an html file/document should have.)
![image](https://user-images.githubusercontent.com/100608327/205430853-885e6c33-bd18-4dc5-b9f4-1b957ab26979.png)

- Now after that is finished, go back and enter your ***src*** directory.
- Create a new node project.
![image](https://user-images.githubusercontent.com/100608327/205430903-81817ccf-1dd9-4a58-8897-9b32bb1d2896.png)

- Next be sure to create an index.js file inside your ***src*** directory.
- Add the following code to the file:
![image](https://user-images.githubusercontent.com/100608327/205430931-4caa9417-dc1f-4293-b9cb-9a5ec209d72e.png)

- Now that you have completed these steps, be sure to send both of the directories into both of your servers. This can be done by using the command:
```
rsync -r <directory_name_in_WSL> "<user_name_in_server>@<ip>:~/" -e "ssh -i /home/<username_here>/.ssh/<key_name> -o StrictHostKeyChecking=no"
```

## Step 5:

## Step 6:
In this step we are going to be installing node and npm with Volta.
These are the steps in order to do so:
```
curl https://get.volta.sh | bash
source ~/.bashrc
volta install node
which npm
volta install npm
```
**THE SOURCE COMMAND IS VERY IMPORTANT, IT IS WHAT ALLOWS US TO INSTALL NODE.**
The result should look similar:
![image](https://user-images.githubusercontent.com/100608327/205431118-e81d3be7-dafc-4636-abc8-e62868194fbc.png)

## Step 7:
In this step we will need to write and create a service file on our local machine, in order for our node application to staart.
The service file should look like this:

