# Enumeration
#### Type of users
```
Administrator
Editor: who can publish and manage all posts, including others.
Author: publish and manage their own posts.
Contributor: who writes and manage their own posts but cannot publish them.
Subscriber: Who can browse posts and edit their profile.
```
#### Identify WordPress version
```
/robots.txt
curl -s https://"$domain" | grep WordPress
```
#### Login Pages 
```
/wp-admin/login.php
/wp-admin/wp-login.php
/login.php
/wp-login.php
```
#### Directories 
```
/wp-content/uploads (must check)
/wp-content/plugins
/wp-content/themes
/wp-includes (WordPress core files)
```
#### WordPress core version enumeration
>#Source code may also provide version information such as CSS, JS
```
#Press CTRL + F
#Search for "meta generator"
						OR
curl -s -X GET http://blog."$domain" | grep '<meta name="generator"'
```

---
# Manual enumeration 
> Take some time and manually browser to look through the page sources.
#### Check themes
```
curl -s -X GET "$ip" | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'wp-content\/themes' | cut -d"'" -f2
```
#### Check plugins
```
curl -s -X GET "$ip" | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'wp-content/plugins/*' | cut -d"'" -f2
```
#### Checking plugins/themes
```
curl -I -X GET http://blog."$domain"/wp-content/plugins/someplugin
```
###### Pretty print html
```
html2text
```
##### Gather version information about themes/plugins
```
/wp-content/themes/business-gravity/readme.txt
/wp-content/plugins/mail-masta/readme.txt (look at stable tag x.y.z)
```
#### Manual users enumeration
```
Go to /wp-login.php
```
# Automatic WordPress enumeration
>#NOTE: it is really important to do manual enumeration because automatic tool often miss something.
```
sudo wpscan --url "$domain" --enumerate --api-token "$wp_token"
```

# Automatic WordPress - aggressive enumeration (scan)
```
wpscan --api-token "$wp_token" --url "$domain" -e ap,vt,tt,cb,dbe,u1-10,m1-50 --plugins-detection aggressive --plugins-version-detection aggressive --detection-mode aggressive
```