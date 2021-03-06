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

emoji
-----
### display

Get emoji font if u don't already have it (for example xubuntu):

`sudo apt-get install fonts-noto-color-emoji`

For Chrome/Firefox: in `~/.config/fontconfig/conf.d/01-emoji.conf`:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <alias>
    <family>serif</family>
    <prefer>
      <family>Noto Color Emoji</family>
    </prefer>
  </alias>
  <alias>
    <family>sans-serif</family>
    <prefer>
      <family>Noto Color Emoji</family>
    </prefer>
  </alias>
  <alias>
    <family>monospace</family>
    <prefer>
      <family>Noto Color Emoji</family>
    </prefer>
  </alias>
</fontconfig>
```


### write

packages:

* ibus
* ibus-gtk
* ibus-gtk3
* ibus-table

```
sudo apt install ibus
git clone https://github.com/salty-horse/ibus-uniemoji.git
cd ibus-uniemoji
sudo make install
ibus restart
```

* run: `ibus-setup`
* add unimoji


see [how-to](https://hk.saowen.com/a/250f4270055aaa3ddeeaed38c981f4f3e1c8dff159f274c5e114722a6353453f)
