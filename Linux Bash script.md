## Linux Bash Script
# ssh into App Server 1
ssh tony@stapp01.stratos.xfusioncorp.com
#  Install zip
sudo yum install -y zip
# Prepare & Create directories - 
sudo mkdir -p /scripts /backup
# Change permission
sudo chown steve: steve /scripts /backup
# Configure passwordless SSH to Backup Server
ssh-keygen -t rsa -b 2048
ssh-copy-id clint@172.16.238.16
ssh clint@172.16.238.16 ls /backup
# Create the backup script
vi /scripts/media_backup.sh
# Paste this 
zip -r /backup/xfusioncorp_media.zip /var/www/html/media
scp /backup/xfusioncorp_media.zip clint@172.16.238.16:/backup/
# Make script executable
chmod +x /scripts/media_backup.sh
# Run the script - 
/scripts/media_backup.sh
# Final validation - 
ls /backup/xfusioncorp_media.zip (on App Server 1)
ssh clint@172.16.238.16 ls /backup/xfusioncorp_media.zip (On Backup Server)