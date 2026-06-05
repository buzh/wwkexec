An overlay for Warewulf 4.x which uses `kexec` to warm boot into a new node image.

Usage:

- Create the overlay on the ww server, adding files from repo
- Add it to the node/profile runtime overlays
- Change a node/profile image to the one you wish to boot into
- Run `wwctl overlay build <node>` (optional, but recommended)
- Trigger the warm boot with `ssh <node> systemctl start wwkexec.service`
- Wait ca 1 minute and confirm that the new image is loaded and running
