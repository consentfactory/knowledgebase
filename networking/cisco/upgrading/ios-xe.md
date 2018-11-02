# Upgrading IOS-XE
## 2960-X
Unlike upgrading 3850s, 2960-Xs are pretty straight-forward:
- Download the image
- Enter global config and configure the switch to boot to a new image.

For me, I copied the files over via FTP (faster):
```
copy ftp://172.16.1.1/c2960x-universalk9-mz.152-4.E6.bin flash:c2960x-universalk9-mz.152-4.E6.bin
```

Next, just enter global config and boot to the new image, then write to memory:
```
boot system switch all flash:c2960x-universalk9-mz.152-4.E6.bin
end
wr
```
Then reload it. Fairly simple. 
