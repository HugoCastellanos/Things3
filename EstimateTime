tell application "Things3"
	set inboxToDos to selected to dos
	set totalMinutes to 0
	set totalTasks to 0
	set taggedTasks to 0
	set timeFound to false
	repeat with inboxToDo in inboxToDos
		set taskName to name of inboxToDo as string
		log "Item: " & taskName
		try
			set foo to to dos of inboxToDo
			log "it's a project"
		on error msg
			log "it's a todo"
			set tagList to tags of inboxToDo
			set totalTasks to totalTasks + 1
			if length of tagList > 0 then
				repeat with aTag in tagList
					if (name of aTag as string) contains "⏰ " then
						set minutes to ((strings 3 thru (length of (name of aTag as string)) of (name of aTag as string)) as string)
					else
						set minutes to name of aTag as string
					end if
					try
						set minutes to (do shell script "echo " & minutes & "|sed 's/\\([0-9]*\\)min/\\1/'") as integer
						set totalMinutes to totalMinutes + minutes
						set timeFound to true
					end try
				end repeat
				if timeFound then
					set taggedTasks to taggedTasks + 1
				end if
				set timeFound to false
			end if
		end try
	end repeat
	display alert "You've have scheduled " & (round (totalMinutes / 60 * 10)) / 10 & " hours of your day. " & taggedTasks & " of " & totalTasks & " tasks had time estimations."
end tell
