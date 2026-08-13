# Pass the ticket attack
# Information gathering 
#### Linux auth via port forward 
```
ssh david@inlanefreight.htb@10.10.121.11 -p 2222
```
#### Check if linux machine is domain joined 
- `sssd`
- `winbind`
#### PS - check if linux machine is domain joined
#domainjoined #linuxdomainjoined #islinuxdomainjoined
```
ps -ef | grep -I "winbind\|sssd"
```

#### Finding `ccache` files 
```
env | grep -I krb5
```
#### Listing keytab file information 
```
klist -k -t
```

### Impersonate a user with [[KeyTab files]]



