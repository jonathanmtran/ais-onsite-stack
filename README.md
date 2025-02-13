# Onsite Stack

This is an Ansible playbook that installs and configures the following:

* Samba
* Docker
* PhotoPrism
* Sanoid

This stack was deployed and used in January 2025. There were bugs.

## Background

I needed a server for the following functions:

* File share (Samba) to
  * store files (audio/video/slide decks/etc)
  * be an ingest target for photos and videos
* Run a web-based photo viewer (PhotoPrism) to facilitate
  * selecting photos for printing
  * curating photos for a (background) slideshow

## License
MIT

## Usage

Enable the Debian Backports repository and install ZFS
```shell
# apt install zfs-dkms zfsutils-linux
```

Create ZFS pool named `tank` (note `o` vs `O`)
```shell
# zpool create -R /mnt -o ashift=12 -O xattr=sa -O compression=lz4 -O atime=off -o autotrim=on tank <partition>
```

Create ZFS datasets
```shell
# zfs create tank/group
# zfs create tank/group/aliveinspirit
# zfs create tank/group/aliveinspirit/AIS_2025
```

Execute playbook
```shell
$ ansible-playbook playbook.yml
```

Create SMB user
```shell
# smbpasswd -a ais
```
