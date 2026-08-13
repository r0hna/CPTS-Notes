# Error
>`sqlplus: error while loading shared libraries: libsqlplus.so: cannot open shared object file: No such file or directory`
```
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig
```