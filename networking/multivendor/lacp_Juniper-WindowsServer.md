## Configuring LACP Between Juniper JunOS and Windows Server

Configuring basic LACP between Cisco IOS-XE and Juniper JunOS is a little tricky on the Juniper side of things.

### Windows Server

I'm lazy and don't want to write this out, so check out these instructions:

https://blogs.technet.microsoft.com/uspartner_ts2team/2012/09/25/nic-teaming-in-windows-server-2012/

Basically, set up a NIC team in LACP mode, set your load balancing mode and click ok. Basically. Super basic. For load balance modes, check this out:

https://technet.microsoft.com/en-us/library/mt179276.aspx#bkmk_lb

### Juniper

First, configure the interfaces:

```
set interfaces ge-0/0/0 ether-options 802.3ad ae0
set interfaces ge-0/0/0 description "<Super Descriptive Description>"
set interfaces ge-0/0/1 ether-options 802.3ad ae0
set interfaces ge-0/0/1 description "<Super Descriptive Description>"
```

Next, configure the aggregated ethernet port:

```
set interfaces ae0 description "<We always document things, right? RIGHT?>"
set interfaces ae0 native-vlan-id 99
set interfaces ae0 aggregated-ether-options lacp active
set interfaces ae0 aggregated-ether-options minimum-links 1
set interfaces ae0 unit 0 family ethernet-switching interface-mode trunk
set interfaces ae0 unit 0 family ethernet-switching vlan members all
```

Final config looks like this:

```
ae0 {
    description "<We always document things, right? RIGHT?>";
    native-vlan-id 99;
    aggregated-ether-options {
        minimum-links 1;
        lacp {
            active;
        }
    }
    unit 0 {
        family ethernet-switching {
            interface-mode trunk;
            vlan {
                members all;
            }
        }
    }
}
```

That's it. 
