# 4d-applescript-remote-launch
Launch an app on another Mac on the same network via Remote Apple Events

Create an account for "sharing only"

<img width="668" alt="2018-05-09 12 21 16" src="https://user-images.githubusercontent.com/1725068/39794086-802b2406-5383-11e8-9954-d2183ffc241c.png">

Enable remote AppleScript Events and give that user access.

<img width="668" alt="2 apple events" src="https://user-images.githubusercontent.com/1725068/39793888-5975f468-5382-11e8-83e0-e16476bad61d.png">

```applescript
on startMyAPP(user, pass, address)
	
	set the remoteMac to machine ("eppc://" & user & ":" & pass & "@" & address as string)
	tell application "Finder" of remoteMac
		using terms from application "Finder"
			set the appPath to path to application support from user domain as string
			set the appPath to appPath & "DGWServer:DB:Doctor’s Good Will Server.app"
			open application file the appPath as string
		end using terms from
	end tell
	
end startMyAPP

on run argv
	set {user, pass, address} to argv
	startMyAPP(user, pass, address)
end run
```

Call it as so:

```sh
osascript theScript.scpt jimmy fallon miyako-no-MacBook.local
```
