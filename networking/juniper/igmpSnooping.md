# IGMP Snooping

## IGMP Snooping, Cisco Interoperperability, and PIM

I found the following configuration to work best the PIM protocol and interoperability with CIsco routers:
```
protocols {
  igmp-snooping {
    vlan all {
      query-interval 60;
      immediate-leave;
    }
  }
}
```
This is assuming Juniper for access/edge to Cisco routing.
