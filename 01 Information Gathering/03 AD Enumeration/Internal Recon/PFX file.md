#pfx #pfxfile
# Extract private key
```
openssl pkcs12 -in lewis.pfx -nocerts -out lewis.pem -nodes
```

# Extract cert
```
openssl pkcs12 -in lewis.pfx -nokeys -out lewis.cert -nodes
```

# Extract information from cert
```
openssl x509 -in clark.crt -text -noout
```
# Decrypt the openssl `.key` file
```
openssl rsa -in baker.key -out decrypted_baker.key -passin pass:<newpassword>
```

# Create `pfx` file from `.key` and `.crt` (certipy)
```
certipy-ad cert -cert baker.crt -key decrypted_baker.key -export -out baker_certipy.pfx
```

# Combine cert and `pem` file (openssl)
```
openssl pkcs12 -export -out 0xdf.pfx -inkey 0xdf.key -in 0xdf.pem -certfile intermediate.cert.pem
```


>You can connect to machine via evil-winrm (nxc, certipy-ad, etc)  over 5986 (SSL) port. 
