# PPPoE Configuration Lab

## Overview
This lab demonstrates PPPoE (Point-to-Point Protocol over Ethernet) 
configuration between a Customer (PPPoE Client) and an ISP (PPPoE Server), 
simulating a real-world broadband access scenario, built and tested in EVE-NG.

## Topology
- Customer Router — configured as PPPoE Client (e1/0)
- ISP Router — configured as PPPoE Server (e1/0)
- Link: /30 subnet — 112.1.1.0/30

## Key Concepts Covered
- Dialer interface configuration on client side
- PPP encapsulation over Ethernet
- BBA (Broadband Access) group configuration on ISP side
- Virtual-template interface for dynamic PPP session assignment
- Dialer pool binding to physical interface

## Configuration

### Customer Side (PPPoE Client)
\
interface e1/0
 no shut
 exit
interface dialer 10
 encapsulation ppp
 ip address 112.1.1.2 255.255.255.0
 dialer pool 5
 exit
interface e1/0
 pppoe-client dial-pool-number 5
\
### ISP Side (PPPoE Server)
\
interface e1/0
 no shut
interface virtual-template 11
 ip address 112.1.1.1 255.255.255.0
 exit
bba group pppoe CCNA
 virtual-template 11
 exit
interface e1/0
 pppoe enable group CCNA
\
## Verification
- show pppoe session
- show interface dialer 10
- show ip interface brief

## Tools Used
- EVE-NG (Cisco IOL/IOSv images)
