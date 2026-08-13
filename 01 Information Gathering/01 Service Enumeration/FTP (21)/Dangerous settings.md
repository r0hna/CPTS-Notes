1. Writable access granted
2. Anonymous access

### Attacks
LFI
FTP logs attacks to RCE

# Vulnerability
 `CoreFTP before build 727` vulnerability assigned [CVE-2022-22836](https://nvd.nist.gov/vuln/detail/CVE-2022-22836).



There are many different security-related settings we can make on each FTP server. These can have various purposes, such as testing connections through the firewalls, testing routes, and authentication mechanisms. One of these authentication mechanisms is the `anonymous` user. This is often used to allow everyone on the internal network to share files and data without accessing each other's computers. With vsFTPd, the [optional settings](http://vsftpd.beasts.org/vsftpd_conf.html) that can be added to the configuration file for the anonymous login look like this:

|**Setting**|**Description**|
|---|---|
|`anonymous_enable=YES`|Allowing anonymous login?|
|`anon_upload_enable=YES`|Allowing anonymous to upload files?|
|`anon_mkdir_write_enable=YES`|Allowing anonymous to create new directories?|
|`no_anon_password=YES`|Do not ask anonymous for password?|
|`anon_root=/home/username/ftp`|Directory for anonymous.|
|`write_enable=YES`|Allow the usage of FTP commands: STOR, DELE, RNFR, RNTO, MKD, RMD, APPE, and SITE?|