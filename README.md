# ssh-shared-sessions
A simple experiment to demonstrate the effectiveness of ssh shared sessions.

Let's say we need to do the following to execute a particular command:

    ssh ${remote_host} mkdir /var/tmp/work
    scp run-script ${remote_host}:/var/tmp/work
    ssh ${remote_host} /var/tmp/work/run-script
    scp ${remote_host}:/var/tmp/work/result.txt
    ssh ${remote_host} rm -rf /var/tmp/work

Without using ssh shared sesions, each `ssh`/`scp` has to establish a
connetion to the remote host, setup the remote `sshd`, send the command,
close it all down.

With ssh shared sessions, the connection is established once so that the
overhead of `ssh` is not paid each time.

Simply run the experiment using `$ ssh-exp <host-name> [<# of iterations>]`
to see how fast a simple command sequence speeds up. 
