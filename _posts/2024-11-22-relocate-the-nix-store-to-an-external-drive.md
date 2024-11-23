---
layout: post
title: Relocate the Nix Store to An External Drive
tags: rails postgresql
---


I have an M1 base model Mac with 8GB RAM and 256GB storage, which means my disk space is very limited. My tech stack includes Flutter, Ruby on Rails, and both Mobile and Web development. When working on multiple projects simultaneously, the nix store can occupy 20–30GB, which is significant for my system.

To manage this, I followed a method inspired by (this thread)[https://discourse.nixos.org/t/how-to-move-nix-store-to-external-drive-on-macos/19592/3] and adapted it to my requirements:

**Steps to Relocate the Nix Store**

1.	Install Nix
Install Nix the conventional way. I used the [Determinate Nix Installer](https://determinate.systems/posts/determinate-nix-installer/) as it’s beginner-friendly. This creates `/nix` entries in /etc/synthetic.conf and /etc/fstab.

2.	Prepare the External Drive
I use an external drive for my projects. Open Disk Utility, create a new volume, and name it “Nix Store.” The default format is APFS, which works for this purpose.

3.	Get the Volume’s UUID
Use the terminal command `diskutil apfs list` to find the newly created volume and note down its UUID.

4.	Copy Existing Nix Store Data
Use rsync to copy the existing Nix store to the external drive. Ensure you include the trailing slash in the source path. For example:
```
sudo rsync -av /nix/ /Volumes/"Nix Store"
```

5.	Update /etc/fstab
Open the terminal and type `sudo vifs` to edit /etc/fstab. Point /nix to the external drive using its UUID. For example:
```
# nix-installer created volume labelled `Nix Store`
UUID=8044D17F-0173-4CF8-A7CD-FC303A91E18A /nix apfs rw,nobrowse,suid,owners
```

Note: Orignally, the `noauto` option is included, preventing the volume from mounting automatically. I removed it so that the volume mounts automatically.


6.	Remove the Original Nix Store
Reboot into recovery mode. Open Utilities > Terminal, and use the following commands:
- Find the /nix device name: `diskutil list`, e.g: /dev/disk2s1
- Unmount it: `diskutil unmount /dev/disk2s1` (replace with your actual device name)
- Delete it: `diskutil apfs deleteVolume /nix`

7.	Reboot

8.	Verify
Open the terminal and ensure the Nix shortcuts are sourced properly.
