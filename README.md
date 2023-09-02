# quick-look-caller
Instruction how to do application to use [Quick Look](https://en.wikipedia.org/wiki/Quick_Look) functionality easily (on mac)

## TD;LR
1. Open [Automator](https://en.wikipedia.org/wiki/Automator_(macOS))
2. Click `New Document` button
3. Choose `Application`
4. Find `Run AppleScript`
5. Paste the following script in the code space
```
on run {input, parameters}
	
	if input is {} then
		set inputFile1 to ¬
			quoted form of POSIX path of ¬
			(choose file with prompt "Please select a file to process:")
	else
		set inputFile1 to quoted form of ¬
			(POSIX path of first item of input)
	end if
	
	tell application "Terminal"
		if not (exists window 1) then reopen
		activate
		do script "qlmanage -p" & space & inputFile1 in window 1
	end tell
	
end run
```
6. Press `command + S` button to save the application.
7. Use [this guide](https://www.tomsguide.com/how-to/how-to-set-default-apps-on-mac) to open applications with your newly created application by default.
