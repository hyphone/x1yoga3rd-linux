x1yoga3rd-linux

# X1 Yoga 3rd Generation

## Requirements
- Lenovo throttle fix for iCore CPUs
  - https://github.com/erpalma/throttled
- thinkfan (shipped with most distros)
  - not needed but fans will rotate higher at high CPU temperatures (6,5k RPMs vs 4,8k RPMs) resulting in higher clock speeds

## What's in here?
- configs for:
  - lenovo throttle fix
    - undervolting
    - set HWP performance hints to "performance" when on high load and on AC
      - I saw a segnificant better and constant performance while gaming for example
    - set cTDP to 25W while on AC
      - allows the CPU to consume more power
    - set cTDP to 15W while on battery
      - turbo boost does not hold on for long but conserves power
  - thinkfan
    - reading temps from hwmon /sys/devices/virtual/thermal/thermal_zone0-1/temp instead of /proc/acpi/ibm/thermal (which seems not accurate)
    - fans will kick in at 75°c CPU temperature
      - after that they keep running until the CPU cools down to 65°c
    - usually no fans while on battery
    - enable krstresume service
      - this restarts the thinkfan service after suspend just in case
  - eGPU
    - enable gpuboot service
    - set the PCI address in /usr/sbin/egpu_detect to your GPU that is connected via Thunderbolt
      - if using AMD change "nvidia" in /etc/X11/xorg.conf.egpu to "amdgpu"
  - disables wakup possibility via XHC kernel module (had sudden wakeups from suspend because of this)
    - enable krstboot service
  - enables hibernation on Ubuntu
    - set the correct UUID of your swap in /etc/initramfs-tools/conf.d/resume

## Set the default scaling factor to 1

The 2560x1440 display is not really suitable for 2x interface scaling. I have the best experience in GNOME with a scaling factor of 1 and increasing the font size by one ammount (via keyboard shortcut).

But GDM scales back to 2 and after closing the lid and resuming GDM kicks in with the 2x scaling and GNOME Shell reverts this to 1. In the past all my windows were then rearranged because of this.

To force a system wide scaling factor by 1 and to prevent this problem I do this:

`
sudo nano /usr/share/glib-2.0/schemas/org.gnome.desktop.interface.gschema.xml
`

`
change "scaling-factor" to 1
`

`
sudo glib-compile-schemas /usr/share/glib-2.0/schemas
`


