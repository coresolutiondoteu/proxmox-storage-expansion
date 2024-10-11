# proxmox-storage-expansion

Case: You have started Proxmox server with smaller drive and would like to grow it with bigger drive (upgrade).

Steps:
1) Get Clonezilla to USB drive (use Rufus, etc. for bootable USB), boot and make disk clone to new disk
2) Get Gparted to USB drive and boot with the new drive attached
3) Exapnd the thir partiiton on the new disk into the free space
4) There is no root, so use sudo for command in the terminal, which you will use now
5) Couple of the useful commands:
   
   lvs,
   vgs,
   pvs,
   df -h
   
7) First expand the metadata as the LVM is Thin in Proxmox and thin can't be shrinked
8) lvextend -L +10G /dev/pve/data_tmeta

   +10G is there to expand the metadata for 10GiB, however this is depended on how you will use metadata (in general https://access.redhat.com/solutions/6318131)

10) Now you can expnad the actual thin pool
11) lvextend -L +300G /dev/pve/data
12) Check the sizes with the lvs, vgs, pvs
13) If all is good for now, you can put the drive back to the server and woila!
