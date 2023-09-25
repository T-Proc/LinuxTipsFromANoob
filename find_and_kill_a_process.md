<h1>Find and kill a process</h1>

<h2>Requirements:</h2>

<h3>Know what you are looking for</h3>

I am going to make a test script<br>

<h1>File: example</h1><br>

```
#!/bin/bash
#Sleep for 10 Minutes in seconds, The ampersand(&) makes it run in the background 
sleep 600 &
```

make executable<br>

```
chmod +x example # make it executable
```

I'll run it a bunch of times<br>
```
for i in {1..10}; do ./example; done
```

running ```ps -e | grep sleep``` shows all the instances of sleep<br>
```
ps -e | grep sleep
   67 tty1     00:00:00 sleep
   75 tty1     00:00:00 sleep
   77 tty1     00:00:00 sleep
   79 tty1     00:00:00 sleep
   81 tty1     00:00:00 sleep
   83 tty1     00:00:00 sleep
   85 tty1     00:00:00 sleep
   87 tty1     00:00:00 sleep
   89 tty1     00:00:00 sleep
   91 tty1     00:00:00 sleep
   93 tty1     00:00:00 sleep
```

NOW LETS KILL THEM ALL USING, kill and awk and some linux awesomeness with a one-liner!<br>
```
kill `ps -e | awk '/sleep/{print $1}'`
```
this will print out every PID and Process running,<nr>
use awk to filter for a string like grep with the //<br>
then the action you want to do in {}<br>
Now we want to print the PID which is the first string before a space (The Field Separator(FS))<br>
Luckily the PID is the first so we just tell it to print the first! with print $1 (variable 1)<br>

having the ps -e command and awk in backticks (prime) \` ` means it will forward the output to the beginning kill command (our end goal)<br>

<h1>DONE!</h1>