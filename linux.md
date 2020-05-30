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