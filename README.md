### Topology:

```
                    +-----------+          +-----------+
                    |           |          |           |
                    |  spine1   |          |  spine2   |
                    |           |          |           |
                    +-----------+          +-----------+
+--------+        Eth1|     |Eth2          Eth1|     |Eth2
|        |            |     |                  |     |
| NMS VM |            |     |                  |     |
|        |            |   +--------------------+     |
+--------+            |   | +--------------------+   |
                  Eth1|   |Eth2              Eth1|   |Eth2
                    +-----------+          +-----------+
                    |           |          |           |
                    |   leaf1   |          |   leaf2   |
                    |           |          |           |
                    +-----------+          +-----------+
```
### Summary

- The above topology diagram describes a 4 device leaf-spine fabric based on Arista vEOS 4.16.13M, the NMS vm is an Ubuntu 14.04 LTS.
- All 5 devices were provisioned via vagrant on a windows 10 host.
- The vagrantfile and hosts file can be found [here](https://github.com/ipspace/NetOpsWorkshop/tree/master/topologies/EOS-Leaf-and-Spine).
- The nms VM has reachability to all 4 switches Management1 interface
- I've used Ansible raw module to confirm reachability and access to the device information.

### Ansible RAW output
```
vagrant@vagrant-ubuntu-trusty-64:/vagrant$ ansible all -i hosts -m raw -a 'show ver'
spine-1 | SUCCESS | rc=0 >>
Arista vEOS
Hardware version:
Serial number:
System MAC address:  0800.27d6.c3d1

Software image version: 4.16.13M
Architecture:           i386
Internal build version: 4.16.13M-6207492.41613M
Internal build ID:      5cb8b1e0-7718-4476-8f1b-21b654a9dbcb

Uptime:                 2 hours and 35 minutes
Total memory:           1643592 kB
Free memory:            60708 kB

Shared connection to 10.0.2.2 closed.


spine-2 | SUCCESS | rc=0 >>
Arista vEOS
Hardware version:
Serial number:
System MAC address:  0800.27dd.3ec8

Software image version: 4.16.13M
Architecture:           i386
Internal build version: 4.16.13M-6207492.41613M
Internal build ID:      5cb8b1e0-7718-4476-8f1b-21b654a9dbcb

Uptime:                 2 hours and 33 minutes
Total memory:           1643592 kB
Free memory:            57316 kB

Shared connection to 10.0.2.2 closed.


leaf-1 | SUCCESS | rc=0 >>
Arista vEOS
Hardware version:
Serial number:
System MAC address:  0800.27f7.45cd

Software image version: 4.16.13M
Architecture:           i386
Internal build version: 4.16.13M-6207492.41613M
Internal build ID:      5cb8b1e0-7718-4476-8f1b-21b654a9dbcb

Uptime:                 2 hours and 30 minutes
Total memory:           1643592 kB
Free memory:            59148 kB

Shared connection to 10.0.2.2 closed.


leaf-2 | SUCCESS | rc=0 >>
Arista vEOS
Hardware version:
Serial number:
System MAC address:  0800.2753.d7ca

Software image version: 4.16.13M
Architecture:           i386
Internal build version: 4.16.13M-6207492.41613M
Internal build ID:      5cb8b1e0-7718-4476-8f1b-21b654a9dbcb

Uptime:                 2 hours and 17 minutes
Total memory:           1643592 kB
Free memory:            56728 kB

Shared connection to 10.0.2.2 closed.
```
