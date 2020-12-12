# Sharing ZFS Datasets on NFS

Not enough to just configure NFS shares in /etc/exports for zfs datasets. You also need to configure zfs to share via NFS.

Example:

```
sudo zfs set sharenfs="rw=@192.168.0.0/24,rw=@10.0.0.0/24" pool-name/dataset-name`
```

Source:
https://blog.programster.org/sharing-zfs-datasets-via-nfs
