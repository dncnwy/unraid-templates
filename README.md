# Spoolroom Unraid templates

Unraid templates for [Spoolroom](https://spoolroom.app).

## Spoolroom watcher

The watcher notices finished 3D prints on your network and logs them into your
Spoolroom, deducting filament from the right spools. It only makes outbound
connections: to your printers and to spoolroom.app.

1. In Spoolroom, open **Settings → Connections → Connect a Watcher**, choose
   **Unraid**, name the watcher and generate a **setup code** (eight
   characters, good for ten minutes, used once).
2. Install the template and paste the code into **Setup code**. On its first
   start the container exchanges the code for its own watcher token and keeps
   that in the State folder; the code can stay in the template or be cleared.
3. When Spoolroom shows the watcher as **Live**, add your printers under it,
   right there: **Find printers** scans your network, or add one by its
   address. The container can't see your home network's address, so Find
   printers asks for it: your NAS's own address with the last number as 0,
   then `/24` (a NAS at `192.168.1.20` means `192.168.1.0/24`). Nothing is
   typed in the container.

Prefer a terminal? The setup wizard still runs in the container's console
(click its icon, choose **Console**, run `spoolroom-setup`), and the
**Watcher token** field (advanced) takes the token itself instead of a code.

The watcher keeps itself up to date. Check it in Spoolroom under
**Settings → Connections**: the watcher shows as Live, and each printer
reports in.

### Installing without Community Apps

Save `templates/spoolroom-watcher.xml` as
`/boot/config/plugins/dockerMan/templates-user/my-spoolroom-watcher.xml` on
your Unraid flash drive, then pick it under **Docker → Add Container →
Template**.

### Good to know

- Leave Unraid's Tailscale option off for this container. The watcher has its
  own remote access, turned on from Spoolroom.
- Don't add printer variables to the container. Printers added in Spoolroom
  (or by the wizard) live in the State folder, and a container variable, even
  a blank one, would override them and could not be removed from the app.
- To remove the watcher: revoke it in Spoolroom under **Settings →
  Connections**, remove the container, and delete the State folder. Your
  printers and prints in Spoolroom stay.
- Your settings and the watcher's state live in
  `/mnt/user/appdata/spoolroom-watcher`. Keep that folder when you update or
  reinstall.

## What's in this repository

Only the template, its icon link and profile, and this README. The watcher's
code is not here: the container pairs with spoolroom.app using your code and
downloads it from there. The MIT license covers the files in this repository only.

Support: https://spoolroom.app/support
