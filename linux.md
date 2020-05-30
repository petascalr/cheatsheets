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

1. lsof

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

1. netstat

        netstat -a              ;; show both listening and non listening ports.
        netstat -at             ;; show all tcp ports.
        netstat -au             ;; show all udp ports.
        netstat -l              ;; show only listening ports
        netstat -lt             ;; show listening tcp ports
        netstat -lu             ;; show listening udp ports
        netstat -lx             ;; show listening UNIX ports
        netstat -s              ;; show statistics for all ports.
        netstat -st             ;; show statistics for tcp ports. -su for udp ports.
        netstat -p              ;; show program names
        netstat -nutlp          ;; show listening tcp and udp ports with numeric (no name resolution) and program name

1. route

        route -n                ;; print routing table and don't perform name resolution

        # Add default route through intf eth0 to gw 192.168.1.254
        route add default gw 192.168.1.254 eth0

1. Misc commands

        # print disk usage by folder sorted by size
        sudo du / --max-depth=1 -h 2> /dev/null | sort -hr

        # Prepend location to PATH
        PATH=/home/liviu/app:$PATH