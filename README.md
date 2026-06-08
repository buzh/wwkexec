# wwkexec

An overlay for Warewulf 4.x which uses `kexec` to warm boot into a new node image

Created by Andreas Skau, Research Computing Services, University of Oslo (2026)
https://github.com/buzh

# Installation:

```
cd /path/to/overlays
git clone https://github.com/buzh/wwkexec
wwctl profile edit default # add wwkexec to runtime overlays, default profile just an example - adapt as needed
wwctl overlay build # give it a minute so the new overlays are propagated
```

# Usage (manual)

`ssh <nodename> systemctl start wwkexec.service`

# Using with Slurm

With slurm's built-in `reboot` method we can automatically trigger reloading a new image
without interfering with running jobs.

In slurm.conf set:

`RebootProgram=/usr/bin/systemctl start wwkexec.service`

...or write a wrapper script that takes any additional steps you might need.

Configure the nodes to load a new image, then:

`wwctl overlay build` (optional but recommended - if you don't, the old image name will be displayed by /etc/issue by default)

`scontrol reboot asap <node(s)>`

That's it! Sit back and watch the new image be rolled out.
