Once we get domain credentials, we can run BLOODHOUND. It consists of two parts: the `sharphound` collector written in C# for use on windows systems, the Bloodhound collector and the bloodhound GUI tool which allows us to upload collected data in the form of JSON file. 

#### Run bloodhound ingestor
```
sudo bloodhound-python -u 'forend' -p 'klmcargo2' -ns 172.16.5.5 -d inlanefreight.local -c all
```
#### Having problem to run bloodhound-python 
```
bloodhound-ce-python -d lab.enterprise.thm. -ns 10.10.125.178 -c All -u bitbucket -p 'littleredbucket' --dns-timeout 15
```
```
bloodhound-ce-python -d INLANEFREIGHT.LOCAL -dc ACADEMY-EA-DC01 -c All -u <username@<domain_dc> -p <pass>
```
#### Bloodhound-ce-python 
#bloodhoundingestor
```
bloodhound-ce-python -c ALL --zip -ns 10.10.11.72 -dc DC01.tombwatcher.htb -u henry -p 'H3nry_987TGV!' -d tombwatcher.htb
```
**bloodhound auth with `ccache` file (TGT)**
```
bloodhound-ce-python -ns 10.10.11.75 -d rustykey.htb -dc dc.rustykey.htb -k --dns-timeout 15 --zip -u rr.parker -no-pass
```

#### nxc
```
nxc ldap tomwatcher.htb -u henry -p H3nry_987TGV! --bloodhound -c All,LoggedOn,DCOM,DCOnly --dns-timeout 15
```

#### Run bloodhound GUI
- Download pre-compiled binaries from GitHub 
- Upload the file one by one or zip file. 
- Explore

# Sharp-hound
#### Run `sharphound` from windows 
```
.\sharphound.exe -c All,GPOLocalGroup --zipfilename trilocor.zip -d domain
```