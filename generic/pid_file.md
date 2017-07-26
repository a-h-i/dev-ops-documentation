
When you have multiple processes running, sometimes you want to manage them or just check on their status. The children they have, etc.

Maybe you want to kill them, halt them, send some any signal that triggers certain code in that program.

well a pidfile is where a process or a launcer writes the *P*rocess *I*dentifier, simply a number.

For each pid you can find a directory with it's details including a virtual memory map file under `/proc/<pid>` directory.

Many launchers and process managers such as uwsgi for django, as an example uses a pid file to keep track of the instances it launched of your application and kill them when you redeploy.
It can also send them signals to die after they are done processing the current request if any
