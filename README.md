# commands

- [Windows](#Windows-Disk-Management)
- [Linux](#Linux-Disk-Management)
- [AWS](#AWS-Commands)


## Windows Disk Management 
### Assign Drive
```powershell
diskpart
list volume
select volume <X>
assign letter=Z
exit
```

### Detach Drive
```powershell
diskpart
list volume
select volume <X>
remove all dismount
```
### Copy
```powershell
xcopy E:\YourFolder D:\YourFolder /E /I
```

/E → Copies all subdirectories, even if they are empty.

/I → Assumes the destination is a folder.


## Linux Disk Management 
### Assign network drive on windows system

```bash
sudo mount -t cifs //<IPADDRESS>/<FOLDER NAME> /mnt/tv -o username=<User>,password=<Password>

```

### Show size of folders

```bash
sudo du -h --max-depth=1 /home/media/video/ | sort -hr | head -10

```


### Get video Resolution


```bash
ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of csv=p=0 $1
```
### how to mount a usb drive

```
lsblk
sudo mount /dev/sda1 /mnt/usb
```

## AWS Commands
### Get secret from parameter store

```bash
aws ssm get-parameter --name "/gousto/pickles/service/plannedcapacity/MESSAGE_ARN" --with-decryption |  jq -r '.Parameter.Value'
```


```
aws logs filter-log-events \
  --log-group-name ecs-production-service-core-webserver-appLog \
  --filter-pattern "ERROR" \
  --start-time $(date -d '1 hour ago' +%s)000 \
  --end-time $(date +%s)000

```
# Kill cloudflare (until restart)

```
sudo launchctl bootout system /Library/LaunchDaemons/com.cloudflare.1dot1dot1dot1.macos.warp.daemon.plist
```