# Linux commands cheatsheet

1. Enable user root on Ubuntu (by default it is disabled).

        sudo passwd root

1. curl examples.
   
        curl google.com > site.html

        # Curl POST request with basic auth header.
        curl -k -u user:pass -X POST -H "Content-Type: application/xml" site.com

1. Pipes, output redirection and xargs.

        # Redirect stderr to /dev/null (supress stderr output).
        du / --max-depth=1 -h 2> /dev/null

        # Redirect both stdout and stderr to a file (combine them).
        du / --max-depth=1 -h 2> /tmp/output

        # Redirect stderr to stdout.
        du / --max-depth=1 -h 2>&1

        # Call mkdir command with cmdline params from stdin through a pipe. (-t to print the commands being executed)
        echo 'one two three' | xarg -t mkdir

        find . -name *.txt | xarg -t rm -f

1. Networking commands

        # Display arp table.
        arp -evn

1. Misc commands

        # list all procs that opened a specific file
        lsof /var/log/syslog

        # list all procs that opened files from a directory
        lsof +D /var/log/

        # list opened files by a specific user
        lsof -u liviu

        # list all files opened by a specific proc
        lsof -p 1456

        # kill all procs belonging to a user
        kill -9 `lsof -t -u lakshmanan`

        # list all network connections (-i4 / -i6)
        lsof -i

        # see all processes listening on a specific port
        lsof -i :ssh

        # list all TCP or UDP connections
        lsof -i tcp; lsof -i udp
