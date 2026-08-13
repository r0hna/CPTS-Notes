# Nmap scan
```
sudo nmap "$ip" -sV -p110,143,993,995 -sC
```
# Connect with service
```
telnet "$target" <port>
```

```
curl -k "imap://$ip" --user user:password -v
curl -k "pop3://$ip" --user user:password -v
```
#### List all mails
```
curl -k "imap://$ip/INBOX?ALL" --user user:password -v
```
#### SSL
```
openssl s_client -connect "$ip":pop3s
```
```
openssl s_client -connect "$ip":imaps
```

# brute force attack
```
hydra -L /usr/share/seclists/Usernames/cirt-default-usernames.txt -p 'Sup3RS3cuR3@123' -f 10.129.140.232 pop3
```


---
#### IMAP

| **Command**                                                 | **Description**                                                                                           |
| ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| A1 LOGIN username password                                  | User's login.                                                                                             |
| 1 LIST "" *                                                 | Lists all directories.                                                                                    |
| 1 CREATE "INBOX"                                            | Creates a mailbox with a specified name.                                                                  |
| 1 DELETE "INBOX"                                            | Deletes a mailbox.                                                                                        |
| 1 LSUB "" *                                                 | Returns a subset of names from the set of names that the User has declared as being active or subscribed. |
| 1 SELECT INBOX                                              | Selects a mailbox so that messages in the mailbox can be accessed.                                        |
| 1 UNSELECT INBOX                                            | Exits the selected mailbox.                                                                               |
| 1 CLOSE                                                     | Removes all messages with the Deleted flag set.                                                           |
| 1 LOGOUT                                                    | Closes the connection with the IMAP server.                                                               |
| 1 FETCH 1:* (FLAGS BODY[HEADER.FIELDS (SUBJECT FROM DATE)]) | Show all mails                                                                                            |
#### POP3

| **Command**   | **Description**                                                                                                  |
| ------------- | ---------------------------------------------------------------------------------------------------------------- |
| USER username | Identifies the user.                                                                                             |
| PASS password | Authentication of the user using its password.                                                                   |
| STAT          | Requests the number of saved emails from the server.                                                             |
| LIST          | Requests from the server the number and size of all emails.                                                      |
| RETR id       | Requests the server to deliver the requested email by ID.                                                        |
| DELE id       | Requests the server to delete the requested email by ID.                                                         |
| CAPA          | Requests the server to display the server capabilities.                                                          |
| RSET          | Requests the server to reset the transmitted information.                                                        |
| QUIT          | Closes the connection with the POP3 server.                                                                      |
| Reference     | [book.hacktricks.xyz - pentesting-imap](https://book.hacktricks.xyz/network-services-pentesting/pentesting-imap) |
| Reference     | [smtp-commands-reference-auth](https://www.samlogic.net/articles/smtp-commands-reference-auth.htm)               |


>Telnet smtp commands
https://www.samlogic.net/articles/smtp-commands-reference-auth.htm