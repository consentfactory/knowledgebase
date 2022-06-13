# Autohotkey on Mac

The gist: AutoHotkey isn't available on Mac as it is for Windows, but you can more or less freely create it using Automator.

## Basic Process

1. Open Automator > Create and Application
2. Enter your code
3. Save as application
4. In Automator > Create quick action 
5. Select the previously created applicaiton
6. Add application from step 1-3 to System Preferences > Security & Privacy > Accessibility
7. Go to System Preferences > Keyboard > Shortcuts > Services
8. Create the keyboard shortcut

Note: if you update the application or change something, you'll need to redo step 6.

## Example code for Shortcut

```
on run {}
  # Get date from terminal shell and save to variable 'theDate'
	set theDate to do shell script "date +%Y%m%d"
  # Get the current application that you're working from
	tell application "System Events"
		tell (first process whose frontmost is true)
			set appName to displayed name
		end tell
	end tell
  # Call the application you're working from currently
	tell application appName to activate
  # Set the text that you're trying to send
	set textToType to "Configured " & theDate & " - Jimmy"
	# Send the text as keystrokes
  tell application "System Events" to keystroke textToType
end run
```

## Sources

- Overall process:
  - https://stackoverflow.com/questions/67181895/automator-permissions-error-when-running-applescript-in-safari-alternatives-an
- How to call currently active window:
  - https://forum.keyboardmaestro.com/t/applescript-to-tell-active-application/6336
