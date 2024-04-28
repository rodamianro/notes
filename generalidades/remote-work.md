# REMOTE WORK

```sh
# Open a vpn tunnel using a config file(FILEPATH)
sudo openfortivpn -c [FILEPATH]
# Copy a file or directory from a remote server to local
scp -P [PORT] [USERNAME]@[IP|DOMAIN]:[REMOTE:FILEPATH|DIRPATH] [LOCALPATH]
# Connect to ssh server
ssh [IP|DOMAIN] -p [PORT] -l [USERNAME]
```
