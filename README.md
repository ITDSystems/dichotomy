##CF API

We use ManageIQ now (CF upstream), since current CF has no REST API. Current ManageIQ should become supportable CF (and bring REST to CF) this September. APIs:
1. [Design spec](http://manageiq.org/documentation/development/rest_api/design/)
2. [Reference](http://manageiq.org/documentation/development/rest_api/reference/)

##Test Infra

1. Everything is on VPN. Connection params:
* Type: OpenVPN
* Gate: host4.itdhq.com
* Certs: ping me in private

2. Networking
Every machine is connected to two networks:
* VPN network - 10.8.0.X/24 - so, you can access it directly
* Internal network - 192.168.1.X/24 - for faster interconnect

3. AD
* Windows 2008 R2
* IP on VPN network - 10.8.0.201
* IP on internal network - 192.168.1.150
* Domain: example.loc
* Admin login: Administrator / qwe123#

4. vCenter
* Windows 2008 R2
* vCenter 5.5
* IP on VPN network - 10.8.0.209
* IP on internal network - 192.168.1.15
* Admin URL: https://vcenter:9443/vsphere-client/
* Admin login: Administrator / qwe123#

5. CloudForms (ManageIQ actually)
* CentOS 6.4
* ManageIQ latest [install from sources instruction](http://manageiq.org/community/install-from-source/)
* IP on VPN network - 10.8.0.213
* IP on internal network - 192.168.1.17
* Admin URL: http://cloudforms:3000/
* Admin login: admin / smartvm

6. KVM host
* CentOS 6.4
* IP on VPN network - 10.8.0.197
* IP on internal network - 192.168.1.104
* Admin login - root / password

7. VMware host
* VMware 5.5 ESXi
* IP on VPN network - none
* IP on internal network - 192.168.1.3
* Admin login - root / password

##Helpers

1. Obvious candidates for /etc/hosts:
10.8.0.1	vpn
10.8.0.197	bender
10.8.0.201	ad
10.8.0.209	vcenter
10.8.0.213	cloudforms

2. Query AD for users from command line:
ldapsearch -x -h 10.8.0.201 -D "Administrator@example.loc" -W -b "cn=users,dc=example,dc=loc" -s sub "(cn=\*)" cn mail sn

3. Connect to AD with RDP:
From VPN: xfreerdp -u Administrator -d example.loc -p qwe123# 10.8.0.201
From LAN: xfreerdp -u Administrator -d example.loc -p qwe123# 192.168.1.150
