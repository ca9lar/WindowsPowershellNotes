##### Test connection over port
```ps
test-netconnection 169.47.155.6 -Port 465
```

##### Get last reboot time
```ps
Get-WmiObject Win32_OperatingSystem | Select-Object LastBootUpTime
```

##### Get last bootup time
```ps
wmic path Win32_OperatingSystem get LastBootUpTime
```
##### Get instance ID like CURL
```ps
Invoke-RestMethod -uri http://169.254.169.254/latest/meta-data/instance-id
```

##### Netstat on Windows instance
```ps
netstat -ano | findstr :80
```

#### Some common Linux one-liners and equivalent PowerShell commands
***
##### Search for a string in a file

```sh
grep <string> <file>
```

```ps
select-string <file> -pattern "<string>"
```
##### Count the number of lines of a file

```sh
bash - wc -l <file>
```
```ps
get-content "<file>" | Measure-Object -Line
```

##### Make a HTTP request to a server and dump the result to STDOUT

```sh
curl <url>
```

```ps
(Invoke-WebRequest -uri "<url>").Content
```

##### Iterate through a file and perform an action on the contents of each line

```sh
for i in $(cat <file>); do echo whois $i; done
```

```ps
get-content "<file>" | ForEach-Object { write-host "whois" $_ }
```

##### Search/Replace a string in a file

```sh
sed 's/<orig_string>/<new_string>/' <file>
```

```ps
gc "<file>" | %{$_ -replace "<orig_string>", "<new_string>"}
```

##### Recursively find files in a directory matching a pattern

```sh
find <path> -name '<pattern>'
```

```ps
get-childitem -Path "<path>" -Filter "<pattern>" -Recurse
```

##### Windows Firewall
###### Start
```ps
netsh advfirewall set allprofiles state on 
```
###### Stop
```ps
netsh advfirewall set allprofiles state off
```
###### Status
```ps
netsh advfirewall show allprofiles
```
