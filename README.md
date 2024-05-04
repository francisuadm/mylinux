# mylinux
my linux commands


#

I can guide you through the process of enabling NFS on your Proxmox server and accessing it from Windows 11. Here are the steps:

**On Proxmox Server:**

1. **Install NFS on Proxmox Server**: You need to install the NFS service packages on your Proxmox server. You can do this by running the following command⁴:
    ```
    sudo apt-get install nfs-kernel-server
    ```
2. **Create a Shared Directory**: Create a directory that you want to share. For example, if you want to create a directory named 'nfsproxmox' under the /var directory, you can do this⁴:
    ```
    sudo mkdir -p /var/nfsproxmox
    sudo chmod -R 777 /var/nfsproxmox/
    ```
3. **Configure NFS Export**: You need to edit the `/etc/exports` file to configure the NFS share⁴. Add a line like this to the file:
    ```
    /var/nfsproxmox *(rw,sync,no_subtree_check)
    ```
    This line means that the directory `/var/nfsproxmox` is shared with all hosts (`*`), and they have read-write access (`rw`). The changes are synced to the disk (`sync`), and the subtree check is disabled (`no_subtree_check`).

4. **Start NFS Services**: After configuring the NFS export, you need to start the NFS services⁴:
    ```
    sudo systemctl start nfs-kernel-server
    sudo systemctl enable nfs-kernel-server
    ```
5. **Configure Firewall to Allow NFS Access**: If you have a firewall enabled, you need to configure it to allow NFS access⁴. Here are the commands to do it:
    ```
    sudo ufw allow from [client-ip] to any port nfs
    sudo ufw status
    ```
    Replace `[client-ip]` with the IP address of your Windows 11 machine.

**On Windows 11:**

1. **Enable NFS on Windows 11**: You need to enable the NFS feature on Windows 11⁹. You can do this by searching for 'Turn Windows features on or off' in the Start menu, checking the box for 'Services for NFS', and clicking OK.

2. **Mount the NFS Share**: After enabling NFS on Windows 11, you can mount the NFS share¹². You can use the 'Map Network Drive' feature in File Explorer to do this. When asked for the folder, enter the NFS share in the format `\\[server-ip]\[share]`, replacing `[server-ip]` with the IP address of your Proxmox server and `[share]` with the name of the NFS share (e.g., `nfsproxmox`).

Please replace `[client-ip]` and `[server-ip]` with the actual IP addresses of your Windows 11 machine and Proxmox server, respectively. Also, please note that these instructions assume that you have sudo privileges on your Proxmox server and administrative privileges on your Windows 11 machine. If you encounter any issues, please let me know! I'm here to help. 😊

Source: Conversation with Bing, 5/3/2024
(1) How to setup an NFS Server and configure NFS Storage in Proxmox VE. https://www.howtoforge.com/tutorial/how-to-configure-nfs-storage-in-proxmox-ve/.
(2) How to Enable NFS on Windows 11. https://www.youtube.com/watch?v=oT0wDJcZi6E.
(3) How to map NFS shares on Windows 11 - Addictive Tips Guide. https://www.addictivetips.com/windows-tips/how-to-map-nfs-shares-on-windows-11/.
(4) How to Setting up an NFS Server (To Store VMs, LXCs, or Data) in Proxmox. https://www.youtube.com/watch?v=XBzp-2hleZ0.
(5) NFS server in Proxmox CT. https://www.youtube.com/watch?v=RW2L5Pa6aCM.
(6) How To Setup NFS Shared Storage In Proxmox. https://www.youtube.com/watch?v=txx0z-4HlSQ.
(7) Storage: NFS - Proxmox VE. https://pve.proxmox.com/wiki/Storage:_NFS.
(8) Rackzar - How to connect Proxmox to Network NFS mount. https://help.rackzar.com/en/knowledgebase/article/how-to-connect-proxmox-to-network-nfs-mount.
(9) Sharing local storage as SMB or NFS share - Proxmox Support Forum. https://forum.proxmox.com/threads/sharing-local-storage-as-smb-or-nfs-share.68330/.
(10) Add NFS Proxmox | A Quick Guide - Bobcares. https://bobcares.com/blog/add-nfs-proxmox/.
(11) How to enable NFS on Windows 11 (QUICK). https://www.youtube.com/watch?v=uBsp17krQZo.
(12) Enable NFS on Windows 10/11 || How to Activate Network File System (NFS) Protocol in Windows 10/11. https://www.youtube.com/watch?v=N7zUR0gz-dY.
(13) Exploring Windows 11 NFS Client: A Comprehensive Guide. https://www.howto-do.it/a-windows-11-nfs-client-step-by-step/.
(14) How to access network shared folder on Windows 11. https://pureinfotech.com/access-network-shared-folder-windows-11/.
(15) Deploy Network File System | Microsoft Learn. https://learn.microsoft.com/en-us/windows-server/storage/nfs/deploy-nfs.
(16) How to access NFS shares from Windows OS – Zadara Support. https://support.zadarastorage.com/hc/en-us/articles/213024566-How-to-access-NFS-shares-from-Windows-OS.
(17) undefined. https://192.168.1.111:8006/.
