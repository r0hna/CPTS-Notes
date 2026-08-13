#### Directory fuzzing
```
ffuf -u http://"$domain"/FUZZ  -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```
				OR
```
ffuf -w /opt/useful/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ
```
				OR
```
feroxbuster -u http://jobs.trilocor.local/ -w /usr/share/seclists/Discovery/Web-Content/common.txt -x .php,.bak,.txt,.conf,.zip,.tar,.txt,.ini -n -C 404 --dont-filter
```

#### Extension name fuzzing
```
ffuf -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt -u http://"$domain"/indexFUZZ
```
#### Page name fuzzing
```
ffuf -w /opt/useful/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/blog/FUZZ.php
```

---
#### Directory Fuzzing (recursive)
```
ffuf -w /opt/useful/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v
```
				OR
```
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://"$ip"/FUZZ -recursion -recursion-depth 2 -e .php,.db,.xml,config -ic -v
```

---
---
#### Extensions for bug bounty
```
feroxbuster --url "$ip" -x list,md,txt,conf,config,bak,backup,swp,old,db,sql,asp,aspx,aspx,~asp~,py,py~,rb,rb~,php,php~,bak,bkp,cache,cgi,conf,csv,html,inc,jar,js,json,jsp,jsp~,lock,log,rar,old,sql,sql.gz,sql.zip,sql.tar.gz,sql~,swp,swp~,tar,tar.bz2,tar.gz,txt,wadl,zip,.log,.xml,.js,.json -C 404 -S 0 -t 210
```