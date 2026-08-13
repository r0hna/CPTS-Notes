# Nmap Scan
```
nmap -p 111,2049,44761,45575,47251,58151 -sVC --script nfs* "$ip" -oN scan/nfs_scan_"$ip".nmap
```

# Footprinting service (Linux)
#### Show available shares
```
showmount -e "$ip"
```
#### Mount NFS share
```
mkdir nfs-share;
sudo mount -t nfs "$ip":/<share> ./nfs-share/ -o nolock;
cd target-NFS;
tree .
```
#### Unmount shares
```
sudo umount ./nfs-share
```
#### List content name with user & groups (NFS)
```
ls -l ./nfs-share
```
#### List content with UIDs & GUIDs
```
ls -n ./nfs-share
```

---

>NOTE: if the `root_squash` option is set, we cannot edit file even as root.

> If you get "permission denied" error (In the nfs folder)
```
sudo useradd -u 1001 randomuser
```

>NFS permission denied error
```
Try ls with sudo, try to mount NFS share elsewhere, not in /mnt
```