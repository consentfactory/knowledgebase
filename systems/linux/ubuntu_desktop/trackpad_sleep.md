# Trackpad Sleep Issue

### Issue

Trackpad buttons seem to fail to work after waking up.

### Solution

Source: 
https://askubuntu.com/questions/1083505/ubuntu-18-04-touchpad-not-fully-working-after-wake-from-suspend

Run sudo -H gedit /lib/systemd/system-sleep/touchpad

Copy and paste in these lines:
~~~
#!/bin/bash

if [[ $1 == post ]]; then
    modprobe -r psmouse
    modprobe psmouse
fi
~~~

Save the file and exit.

Now make it a program by setting the execution bit:

~~~
chmod a+x /lib/systemd/system-sleep/touchpad
~~~

You will need to reboot for changes to take effect.
