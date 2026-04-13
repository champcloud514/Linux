## SELinux installation & Configuration 
# SSH into App Server
ssh <username>@<app server>
# Switch to Root user
sudo su -
# install SELinux 
sudo yum install selinux-policy-targeted policycoreutils setools
# Edit the config
vi /etc/selinux/config
SELINUX=enforcing or SELINUX=permissive
# Activate SELinux 
selinux-activate