# YTNotify
Get YouTube channel updates on your desktop!

YTNotify is a simple Java application that periodically checks YouTube channels that you specify and notifies you of any updates.

## How to Use it
### Initial setup

YTNotify requires two things: [Simple JSON](https://mvnrepository.com/artifact/com.googlecode.json-simple/json-simple/1.1.1)'s jar file in the same folder and a Google API key with YouTube enabled in `key.txt`.

1) Add your java bin to PATH environment, "C:\Program Files\Java\*your java version*\bin"

2) Compile it first: javac -classpath json-simple-1.1.1.jar YTNotify.java

3) Command to start: javaw -classpath json-simple-1.1.1.jar YTNotify.java

### General Usage

Once the program is running, an icon will show up in the taskbar at the bottom right (usually) of the screen. Just right click on that and select "Add by Name" or "Add by ID" and follow the instructions. Once you've entered a new channel, any updates to that channel will show up as notifications on your screen. When you get a notification you can right click on the taskbar icon again and go over to the "Recent Updates" menu to have the new video show up in your web browser.

## How it Works

Once you give YTNotify the name or ID of the channel that you want to follow, it contacts Google's YouTube API and gets the channel's upload playlist ID. From there, it periodically queries the API and if the newest video's title has changed, it knows that there's a new video.

## Issues/Questions

### Why isn't there a prebuilt JAR? / Why isn't there an API key included?

Each API key gets a limited "quota" per day that it can use before the API will lock the key out for the rest of the day. While one key is good enough for up to a few users, eventually enough people would bring it down. This way, everyone has their own quota.

### Why doesn't clicking on the notification bring up the video?

There IS supposed to be a way to have notifications send actions to Java listeners, but the documentation somehow left out HOW this can be done (probably because a lot of this stuff is platform-dependent). I've tried some ideas from places like StackExchange like adding extra `ActionListener`s to the `TrayIcon`, but nothing seems to work. If someone out there knows how to do this, please tell me and I will add it in.

### Why is "Add by Name" wonky? / Why not search by name?

The "Add by Name" feature gets a channel's ID by using an internal name that may or may not match the channel's displayed name and will never have spaces. This is to avoid using "search" API calls, which use 10-30 times more quota and can easily use up a key. Nevertheless, I'll try adding in a name search feature in the future. Just use it carefully. Until then, use the channel's ID, which is usually part of its URL.
