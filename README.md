x1yoga3rd-linux

I bought a Lenovo X1 Yoga recently to run GNU/Linux exclusivly. As it turned out there are some hickups to overcome.

Usually users complain about not working fans with the newest BIOS in combination with the newest EC firmware. Both get updated with Windows at the same time.

There is a trick to get the newest BIOS and keep an older EC. One has to downgrade to BIOS 1.12 so EC is downgraded to 1.06. The fans are working fine now.

When someone updates the BIOS through GNU/Linux now via fwupd (through Gnome Software for example) the EC does not get updated so someone can have the newest BIOS and an older EC to have working fans.

There is one issue though. When the EC is at 1.06 there are other issues like keyboard and trackpad not respondig after suspend and flickering keyboard backlight.

What I encountered is when the BIOS is downgraded via Windows to 1.12 / 1.06, then updated via GNU/Linux to 1.27 / 1.06 (EC stays the same) and then the BIOS gets updated again through Windows to the newest 1.27 / 1.09 the fans are still working. And so is the keyboard, trackpad and keyboard backlight after suspend.

So the procedure to have everything working is this:

## newest BIOS / EC and working fans
- verify BIOS 1.12 with EC 10.6 is installed
  - if a higher version is present downgrade first: https://download.lenovo.com/pccbbs/mobiles/n25uj10w.exe
  
- update the BIOS to the newest version with fwupd (via Gnome / Ubuntu Software Center for example)
  - updating via fwupd the EC won't be updated
  - you should now have the newest BIOS and EC 1.06

- update the BIOS to the newest version with Windows
  - you should now have the newest BIOS and the newest EC with working fans under GNU/Linux without the need of "thinkfan"
  
## prevent sudden wakeups from sleep
I had some wakeups after putting the machine to sleep. I don't exactly know the reason but disabling XHC from the allowed wakeups helped and the X1Y3 sleeps like it should. This will disable the ability to wake the machine from USB devices I suppose.

- add this to a startup script:
  
  ```echo "XHC" > /proc/acpi/wakeup```

## since Kernel 4.18 and the BIOS updated as stated above I couldn't find any other issue for now (state December 2018)
- s2idle power consumption is acceptable
- idle while power on consumes about 5+ watts
- SD card reader does not consume useless power like users of the X1 Carbon 6 experience
- GRUB parameter ```acpi.ec_no_wakeup=1``` is not needed anymore since Kernel 4.18 to prevent wakeups caused by the EC
- touchpad / trackpoint / keyboard are working reliably after suspend

## so back to work :)

