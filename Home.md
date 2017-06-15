Welcome to the speedtest-cli wiki!

## Python API

```python
import speedtest

servers = []
# If you want to test against a specific server
# servers = [1234]

s = speedtest.Speedtest()
s.get_servers(servers)
s.get_best_server()
s.download()
s.upload()
s.share()

results_dict = s.results.dict()
```

### To avoid `MemoryError`

```
s.upload(pre_allocate=False)
```

### Set a mini server
```
s = speedtest.Speedtest()
s.get_best_server(s.set_mini_server("http://speedtest.test.fr/"))
s.download()
```

### Bind source
```
source = "192.168.1.100"
speedtest.SOURCE = source
socket.socket = speedtest.bound_socket
s = speedtest.Speedtest()
s.get_best_server()
s.download()
s.upload()
```

### A zenity-powered bash script to display test results graphically
```
#!/bin/bash
notify_send_messages()
{
notify-send "www.SpeedTest.net:" "Retrieving speedtest.net configuration and server list..." -i network-modem -t 30
notify-send "www.SpeedTest.net:" "Selecting best server & calculating speeds..." -i network-modem -t 40
}
TMPFILE=`mktemp -t speedtest.XXXXXX`
notify_send_messages &
speedtest-cli 2>&1 > $TMPFILE
# Check if temp file is empty: if true there's something wrong with network
if [ -z "$TMPFILE" ]
then
	zenity --class=Err --error --title="www.SpeedTest.net" --text="Network Error!"
else
#	Determine ISP source server, best target server, ping, dowload and upload speeds
	SOURCE=$(cat "$TMPFILE" | grep "Testing from " | sed -e "s/Testing from //g" -e "s/\.\.\.//g")
	TARGET=$(cat "$TMPFILE" | grep "Hosted by " | sed -e "s/Hosted by //g" -e "s/: .\+$//g")
	PING=$(cat "$TMPFILE" | grep "Hosted by " |  awk -F ": " '{print $2}')
	DOWNLD=$(cat "$TMPFILE" | grep "Download: " | sed -e "s/Download: //g")
	UPLOAD=$(cat "$TMPFILE" | grep "Upload: " | sed -e "s/Upload: //g")
#	Display information
	zenity --class=SpeedTest --info --height 200 --title="www.SpeedTest.net" --text="\nISP Server: <b>$SOURCE</b>\n\nTarget Server: <b>$TARGET</b>\n\nPing Speed: <b>$PING</b>\n\nDownload Speed: <b>$DOWNLD</b>\n\nUpload Speed: <b>$UPLOAD</b>"
#	Remove temp file
	rm -f $TMPFILE
fi
```
