## Linux Data transfer
# SSH into App Server
ssh <username>@<app server>
# Switch to Root user
sudo su -
# copy files owned by a User preserving the directory structure
find /source/path -type f -user username -exec cp --parents {} /destination/path/ \;

# Copy files owned by a User not preserving the directory structure
find /source/path -type f -user username -exec cp {} /destination/path/ \;
# Copy only .php files owned by the User
find /source/path -type f -user username -name "*.php" -exec cp --parents {} /destination/path/ \;
