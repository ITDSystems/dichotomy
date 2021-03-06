#CF API

We use ManageIQ now (CF upstream), since current CF has no REST API. Current ManageIQ should become supportable CF (and bring REST to CF) this September. APIs:

### Main Info for Dihotomy
1. [Docs on Apiary](http://docs.dihotomy.apiary.io/)
2. [Mock Server](http://dihotomy.apiary-mock.com/)
3. [Domain Specific Permissions](https://github.com/ITDSystems/dichotomy/wiki/List-of-Permissions)

### Complete Official Docs
1. [Design spec](http://manageiq.org/documentation/development/rest_api/design/)
2. [Reference](http://manageiq.org/documentation/development/rest_api/reference/)


#Test Infra

### VPN
* Type: OpenVPN
* Gate: host4.itdhq.com
* Certs: ping me in private


### Networking
Every machine is connected to two networks:
* VPN network - 10.8.0.X/24 - so, you can access it directly
* Internal network - 192.168.1.X/24 - for faster interconnect

### AD
* Windows 2008 R2
* IP on VPN network - 10.8.0.201
* IP on internal network - 192.168.1.150
* Domain: example.loc
* Admin login: Administrator / qwer1234@

### vCenter
* Windows 2008 R2
* vCenter 5.5
* IP on VPN network - 10.8.0.209
* IP on internal network - 192.168.1.15
* SSO Admin URL: https://vcenter:9443/vsphere-client/
* SSO Admin: Administrator@example.loc / qwer1234@

### ManageIQ
* CentOS 6.4
* ManageIQ latest ([install from sources instruction](http://manageiq.org/community/install-from-source/))
* IP on VPN network - 10.8.0.213
* IP on internal network - 192.168.1.17
* Admin URL: http://cloudforms:3000/
* Admin login: admin / smartvm
* Provides all APIs described at http://docs.dihotomy.apiary.io/

### CloudForms
* CentOS 6.4
* CloudForms 3.1
* IP on VPN network - 10.8.0.81
* IP on internal network - 192.168.1.16
* Admin URL: http://cloudforms/
* Admin login: admin / smartvm
* Provides all APIs described at http://docs.dihotomy.apiary.io/

### CloudForms
* CloudForms 3.2
* IP on internal network - 192.168.1.111
* Admin URL: http://192.168.1.111/
* Admin login: admin / smartvm

### KVM host
* CentOS 6.4
* IP on VPN network - 10.8.0.197
* IP on internal network - 192.168.1.104
* Admin login - root / password

### Arch + Docker host
* IP on VPN network - 10.8.0.221
* IP on internal network - 192.168.1.105
* Admin login - root / qwe123#

### VMware 5.5 host
* VMware 5.5 ESXi
* IP on VPN network - none
* IP on internal network - 192.168.1.3
* Admin login - root / password

### VMware 6.0 host
* VMware 6.0 ESXi
* IP on VPN network - none
* IP on internal network - 192.168.1.103
* Admin login - root / password

### VMware 6.0 vCenter
* Deployed from appliance (no OS manual install procedure)
* vCenter 6.0
* IP on VPN network - not yet
* IP on internal network - 192.168.1.110
* SSO Admin URL: https://192.168.1.110
* SSO Admin: Administrator@example.loc / 123qweASD!

### JBoss Application Server
* CentOS 6.4
* IP on VPN network - 10.8.0.217
* IP on internal network - 192.168.1.65
* Admin login - root / password
* JBoss EAP 6.3 - see root's home
* Check CF access - wget http://admin:smartvm@cloudforms:3000/api/dihotomy/pools

### Redmine (Service Desk)
* CentOS 6.4
* IP on VPN network - 10.8.0.105
* IP on internal network - 192.168.1.66
* Admin login - root / password

### IPAM
* Centos
* IP on internal network - 192.168.1.68
* Admin login - root / redhat
* IPAM web - admin / 123qweASD

#Helpers

### Obvious candidates for /etc/hosts:
```
10.8.0.1	vpn
10.8.0.197	bender
10.8.0.201	ad
10.8.0.209	vcenter
10.8.0.213	cloudforms
10.8.0.213	cloudforms
10.8.0.217	jbosseap
10.8.0.105	redmine
```

### Query AD for users from command line:
```
ldapsearch -x -h 10.8.0.201 -D "Administrator@example.loc" -W -b "cn=users,dc=example,dc=loc" -s sub "(cn=\*)" cn mail sn
```

### Connect to AD with RDP:
From VPN: ```xfreerdp /u:Administrator /d:example.loc /p:qwer1234\@ /v:10.8.0.201```

From LAN: ```xfreerdp /u:Administrator /d:example.loc /p:qwer1234\@ /v:192.168.1.150```
