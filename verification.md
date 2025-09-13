# Verification – Week 1 VLAN Lab

## SW1

SW1#sh vlan br

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/4, Fa0/5, Fa0/6, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Gig0/1
                                                Gig0/2
10   VLAN10                           active    Fa0/1, Fa0/2, Fa0/3
20   VLAN20                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

##SW2


SW2#sh vlan br

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/4, Fa0/5, Fa0/6, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Gig0/1, Gig0/2
10   VLAN10                           active    
20   VLAN20                           active    Fa0/1, Fa0/2, Fa0/3
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active  
  
### show interfaces trunk SW1

SW1#show interface trunk
Port        Mode         Encapsulation  Status        Native vlan
Fa0/23      on           802.1q         trunking      1
Fa0/24      on           802.1q         trunking      1

Port        Vlans allowed on trunk
Fa0/23      10,20
Fa0/24      10,20

Port        Vlans allowed and active in management domain
Fa0/23      10,20
Fa0/24      10,20

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/23      10,20
Fa0/24      10,20

### show interfaces trunk SW2

SW2#show interface trunk
Port        Mode         Encapsulation  Status        Native vlan
Fa0/24      on           802.1q         trunking      1

Port        Vlans allowed on trunk
Fa0/24      10,20

Port        Vlans allowed and active in management domain
Fa0/24      10,20

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/24      10,20


### show mac address table SW1

SW1#show mac address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

   1    0001.4290.4901    DYNAMIC     Fa0/23
   1    0050.0f22.5718    DYNAMIC     Fa0/24
  10    0001.4290.4901    DYNAMIC     Fa0/23
  20    0001.4290.4901    DYNAMIC     Fa0/23


### show mac address table SW2

SW2#show mac address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

   1    0060.7097.6c18    DYNAMIC     Fa0/24
  10    0060.7097.6c18    DYNAMIC     Fa0/24
  20    0060.7097.6c18    DYNAMIC     Fa0/24


## R1
RTR1#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     unassigned      YES unset  up                    up 
GigabitEthernet0/0.10  192.168.10.1    YES manual up                    up 
GigabitEthernet0/0.20  192.168.20.1    YES manual up                    up 
GigabitEthernet0/1     unassigned      YES unset  administratively down down 
Vlan1                  unassigned      YES unset  administratively down down


## R1 show ip route 

RTR1#show ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

     192.168.10.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.10.0/24 is directly connected, GigabitEthernet0/0.10
L       192.168.10.1/32 is directly connected, GigabitEthernet0/0.10
     192.168.20.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.20.0/24 is directly connected, GigabitEthernet0/0.20
L       192.168.20.1/32 is directly connected, GigabitEthernet0/0.20


## Pings
- PC1 (192.168.10.10) → PC4 (192.168.20.10): SUCCESS
C:\>ping 192.168.20.10

Pinging 192.168.20.10 with 32 bytes of data:

Reply from 192.168.20.10: bytes=32 time<1ms TTL=127
Reply from 192.168.20.10: bytes=32 time=11ms TTL=127
Reply from 192.168.20.10: bytes=32 time<1ms TTL=127
Reply from 192.168.20.10: bytes=32 time=1ms TTL=127

Ping statistics for 192.168.20.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 11ms, Average = 3ms

- PC2 (192.168.10.11) → PC5 (192.168.20.11): SUCCESS
C:\>ping 192.168.20.11

Pinging 192.168.20.11 with 32 bytes of data:

Reply from 192.168.20.11: bytes=32 time<1ms TTL=127
Reply from 192.168.20.11: bytes=32 time=11ms TTL=127
Reply from 192.168.20.11: bytes=32 time=1ms TTL=127
Reply from 192.168.20.11: bytes=32 time<1ms TTL=127

Ping statistics for 192.168.20.11:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 11ms, Average = 3ms


- PC3 (192.168.10.12) → PC6 (192.168.20.12): SUCCESS
C:\>ping 192.168.20.12

Pinging 192.168.20.12 with 32 bytes of data:

Reply from 192.168.20.12: bytes=32 time<1ms TTL=127
Reply from 192.168.20.12: bytes=32 time=12ms TTL=127
Reply from 192.168.20.12: bytes=32 time=1ms TTL=127
Reply from 192.168.20.12: bytes=32 time=1ms TTL=127

Ping statistics for 192.168.20.12:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 12ms, Average = 3ms