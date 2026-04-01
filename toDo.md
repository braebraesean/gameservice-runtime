development progress file

# services
## gameServer.service
service that will install dependencies (tmux/jre), switchj to the correct jre version, 
and launch server in a detached tmux via the run script given in the directory given 
(in the future this may handle the entire server launch via the provided server.jar{WIP})

## serverBackup.timer
timer that will make a tar/xz backup of gameServer directory and save it to the gameServer backup directory

## serverRestart.timer
timer that will restart the server at serverInfo ($restartTimes) 

## resource-guard.timer
timer that runs resourceGuard.sh every serverInfo.sh's ($rgd)

## gameServer.target
promts and asks for essential serverInfo.sh information such as:
- gameServer default directory
- gameServer default jre runtime
- gameServer default run executable or server jar file


# scripts 
## serverInfo 
## -update -read -dir -run -java -backupDir -user -backupNum
- -update / -read weather to read or write to the following:


- -dir (directory server runs from) (no default, must be set)
- -startScript (name of the bash script that launches the server) or -jar (instead gameServer.service will Handle launch {WIP}) (no default, must be set)
- -java (version of java to run the server on if applicable) (no default, must be set)
- -backupDir (location to save backups to) (default ~/serverBackups)
- -user (which user to run server through) (for permissions) (no default, must be set)
- -backupNum (how many backups to keep) (default 2) (set to -1 to disable)
- -backupSize (max size of backups to keep) (default 5gb) (set to -1 to disable)
- -backupTimer (how often server will take a backup) (default 2 hours) (set to -1 to disable)
- -restartTimes (set times for server to restart ex: 2:00, 14:00) (default 2:00 and 14:00) (set to -1 to disable)
- -MemoryGuard (sets how often the server checks for memory leaks and attempts to repair them if using a server jar instead of a premade startScript) (default 10 min) (set to -1 to disable)
- -rgr (resource-guard ram, sets ram limits so resource-guard will attempt to reclaim memory with a server restart) (default off or user_jvm_args -Xmx -1gb if using server jar over premade startScript) (set to -1 to disable)
- -rgd (resource-guard delay, sets delay so resource guard will not constantly restart server if it is actually in need of ram over its ram limit) (default 2 hours) (set to -1 to disable)
- -rgs (resource-guard storage, sets storage limits so resource-guard will shutdown services if there is risk of corruption due to lack of storage space) (default 3gb) (set to -1 to disable)

## run

{WIP} will launch the server using a user_jvm_args file and serverInfo.sh's ($jar)

and potentially check for memory leaks every serverInfo.sh's ($MemoryGuard)

## resourceGuard
a script that attempts to save resources/corruption via restarting the server when ram usage is above serverInfo.sh's ($rgr) limit to attempt to reclaim memory
and stops the server if there is less than serverInfo.sh's ($rgs) storage limit ramaining on the drive gameServers directory is on to prevent corruption
