# Useful oneliners

Useful list of oneliners I feel needs to be rememebered

Remove old key ID from known_hosts (when SSH complains..)

	perl -pi -e 's/\Q$_// if ($. == ID);' ~/.ssh/known_hosts

Limit bandwidth of apt-get to MAX-SPEED kbps
	
	sudo apt-get -o Acquire::http::Dl-Limit=[MAX-SPEED] install|upgrade|...

List all processes exept those run by root
	
	ps -U root -u root -N

List 5 worst RAM eating processes (not working on OS X)
	
	ps axo pid,args,pmem,rss,vsz --sort -pmem,-rss,-vsz | head -n 6

Above but for OS X
	
	ps -axm -o "pid,comm,%mem,rss,vsz" | head -n 6

Show permissions as octal values 
	
	ls -l | sed -e 's/--x/1/g' -e 's/-w-/2/g' -e 's/-wx/3/g' -e 's/r--/4/g' \
	-e 's/r-x/5/g' -e 's/rw-/6/g' -e 's/rwx/7/g' -e 's/---/0/g'

Removes everything but SOMETHING_IMPORTANT
	
	ls * | grep -v SOMETHING_IMPORTANT | xargs rm -rf

Assign en1 a random MAC-address
	
	sudo ifconfig en1 ether $(openssl rand -hex 6 | sed 's/\(..\)/\1:/g; s/.$//')

Get a progressbar when using dd to burn OUTPUT.img to /dev/rdiskX
	
	pv -tpreb OUTPUT.img | sudo  dd of=/dev/rdiskX bs=1m

Remove all subdirs in DIRPATH
	
	find [DIRPATH] -d -type d -exec rm -rf '{}' \;

Calculate nof rows in in all php-files in current dir and its subdirs
	
	find . -name '*.php' | wc -l

Use rsync instead of cp "IMO cp is outdated" : http://askubuntu.com/questions/17275/progress-and-speed-with-cp

	alias cp="rsync -avz"

List all connected disks
	
	(sudo) fdisk -l

Tunnel SMB over SSH from host on on remote network to local machine on localhost:22000
	
	ssh -f -N -L 22000:[IP of SMB share in remote network]:139 [remote user]@[remote SSH server] -p [remote SSH port]

Reverse SSH tunnel (to bypass firewall). Sets up 51021 on remote server as SSH-port

	ssh -nNTR 51021:localhost:22 [remote user]@[remote SSH server] -p [remote SSH port]

To connect to above, on the remote SSH-server just use
	
	ssh [forwarded user]@127.0.0.1 -p 51021

And remember, autossh > ssh! Just replace ssh with autossh.

Start screen in background running some process

	screen -S [desired screen session name] -d -m -- sh -c '[Command to run]'

Clone one disk (/dev/sdd) to another (/dev/sdc) with dd and progress bar with pv 
(https://wiki.archlinux.org/index.php/disk_cloning#Cloning_an_entire_hard_disk)

	sudo pv -tpreb /dev/sdd | sudo dd of=/dev/sdc bs=4096 conv=notrunc,noerror,sync
