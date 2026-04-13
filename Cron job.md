## Secure Root SSH Access Data 
# SSH into App Server
ssh <username>@<app server>
# Switch to Root user
sudo su -
## Install Cronie
yum install -y cronie
# Add the Cron job 
*/5 * * * * echo hello > /tmp/cron_text
type i,Esc,:wq and Enter
## Repeat on all 3 app servers and check with 
crontab -l + cat /tmp/cron_text.
sudo_tony ALL=(ALL) NOPASSWD:ALL