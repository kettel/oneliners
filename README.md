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

Calculate nof rows in in all php-files in current dir and it's subdirs
	find . -name '*.php' | wc -l
