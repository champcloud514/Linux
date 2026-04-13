## Script Execution permission
# SSH into App Server
ssh <username>@<app server>
# Switch to Root user
sudo su -
# Locate the script
ls -l /tmp/xfusioncorp.sh
# Grant Executable permission to everyone
chmod a+x /tmp/xfusioncorp.sh
or equivalently:
chmod 755 /tmp/xfusioncorp.sh
# Verify the permission
ls -l /tmp/xfusioncorp.sh


