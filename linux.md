natural scroll
-----

* `synclient VertScrollDelta=-58`
* add to startup

add scrollwheel
-----
* `xinput list`
* `xinput list-props 19` "libinput Natural Scrolling Enabled (528)"
* `xinput set-prop 19 "528" 1`
* add to startup

disable keyboard
-----
#!/bin/bash
KeyboardID=`xinput --list | grep "AT Translated Set 2 keyboard" | sed 's/[^=]*=\([1-9]*\).*/\1/'`
sudo xinput set-int-prop $KeyboardID "Device Enabled" 8 0

save window displays
-----
```
#!/bin/bash
fileName="$1"
while read -r line; do
    IFS=" "
    entry=( $line )
    display=${entry[0]}
    IFS="x+"
    if [[ "${entry[2]}" == primary ]]; then
        primary=1
        measurement=( ${entry[3]} )
    else
        primary=0
        measurement=( ${entry[2]} )
    fi  
    unset IFS
    width=${measurement[0]}
    height=${measurement[1]}
    left=${measurement[2]}
    top=${measurement[3]}

    xrandrOpt="$xrandrOpt --output $display --mode ${width}x${height} --pos ${left}x${top}"
    ((primary)) && xrandrOpt="$xrandrOpt --primary"

done < <(xrandr | grep " connected")

echo $'#!/bin/bash\n'xrandr $xrandrOpt > "$fileName"
chmod +x "$fileName"                           
```
add launcher for displays
-----
add panel launcher

add ~/.local/bin to path
-----
* add to `bashrc`

generate ssh keys
-----

light locker issue w/ unlock
-----
* switch tty
* ctrl + alt + function key (other than f2 or f7)
* then go back to f2 or f7

mount sd card (exfat) on startup
-----
* `sudo blkid`
* `UUID=3732-3034 /media/joe/3732-3034               exfat   defaults,auto,umask=000,users,rw 0 0`
