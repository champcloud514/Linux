## Secure Root SSH Access Data 
# SSH into App Server
ssh <username>@<app server>
# Switch to Root user
sudo su -
## locate the Config file & disable root ssh login access
vi etc/ssh/sshd-config
type i and Change PermissionRootLogin to No
Esc,:wq and Enter

