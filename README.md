x1yoga3rd-linux

## newest BIOS and working fans
- verify BIOS 1.12 with EC 10.6 is installed
  - if a higher version is present downgrade first: https://download.lenovo.com/pccbbs/mobiles/n25uj10w.exe
  
- update the BIOS with fwupd (via Gnome / Ubuntu Software Center for example)
  - updating via fwupd the EC won't be updated
  
- you should now have the newest BIOS and EC 1.06
  - fans under Linux only work with EC 1.06
  
Hint: if you cannot get the EC to 1.06 you can use thinkfan

## working touchpad after suspend and lower power consumtion while suspending
- add thos parameters to your grub config under GRUB_CMDLINE_LINUX_DEFAULT:
  'acpi.ec_no_wakeup=1 psmouse.synaptics_intertouch=1'


