x1yoga3rd-linux

# X1 Yoga 3rd Generation

- added thinkfan config
- added undervolt settings (above -85mv locked up my machine)

best experience with GNOME and scaling factor 1.

To force GDM to use scaling factor 1 (and prevent window-reordering after suspend) do this:

`
sudo nano /usr/share/glib-2.0/schemas/org.gnome.desktop.interface.gschema.xml
`

`
change "scaling-factor" to 1
`

`
sudo glib-compile-schemas /usr/share/glib-2.0/schemas
`


