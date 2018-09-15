# Spanning Tree Notes

## VSTP

### Cisco and Juniper
On Cisco side, rapid-pvst needs to be enabled.

### Base config
  set protocols vstp interface all bpdu-timeout-action block
  set protocols vstp vlan all
  set protocols vstp interface ge-x/x/x edge (access ports)
  set protocols vstp interface ge-x/x/x no-root-port (downstream trunk ports)

### VSTP port limits
 https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/layer-2/layer-2-spanning-tree-protocols.pdf
 Page 28: “VSTP supports a limited number of ports compared to RSTP.”
 I suspect around 300 ports is the maximum number of ports supported (20180816).
 When port limit reached, find active ports and configure edge for them
