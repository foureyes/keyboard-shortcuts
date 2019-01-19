natural scroll
-----

`synclient VertScrollDelta=-58`

disable keyboard
-----
#!/bin/bash
KeyboardID=`xinput --list | grep "AT Translated Set 2 keyboard" | sed 's/[^=]*=\([1-9]*\).*/\1/'`
sudo xinput set-int-prop $KeyboardID "Device Enabled" 8 0
