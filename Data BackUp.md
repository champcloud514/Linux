## Data BackUp for Developer
# SSH into Storage Server
ssh <username>@<app server>
# Switch to Root user
sudo su -
# Compressed the files 
tar -zcvf <name of compressed file> <folde or files to be compressed>
tar: The utility used for creating and manipulating streaming archives.

-z: Tells tar to compress the archive using gzip.

-c: Stands for Create a new archive file.

-v: (Optional) Verbose mode—it lists the files on your screen as they are being added.

-f: Specifies the Filename of the resulting archive (always put the filename immediately after this flag).
# verify the content without extracting it
tar -ztvf mark.tar.gz
# Transfer or Move files
mv <files> <destination>
