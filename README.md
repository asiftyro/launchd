## documentation in progress

# How to create Launchd User Agents to run python script at a schedule on MacOS Catalina


Steps:
1. Create a plist (Propert List) file in /Users/<user_name>/Library/LaunchAgents. It is an XML file that contains command to run script, location of the script, script execution time table, error reporting file path and stdout file path among some other specification.
2. Load and start the plist by `launchctl` command.


Sample plist file:
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

