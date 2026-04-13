# Linux Commands
## Create Keypair
ssh-keygen -t rsa -b 2048 -f ~/.ssh/<my_keyname>

## creating non interactive shell
sudo useradd -m -s /sbin/nologin <username>

2. ## Create the User with Expiry
sudo useradd -e 2027-04-15 anita

3. ## Verify the Expiry Date
sudo chage -l anita

4. ## Add a user to a group
sudo useradd -G nautilus_developers kano
4a. ## add existing user to a group
sudo usermod -aG dba_users bob

5.## Create a user with home directory
useradd -M <username>

6.## disable root ssh login access
vi /etc/ssh/sshd_config
type I ,change permitrootlogin to NO
type- esc,:wq and Enter

## 7.Restart SSH 
systemctl restart sshd

## 8.Verify
sshd -T | grep permitrootlogin

## 8.a confirmation test
ssh root@app01

## 9.Display hostname info
hotnamectl
10. search for configuration files(nfs mount)
apropos "nfs mount" | grep "conf"
11.Save the name to the specified file
echo “nfsmount.conf” > /home/bob/nfs


##When you run apropos ssh and see ssh: nothing appropriate, it means your computer's "manual page index" is either empty or hasn't been built yet.
The apropos command searches a pre-built database of command descriptions. If that database is missing, it can't find anything—even common commands like ssh or ls.
Solution
sudo mandb -c
Switch to root: sudo su -

Install + start cron: yum install -y cronie && systemctl start crond && systemctl enable crond

Edit root’s crontab: crontab -e

Add: */5 * * * * echo hello > /tmp/cron_text

Repeat on all 3 app servers and check with crontab -l + cat /tmp/cron_text.

Step 1: Generate SSH Keys for thor
Log in to the Jump Host as user thor and generate a new SSH key pair.
Bash
# Log in as thor
sudo su - thor

# Generate the key (Press ENTER for all prompts to keep it truly password-less)
ssh-keygen -t rsa -b 4096
Step 2: Distribute Public Key to App Servers
You must copy thor's public key to the respective sudo users on each app server. Replace stapp0X and user with your actual server names and sudo usernames (e.g., tony, steve, banner).
Bash
# Repeat for each App Server
ssh-copy-id tony@stapp01
ssh-copy-id steve@stapp02
ssh-copy-id banner@stapp03
Step 3: Enable Password-less Sudo on App Servers
Now that thor can log in, he still needs permission to run sudo without a password. Log into each App Server and edit the sudoers file.
    1. SSH into the App Server: ssh tony@stapp01
    2. Edit the sudoers configuration: It is best practice to create a separate file in /etc/sudoers.d/ rather than editing the main file.
       Bash
       sudo visudo -f /etc/sudoers.d/thor_access
    3. Add the following line (replacing tony with the specific user for that server):
       Plaintext
       tony ALL=(ALL) NOPASSWD: ALL
To set up password-less authentication from user thor on the Jump Host to all App Servers, you need to configure two things: SSH Key-Based Authentication (to log in without a password) and Sudoers NOPASSWD (to run root commands without a password).

Step 1: Generate SSH Keys for thor
Log in to the Jump Host as user thor and generate a new SSH key pair.
Bash
# Log in as thor
sudo su - thor

# Generate the key (Press ENTER for all prompts to keep it truly password-less)
ssh-keygen -t rsa -b 4096
This creates a private key (id_rsa) and a public key (id_rsa.pub) in /home/thor/.ssh/.

Step 2: Distribute Public Key to App Servers
You must copy thor's public key to the respective sudo users on each app server. Replace stapp0X and user with your actual server names and sudo usernames (e.g., tony, steve, banner).
Bash
# Repeat for each App Server
ssh-copy-id tony@stapp01
ssh-copy-id steve@stapp02
ssh-copy-id banner@stapp03
Note: You will be asked for the user's password one last time during this step.

Step 3: Enable Password-less Sudo on App Servers
Now that thor can log in, he still needs permission to run sudo without a password. Log into each App Server and edit the sudoers file.
    1. SSH into the App Server: ssh tony@stapp01
    2. Edit the sudoers configuration: It is best practice to create a separate file in /etc/sudoers.d/ rather than editing the main file.
       Bash
       sudo visudo -f /etc/sudoers.d/thor_access
    3. Add the following line (replacing tony with the specific user for that server):
       Plaintext
       tony ALL=(ALL) NOPASSWD: ALL

Step 4: Verify the Setup
Go back to the Jump Host as user thor and test the connection to ensure you are not prompted for any passwords:
Bash
# Test SSH login
ssh tony@stapp01

# Test Sudo access (should return 'root' immediately)
ssh tony@stapp01 "sudo whoami"
