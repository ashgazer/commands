# commands

- [Windows](#Windows-Disk-Management)
- [Linux](#Linux-Disk-Management)
  - [Logs](#Logs) 
- [AWS](#AWS-Commands)
- [Networking](#Networking)


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

### Shutdown
```
shutdown /s /f /t 0
```
### find md5 hash of a file
```
certutil -hashfile <file> MD5
```

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
### Logs

#### get logs size
```
sudo du -sh /var/log/*
```
#### clean system logs
```
sudo journalctl --vacuum-time=7d
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

## Networking

```
nmap -sn 192.168.1.0/24
```
-sn does a "ping scan" — discovers hosts but doesn’t port scan them.```

### Tailscale
```
sudo tailscaled

```

```
tailscale up
```

