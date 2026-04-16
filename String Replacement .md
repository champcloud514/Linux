String Replacement
# ssh into App Server 1
ssh tony@stapp01.stratos.xfusioncorp.com
# View the given file
sudo cat <filename:/root/nautilus.xml>
# Edit the file
sudo vi <filename:/root/nautilus.xml>
:$s/<text to replace:text>/<replacing text:LUSC>
# verify
sudo cat <filename:/root/nautilus.xml>