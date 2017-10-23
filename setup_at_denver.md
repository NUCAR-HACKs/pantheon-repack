# Shipping to Denver

Be sure to properly label which node is in which box before shipping. Network
interface setup is hardcoded for each NIC, and misconnecting NICs will cause
links to fail.

# Setting Up the Hardware
## Network Interfaces

The nodes have 4 Ethernet NICs, and one NIC for power management that will go
unused at the competition. The NICs are numbered `eno1` through `eno4`,
physically broken out on the back of the node in the below layout.

| eno3 | eno4 |
| ---- | ---- |
| eno1 | eno2 |

The interface MAC addresses are sequentially assigned. This is used to assign
hostnames at OS install time, and configure the network interfaces by files in
`/etc/network/interfaces.d`.

| node | eno1 | eno2 | eno3 | eno4 |
| ---- |
| pantheon-0 | 0c:c4:7a:fa:32:96 | 0c:c4:7a:fa:32:97 | 0c:c4:7a:fa:32:98 | 0c:c4:7a:fa:32:99 |
| pantheon-1 | 0c:c4:7a:fa:33:ee | 0c:c4:7a:fa:33:ef | 0c:c4:7a:fa:33:f0 | 0c:c4:7a:fa:33:f1 |
| pantheon-2 | 0c:c4:7a:fa:32:ca | 0c:c4:7a:fa:32:cb | 0c:c4:7a:fa:32:cc | 0c:c4:7a:fa:32:cd |
| pantheon-3 | 0c:c4:7a:fa:32:ce | 0c:c4:7a:fa:32:cf | 0c:c4:7a:fa:32:d0 | 0c:c4:7a:fa:32:d1 |

Each node's `eno1` is configured for DHCP, and should be connected to the
external network. The remaining NICs are used to setup a fully connected network
between the nodes. The rules for this network are below:

### Connecting the Nodes
#### Node 0
Node 0's `eno(k+1)` should be connected to Node k's `eno(k+1)`.

#### Node n
Node n's `eno(k+1)` should be connected to Node k's `eno(k+1)` except for k=n,
in which case `eno(n+1)` should be connected to Node 0's `eno(n+1)`.

#### Diagram
