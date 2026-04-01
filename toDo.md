development progress file

# services
## gameServer.service
service that will install dependencies (tmux/jre), switchj to the correct jre version, and launch server in a tmux named %i via the run script given in the directory given 
(in the future this may handle the entire server launch via the provided server.jar{WIP})
- serverBackup.timer
- gameServer.target

# scripts 
## serverInfo -update -read -dir -run -java -backupDir -user -backupNum
- -update / -read weather to read or write to the following:

- -dir (directory server runs from)
- -run (name of the bash script that launches the server) or -jar (instead gameServer.service will Handle launch {WIP})
- -java (version of java to run the server on if applicable)
- -backupDir (location to save backups to)
- -user (which user to run server through) (for permissions)
- -backupNum (how many backups to keep)
- -backupSize (max size of backups to keep)
