---
layout: post
title: Put Nix Store At External Drive
tags: rails postgresql
---


### Why

I have a M1 base model (8g + 256g). So that my disk space is very limited. My stack includes Flutter, Ruby on Rails, Pyhton. When I work on several projects simultaneously, `nix store` will usually take 20 ~ 30G, which is a lot for my disk.

### What

1. Install nix in a conventional way. This will create /nix entry in /etc/synthetic.conf and /nix entry in /etc/fstab.
2. Connect external drive. I formatted it to encrypted, case-sensitive APFS. Save the disk’s UUID (it’s shown in Disk Utility info and in diskutil apfs list). rsync the contents of /nix to this drive.
3. Delete the /nix disk created by the installer with sudo diskutil apfs deleteVolume /nix.
4. Using sudo vifs, edit /etc/fstab to point /nix to your disk’s UUID. For me,
mateusz@Mateuszs-MacBook-Pro ~ % cat /etc/fstab 
UUID=EBC0B7AA-1BD5-4F56-A677-6BDD47AC95F5 /nix apfs rw,noauto,nobrowse,suid,owners
This way, your disk will be automatically mounted to /nix when connected.

5. Reboot.
6. Connect the disk, if it’s not connected. With noauto it shouldn’t mount automatically; open Disk Utility and mount. This should automatically mount it to /nix.
7. Voila! Open the terminal and see whether the shortcuts to nix are sourced properly.


### How

- We should ask locally running psql server to handle all in-development client. Rather than create psql server for each client.

### Where


### When



**References**:

- [Nix Language Basics](https://nix.dev/tutorials/nix-language)

- ['nix shell' vs 'nix develop'](https://www.reddit.com/r/NixOS/comments/r15hx4/nix_shell_vs_nix_develop/)