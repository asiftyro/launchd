## documentation in progress

# How to create Launchd User Agents to run python script at a schedule on MacOS Catalina


Steps:
1. Create a plist (Propert List) file in /Users/<user_name>/Library/LaunchAgents. It is an XML file that contains job details, i.e. command to run script, location of the script, script execution time table, error reporting file path and stdout file path among some other specification. The plist file name should be unique and as a convention, its should be written in reverse domain notation, e.g.org.w3c.dom
2. Load and start the plist by `launchctl` command.
```
launchctl load  /Users/<user_name>/Library/LaunchAgents/local.script.plist
launchctl unload  /Users/<user_name>/Library/LaunchAgents/local.script.plist
launchctl start local.script.plist
launchctl stop local.script.plist
launchctl list
```

Sample plist files:
1. Run script at 5:30 pm everyday:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>local.script</string>
    
    <key>ProgramArguments</key>
    <array>
        <string>path/to/python</string>
        <string>path/to/script/script.py</string>
    </array>
    
    <key>StandardOutPath</key>
    <string>path/to/log/stdout_log_file.log</string>
    
    <key>StandardErrorPath</key>
    <string>path/to/error/error_log_file.log</string>

    <key>StartCalendarInterval</key>
    <dict>
        <key>Hour</key>
        <integer>17</integer>
        <key>Minute</key>
        <integer>30</integer>
    </dict>
</dict>
</plist>
```

2. Run script at 5:30 pm and 8:00 am everyday:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>local.script</string>
    
    <key>ProgramArguments</key>
    <array>
        <string>path/to/python</string>
        <string>path/to/script/script.py</string>
    </array>
    
    <key>StandardOutPath</key>
    <string>path/to/log/stdout_log_file.log</string>
    
    <key>StandardErrorPath</key>
    <string>path/to/error/error_log_file.log</string>

    <key>StartCalendarInterval</key>
    <array>
        <dict>
            <key>Hour</key>
            <integer>17</integer>
            <key>Minute</key>
            <integer>30</integer>
        </dict>
        <dict>
            <key>Hour</key>
            <integer>8</integer>
            <key>Minute</key>
            <integer>0</integer>
        </dict>        
    </array>
</dict>
</plist>
```


3. Run script at 5:30 pm on every Sunday:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>local.script</string>
    
    <key>ProgramArguments</key>
    <array>
        <string>path/to/python</string>
        <string>path/to/script/script.py</string>
    </array>
    
    <key>StandardOutPath</key>
    <string>path/to/log/stdout_log_file.log</string>
    
    <key>StandardErrorPath</key>
    <string>path/to/error/error_log_file.log</string>

    <key>StartCalendarInterval</key>
    <dict>
        <key>Weekday</key>
        <integer>0</integer>
        <key>Hour</key>
        <integer>17</integer>
        <key>Minute</key>
        <integer>30</integer>
    </dict>
</dict>
</plist>
```
3. Run script at 5:30 pm on every Sunday and Saturday:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>local.script</string>
    
    <key>ProgramArguments</key>
    <array>
        <string>path/to/python</string>
        <string>path/to/script/script.py</string>
    </array>
    
    <key>StandardOutPath</key>
    <string>path/to/log/stdout_log_file.log</string>
    
    <key>StandardErrorPath</key>
    <string>path/to/error/error_log_file.log</string>

    <key>StartCalendarInterval</key>
    <array>
        <dict>
            <key>Weekday</key>
            <integer>0</integer>
            <key>Hour</key>
            <integer>17</integer>
            <key>Minute</key>
            <integer>30</integer>
        </dict>
        <dict>
            <key>Weekday</key>
            <integer>6</integer>
            <key>Hour</key>
            <integer>17</integer>
            <key>Minute</key>
            <integer>30</integer>
        </dict>        
    </array>
</dict>
</plist>
```
4. Run script every minute:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>local.script</string>
    
    <key>ProgramArguments</key>
    <array>
        <string>path/to/python</string>
        <string>path/to/script/script.py</string>
    </array>
    
    <key>StandardOutPath</key>
    <string>path/to/log/stdout_log_file.log</string>
    
    <key>StandardErrorPath</key>
    <string>path/to/error/error_log_file.log</string>

    <key>StartInterval</key>
    <integer>60</integer>
</dict>
</plist>
```




### Some useful keys to use in plist files:


```
<key>Program</key>
<string>/path/to/program</string>
```


```
<key>ProgramArguments</key>
<array>
	<string>/usr/bin/rsync</string>
	<string>--archive</string>
	<string>--compress-level=9</string>
	<string>/Volumes/Macintosh HD</string>
	<string>/Volumes/Backup</string>
</array>
```


```
<key>StandardInPath</key>
<string>/tmp/test.stdin</string>
```


```
<key>StandardOutPath</key>
<string>/tmp/test.stdout</string>
```


```
<key>StandardErrorPath</key>
<string>/tmp/test.stderr</string>
```


```
<key>WorkingDirectory</key>
<string>/tmp</string>
```


```
<key>RunAtLoad</key>
<true/>
```


```
<key>StartCalendarInterval</key>
<dict>
	<key>Hour</key>
	<integer>3</integer>
	<key>Minute</key>
	<integer>0</integer>
</dict>
```


|Key|Type|Values|
|---|----|------|
|Month|Integer|Month of year 1..12, 1 = January)|
|Day|Integer|Day of month (1..31)|
|Weekday|Integer|Day of week 0..7, 0 and 7 = Sunday|
|Hour|Integer|Hour of day 0..23|
|Minute|Integer|Minute of hour 0..59|


* Ranges: Use hyphen, e.g. 2-6
* List: Use comma, e.g. 1,2,3
* Skip in range: Use slash, e.g 0-60/2 run every other minute



```
<key>KeepAlive</key>
<true/>
```


```
<key>KeepAlive</key>
<dict>
	<key>SuccessfulExit</key>
	<true/>
</dict>
```


```
<key>KeepAlive</key>
<dict>
	<key>NetworkState</key>
	<true/>
</dict>
```


```
<key>KeepAlive</key>
<dict>
	<key>PathState</key>
	<dict>
		<key>/tmp/runJob</key>
		<true/>
	</dict>
</dict>
```


```
<key>KeepAlive</key>
<dict>
	<key>OtherJobEnabled</key>
	<dict>
		<key>local.other_job</key>
		<false/>
	</dict>
</dict>
```


```
<key>StartInterval</key>
<integer>3600</integer>
```
