ls
sudo chown root:root <filename> or sudo chmod 644 <filename>>
## Remove all permissions for <username>
sudo setfacl -m u:<username>:--- <filename>
## Grant read-only permission to <username>
sudo setfacl -m u:<username>:--- <filename>
## Verify the ACL configuration
getfacl <filename>