# README

This fork adds a few minor patches (and definetely breaks some compat) to make this stupid driver compile on archlinux (6.14.1). If the original doesn't work for you, you might want to try this one.

## Building

```sh
git clone https://github.com/mageOfstructs/ax88179_178a
cd ax88179_178a
make
sudo make install
```

Note that this just puts the .ko file right inside `/lib/modules/<your-current-active-kernel-version>/etc...`. If you want this driver installed on a kernel other than the one you're currently running, either reboot with that kernel and redo the installation steps or change the CURRENT variable inside the makefile

## Changes

- changed `strlcpy` call to `strncpy` one: the module build context thingy didn't know the l-one and strncpy is the closest replacement. It's *technically* unsafer, but for the usage here (copying a version string) it should be completely fine.
- removed some strange RHEL macro: I just didn't wanted to put up with the preprocessor (and this fork concerns only Archlinux anyways)
- fix Makefile circular dependency: I have no idea what they were cooking but my solution works
- remove su: just call make with sudo like a normal person

## Bug Reporting

- Please report any driver bugs to upstream (although that one seems kinda ded)
- If the Makefile breaks in the future *and* you have a similar system to me (Archlinux latest), feel free to report bugs here. I may or may not react.
