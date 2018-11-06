## Configuring LACP Between Cisco IOS-XE and Juniper JunOS

Configuring basic LACP between Cisco IOS-XE and Juniper JunOS is a little tricky on the Juniper side of things.

### Cisco

For Cisco, it's just a standard LACP configuration. Configure the individual interfaces with the channel group number corresponding with the port group interface. Mode 'Active' indicates we're using LACP instead of Etherchannel:

```
interface GigabitEthernet1/0/1
 description <Super Descriptive Description>
 channel-group 1 mode active
!
interface GigabitEthernet1/0/2
 description <Super Descriptive Description>
 channel-group 1 mode active
end
```

Then configure your port channel group like you want it to be:

```
interface Port-channel1
 description <We always document things, right? RIGHT?>
 switchport trunk native vlan 99
 switchport mode trunk
end
```

### Juniper

My personal opinion is that the Juniper configuration is a tad more hairy (but that tends to be how Juniper configs are anyways compared to Cisco -- again, my opinion).

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
set interfaces ae0 unit 0 family ethernet-switching interface-mode trunk
set interfaces ae0 unit 0 family ethernet-switching vlan members all
```

Commit the changes and you're done. Right? Not so fast. There's one interoperability issue that you'll want to address before committing these changes. 

You need to configure the minimum number of links for LACP to run on if one of the interfaces go down. In a two interface setup, like this one, Cisco defaults to running LACP with at least one interface online. Juniper, however, does not, so we have to set the minimum number to one:

```
set interfaces ae0 aggregated-ether-options minimum-links 1
```

That's it. 
