# commands


## Windows Disk Management 
### Assign Drive
```
diskpart
list volume
select volume <X>
assign letter=Z
exit
```

### Detach Drive
```
diskpart
list volume
select volume <X>
remove all dismount
```
### Copy
```
xcopy E:\YourFolder D:\YourFolder /E /I
```

/E → Copies all subdirectories, even if they are empty.

/I → Assumes the destination is a folder.


## Linux Disk Managment 
### Assign network drive on windows system

```

sudo mount -t cifs //<IPADDRESS>/<FOLDER NAME> /mnt/tv -o username=<User>,password=<Password>


```