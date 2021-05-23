# Removing CDP Duplex Mismatch from Console 

The following console message will flood the console when working in EVE-NG on some Cisco images:

```
%CDP-4-DUPLEX_MISMATCH: duplex mismatch discovered on GigabitEthernet1/3 (not half duplex), with Internet Ethernet0/0 (half duplex).
```

There are two fixes for this. 

First is to try to configure CDP to ignore the messages in the log:

```
no cdp log mismatch duplex
```

However, this only works on recent/updated images. If you're working from old images, the following will work:

```
logging discriminator DROPCDP msg-body drops duplex
logging buffered discriminator DROPCDP
logging console discriminator DROPCDP
```
