## Linux SSH Authentication
# SSH into User Host
ssh <username>@<app server>
# Switch to Root user
sudo su -
## Generate SSH key on user Host(generate key pair)
ssh-keygen -t rsa
# Copy the public key to all Servers(app01,App02,App03)
ssh-copy-id tony@<hostname>,
## verify
ssh tony@<hotname>