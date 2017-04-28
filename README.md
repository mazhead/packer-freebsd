# FreeBSD Packer Templates

Creates FreeBSD images using official `disk1.iso` snapshot and release media.

Common Workflow:
```sh
% ./automatic-11.0-release-zfs.sh
% vagrant up
% vagrant ssh
% vagrant destroy
```

Images supported:
* Virtualbox + Vagrant

Prerequisites:
* Install [Vagrant](https://www.vagrantup.com)
* Install [Packer](https://www.packer.io/)
* Clone this repo onto your machine

Notes:
* The VM is set to have 1024MB of RAM and a 20GB drive
* When bringing Vagrant boxes up for the first time, you will need `sudo`
  privileges on the host machine (i.e. your laptop) to add entries to
  `/etc/exports` in order to allow Vagrant to mount `/vagrant` in the guest.
  See
  [Vagrant NFS synced folders](https://docs.vagrantup.com/v2/synced-folders/nfs.html)

## FreeBSD `11.0-RELEASE`

To create a Vagrant box for `11.0-RELEASE` using a ZFS filesystem:

```sh
% ./automatic-11.0-release-zfs.sh
```

## Debugging Builds

The following are "common" problems with workarounds:

1. Packer fails because the `bsdinstall` menus have changed. Solution: Change `"headless": "true"` to
   `"false"`, add the `-debug` flag to `packer build` and submit a patch
   fixing the menu change.

2. Packer fails to connect via SSH to the instance to do the post-install.
   Possible solution: There are too many SSH keys loaded in your agent.
   Prefix your command with `env SSH_AUTH_SOCK=/dev/null ...`
