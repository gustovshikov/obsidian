# Volatility 2
Command List
`volatility -f memdump.mem imageinfo` // Take memory image “memdump.mem” and determine the suggested profile for analysis. The profile is the operating system, version, and architecture.

`volatility -f memdump.mem --profile=PROFILE pslist` // Take memory image, provide the profile, then use the pslist plugin to print a list of processes to the terminal.

`volatility -f memdump.mem --profile=PROFILE pstree` // Use the pstree plugin to print a process tree to the terminal.

`volatility -f memdump.mem --profile=PROFILE psscan` // Use the psscan plugin to print all available processes, including hidden ones often used by malware (compare this to pslist to see if there’s any differences!).

`volatility -f memdump.mem --profile=PROFILE psxview` // Use the plugin psxview plugin to print expected and hidden processes. This is a combination of pslist and psscan plugins.

`volatility -f memdump.mem --profile=PROFILE procdump -p PIDHERE` // Use the procdump plugin to save a process as a file. You must provide a process ID using the -p flag.

`volatility -f memdump.mem --profile=PROFILE netscan` // Use the plugin netscan to identify any active or closed network connections.

`volatility -f memdump.mem --profile=PROFILE timeliner` // Use the timeliner plugin to create a timeline of events from the memory image.

`volatility -f memdump.mem --profile=PROFILE iehistory` // Use the iehistory plugin to pull internet browsing history.

`volatility -f memdump.mem --profile=PROFILE filescan` // Use the filescan plugin to identify any files on the system from the memory image.

`volatility -f memdump.mem --profile=PROFILE cmdline -p PIDHERE` // Use the cmdline plugin to retrieve any command-line arguments passed to a process. You must provide a process ID using the -p flag.

`volatility -f memdump.mem --profile=PROFILE dumpfiles -n --dump-dir=./` // Use the dumpfiles plugin to retrieve files from the memory image. In this case our terminal is open in the Desktop (root@SBTLab2:~/Desktop) and we are using the output location ./ which tells Volatility to put the files in our current location, the Desktop.

# Volatility 3
- --profile is no longer present in Vol 3
- Generic plugin names are now replaced with OS-specific plugins
- pstree > windows.pstree, linux.pstree, mac.pstree

| Command Purpose               | **Volatility 2 Command**                                   | **Volatility 3 Command**                             |
| ----------------------------- | ---------------------------------------------------------- | ---------------------------------------------------- |
| Get process tree              | volatility --profile=PROFILE pstree -f file.dmp            | python3 vol.py -f file.dmp windows.pstree            |
| List services                 | volatility --profile=PROFILE svcscan -f file.dmp           | python3 vol.py -f file.dmp windows.svcscan           |
| List available registry hives | volatility --profile=Win7SP1x86_23418 -f file.dmp hivelist | python3 vol.py -f file.dmp windows.registry.hivelist |
| Print cmd commands            | volatility --profile=PROFILE cmdline -f file.dmp           | python3 vol.py -f file.dmp windows.cmdline           |
**Gui**
Volatility Workbench