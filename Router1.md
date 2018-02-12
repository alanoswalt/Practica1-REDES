Current configuration : 2301 bytes
!
! Last configuration change at 12:05:02 UTC Thu Feb 8 2018 by cisco
version 15.1
service timestamps debug datetime msec
service timestamps log datetime msec
service password-encryption
!
hostname Router1
!
boot-start-marker
boot-end-marker
!
!
enable secret 4 tnhtc92DXBhelxjYk8LWJrPV36S2i4ntXrpb4RFmfqY
!
no aaa new-model
clock timezone UTC -6 0
!
no ipv6 cef
ip source-route
ip cef
!
!
!
!
ip dhcp pool LAN_1
 network 172.18.160.0 255.255.254.0
 domain-name labredes.com
 default-router 172.18.161.254
!
ip dhcp pool LAN_2
 network 172.18.162.0 255.255.254.0
 domain-name labredes.com
 default-router 172.18.163.254
!
!
ip domain name labredes.com
multilink bundle-name authenticated
!
!
!
!
!
crypto pki token default removal timeout 0
!
!
voice-card 0
!
!
!
!
!
!
!
license udi pid CISCO2901/K9 sn FTX161687X4
license boot module c2900 technology-package uck9
hw-module pvdm 0/0
!
!
!
vtp mode client
username cisco password 7 00071A150754
!
redundancy
!
!
ip ssh version 2
!
!
!
!
interface Loopback0
 ip address 172.18.169.30 255.255.255.224
!
interface Embedded-Service-Engine0/0
 no ip address
 shutdown
!
interface GigabitEthernet0/0
 description acceso a LAN-1
 ip address 172.18.161.254 255.255.254.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 description Acceso a LAN-2
 ip address 172.18.163.254 255.255.254.0
 duplex auto
 speed auto
!
interface Serial0/0/0
 description Acceso a la WAN-1
 ip address 172.18.168.1 255.255.255.252
 shutdown
 no fair-queue
 clock rate 8000000
!
interface Serial0/0/1
 description Acceso a WAN-1
 ip address 172.18.168.5 255.255.255.252
!
ip forward-protocol nd
!
no ip http server
no ip http secure-server
!
ip route 0.0.0.0 0.0.0.0 172.18.168.2 5
ip route 0.0.0.0 0.0.0.0 172.18.168.6 10
!
!
!
!
control-plane
!
!
!
!
mgcp profile default
!
!
!
!
!
gatekeeper
 shutdown
!
!
banner motd ^C--------Bienvenido al Router 1 Equipo:Los Rudos-----^C
!
line con 0
 logging synchronous
 login local
line aux 0
line 2
 no activation-character
 no exec
 transport preferred none
 transport input all
 transport output pad telnet rlogin lapb-ta mop udptn v120 ssh
 stopbits 1
line vty 0 4
 logging synchronous
 login local
 transport input all
line vty 5 15
 logging synchronous
 login local
 transport input all
!
scheduler allocate 20000 1000
end
