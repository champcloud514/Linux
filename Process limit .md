Process limit Adjustment
# ssh into App Server 1
ssh tony@stapp01.stratos.xfusioncorp.com
# Update the limit configuration file
sudo vi /etc/security/limits.conf
# Add the file to the config
nfsuser    soft    nproc    ****
nfsuser    hard    nproc    ****
# check the limit
ulimit -u
## Count Total Processes for the User
ps -u <user> --no-headers | wc -l
## Set New Limit
ulimit -u 500