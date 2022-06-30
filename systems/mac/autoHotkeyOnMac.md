# Autohotkey on Mac

The gist: AutoHotkey isn't available on Mac as it is for Windows, but you can more or less freely create it using Automator.

## Basic Process

1. Open Automator > File > New > Application
2. Add 'Run AppleScript' action
3. Enter your code
4. Save as application
5. Open Automator again > File > New > Quick Action 
6. Go to Library > Utilities > Launch Application
7. Select the previously created application
8. Save quick action with appropriate name
9. Add application from step 1-3 to System Preferences > Security & Privacy > Accessibility
10. Go to System Preferences > Keyboard > Shortcuts > Services
11. Find your application in the list (under General)
12. Create the keyboard shortcut

Note: if you update the application or change something, you'll need to redo step 6.

## Example code that types out the current date and some text

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

## Example code that types out contents of clipboard

```
on run {}
  # Get the current application that you're working from
	tell application "System Events"
		tell (first process whose frontmost is true)
			set appName to displayed name
		end tell
	end tell
  # Call the application you're working from currently
	tell application appName to activate
  # Set the text that you're trying to send
	set textToType to the clipboard
  # Send the text as keystrokes
	tell application "System Events" to keystroke textToType
end run
```

## Sources

- Overall process:
  - https://stackoverflow.com/questions/67181895/automator-permissions-error-when-running-applescript-in-safari-alternatives-an
- How to call currently active window:
  - https://forum.keyboardmaestro.com/t/applescript-to-tell-active-application/6336
