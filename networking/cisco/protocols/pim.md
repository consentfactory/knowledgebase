# PIM

## PIM and HSRP 

Encountered issue where we had PIM configured on two routers in a HSRP group. However, when large
quantities of multicast groups were being created/sent, we started having packets not being
received. 

The issue was that the designated router in PIM didn't have any priority set (so default 100 on each), so while HSRP was
active on one router's VLAN, PIM was using both routers in a round-robin fashion.

The solution was simple: set a higher DR priority for the same router that has the higher priority
in HSRP.

Config:
```
# Router1 (that has higher HSRP)
int vlan 100
 ip pim dr-priority 150

# Router2
int vlan 100
 ip pim dr-priority 100 #(which is default, so no need to config)
```
