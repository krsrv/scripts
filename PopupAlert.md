Configures popups (which are different from notifications) to appear periodically. I used this to create a reminder for correcting posture every 30 minutes.

## Script:
```osascript -e 'display alert "Sit straight" message "Sit straight with your neck in line. Deep breath out then in will help."'```
Save this as some bash file somewhere.

## Scheduler:
I stored the scheduler in `/Library/LaunchAgents/` so that the script runs when *any* user is logged in. The name should be of the format `com.mycompanyname.mydepartment.mytaskname.plist`:
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.user.notification</string>
    <key>ProgramArguments</key>
    <array>
        <string>/Users/utkarshmishra/Scripts/posture.sh</string>
    </array>
    <key>StartInterval</key>
    <integer>420</integer>
</dict>
</plist>
```

To load the daemon:

```
launchctl load -w /Library/LaunchDaemons/com.mycompanyname.mydepartment.mytaskname.plist
```

To unload the daemon:

```
launchctl unload -w /Library/LaunchDaemons/com.mycompanyname.mydepartment.mytaskname.plist
```

The `load`, `unload` commands are legacy now even though they still work - use `enable`, `disable` instead.

References:
1. https://stackoverflow.com/questions/132955/how-do-i-set-a-task-to-run-every-so-often
2. XML file sample: https://www.splinter.com.au/using-launchd-to-run-a-script-every-5-mins-on/
3. https://stackoverflow.com/questions/5588064/how-do-i-make-a-mac-terminal-pop-up-alert-applescript

