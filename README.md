# Spoolroom Unraid templates

Unraid templates for [Spoolroom](https://spoolroom.app).

## Spoolroom watcher

The watcher notices finished 3D prints on your network and logs them into your
Spoolroom, deducting filament from the right spools. It only makes outbound
connections: to your printers and to spoolroom.app.

1. In Spoolroom, open **Settings → Connections → Connect a Watcher** and copy
   the watcher token (it starts with `swt_`).
2. Install the template and paste the token into **Watcher token**.
3. When the container is running, click its icon, choose **Console**, and run:

   ```sh
   spoolroom-setup
   ```

   It scans your network for printers and adds the ones you pick. The
   container can't see your home network's address, so type it when asked:
   your NAS's own address with the last number as 0, then `/24` (a NAS at
   `192.168.1.20` means `192.168.1.0/24`). Run it again to add or change a
   printer.

The watcher keeps itself up to date. Check it in Spoolroom under
**Settings → Connections**: the watcher shows as connected, and each printer
reports in.

### Installing without Community Apps

Save `templates/spoolroom-watcher.xml` as
`/boot/config/plugins/dockerMan/templates-user/my-spoolroom-watcher.xml` on
your Unraid flash drive, then pick it under **Docker → Add Container →
Template**.

### Good to know

- Leave Unraid's Tailscale option off for this container. The watcher has its
  own remote access, turned on from Spoolroom.
- Don't add printer variables to the container. The setup wizard saves your
  printers in `/data/watcher.env`, and a container variable, even a blank one,
  would override them.
- Your settings and the watcher's state live in
  `/mnt/user/appdata/spoolroom-watcher`. Keep that folder when you update or
  reinstall.

## What's in this repository

Only the template, its icon link and profile, and this README. The watcher's
code is not here: the container downloads it from spoolroom.app with your own
watcher token. The MIT license covers the files in this repository only.

Support: https://spoolroom.app/support
