# Archived Keyboard Maestro macros

I've been clearing out some old Keyboard Maestro macros, I'm archiving a few here in case they're useful as a reference at some point.

## Get YouTube channel RSS

It's not immediately obvious how to get an RSS feed for a YouTube channel. This takes a channel's URL from the current Safari tab and converts it to an RSS feed URL.

```
**Get YouTube RSS
No triggers specified.
Will execute the following actions:**
		Set Variable “local_ChannelURL” to Text
		%SafariURL% 
		Search Environment Variable “local_ChannelURL” Using Regular Expression (ignoring case)
		Search for “(.*/)(.*)”
		And capture to:
	0	Ignored
	1	Ignored
	2	local_ChannelID
		Stop macro and notify on failure.

		Set System Clipboard to Text
		https://www.youtube.com/feeds/videos.xml?channel_id=%Variable%local_ChannelID% Notify on failure.
```

# Copy page URL and title separately (useful to then do a sequential paste somewhere else).

```
Copy title and link
Triggered by any of the following:
		The Hot Key ⌃⌥⇧⌘M is pressed
Will execute the following actions:
		Set System Clipboard to Text
		%SafariTitle% Notify on failure.
		 
		Set System Clipboard to Text
		%SafariURL% Notify on failure.

```
