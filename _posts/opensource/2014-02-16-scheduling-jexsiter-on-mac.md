---
layout: post
title: "Scheduling Jexsiter on Mac"
description: "Using OSX launchd to execute Jexsiter on a schedule"
category: "opensource"
tags: [osx, mac, jexsiter]
---
{% include JB/setup %}

# Resources distilled and preserved
For much more detail check out the following:
* [Nathan Grigg's blog entry on launchd](http://nathangrigg.net/2012/07/schedule-jobs-using-launchd/)
* [A plist generator courtesy of Nathan Witmer at zerowidth.com](http://launched.zerowidth.com/)
* [Apple Developer on launchd](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html) (also has link to launchd.plist
page)
* [Logging with launchd](http://erikslab.com/2011/02/04/logging-with-launchd/)

# Overview
* Launchd is OSX replacement for cron jobs. Use /Library/LaunchAgents for root jobs to be launched on start up. User log in runs that users ~/Library/LaunchAgents. 
* launchd expects .plist file. Best practice, use reverse domain name (unique) in file name and label field! Remember to make label field the same as file name (needs to be unique).

# plist file

    <?xml version="1.0" ?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs PropertyList-1.0.dtd">
    <plist version="1.0">
        <dict>
            <key>Label</key>
            <string>org.medale.exsiter</string>
            <key>ProgramArguments</key>
            <array>
               <string>/Users/medale/exsiter/backup.sh</string>
            </array>
            <key>StartCalendarInterval</key>
	        <dict>
		        <key>Hour</key>
		        <integer>19</integer>
		        <key>Minute</key>
		        <integer>45</integer>
		        <key>Weekday</key>
		        <integer>5</integer>
	        </dict>
	        <key>StandardOutPath</key>
            <string>/var/log/exsiter/exsiter.log</string>
            <key>StandardErrorPath</key>
            <string>/var/log/exsiter/exsiter-error.log</string>
        </dict>
    </plist>
    
# Controlling plist

## Load/Unload - use schedule in plist

Loads script to be executed on the schedule listed in its .plist file.

    launchctl load/unload ~/Library/LaunchAgents/org.medale.exsiter.plist
    
## Start/stop script now

$Label is value of /dict/key=Label in .plist file

    launchctl start/stop $Label
    
# Troubleshooting

Checking plist for valid format:

    plutil -lint org.medale.exsiter.plist

Show all processes under launchctl:

    launchctl list

Remove old plist from launchctl:

    launchctl remove $Label
