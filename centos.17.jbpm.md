## CentOs 7 64bit
---


  SO     : CentOS-7-x86_64-Minimal-1908
  Name   : CenSer17.jbpm
  CPU    : 1
  Memoria: 8192Mb
  Disco  : CenSer17.jbpm.Disk01 20Gb Tipo VirtualMachine Disk (VMDK)
  Red    : 1.- VirtualBox Host-Only (tipo de tarjeta de Red virtio-net)
           2.- NAT Network (tipo de tarjeta de Red virtio-net)

-----------------------
--  Manual Partition --
-----------------------

--------------------
--Guia.File.System--
--------------------
Disk01
  /       1 GiB 
  /usr    5 GiB
  /tmp    2 GiB
  /var    5 GiB
  /home   2 GiB
  /boot   1 GiB
  /opt    2 GiB
  swap    2 GiB

  user  : root
  passwd: 919094

  Activar las Redes en Instalacions
  Definir Host name jbpm-n01

------------------
--Configurar Red--
------------------
  nmcli d

  nmtui

  service network restart

  ip a

  #Fija IP Red Host-Only
  #192.168.56.17
  #Solo dejar la Lineas  

```bash
  cd /etc/sysconfig/network-scripts
  cp ifcfg-eth0 ifcfg-eth0.old
  vi ifcfg-eth0
```


  TYPE=Ethernet
  BOOTPROTO=none
  NAME=eth0
  DEVICE=eth0
  ONBOOT=yes
  IPADDR=192.168.56.17
  PREFIX=24
    
  #Reinicia
  service network restart

  ip addr

  shutdown

=================
==CenSer17.BP01==
================= 

#opcional
----------------------
--Configue.Proxy.Ofi--
----------------------

----------------
--Actualiza SO--
----------------
  #Se Actualizan los paquetes
  yum update
  yum upgrade

------------
--Firewall--
------------
systemctl is-enabled firewalld
systemctl is-active firewalld
systemctl disable firewalld
systemctl stop firewalld

------------------
--Habilitar Ipv4--
------------------
#I added the following to 
vi /etc/sysctl.conf
net.ipv4.ip_forward=1

#setting 
vi /etc/ssh/sshd_config
#Descomentar
UseDNS  no

=================
==CenSer17.BP02==
=================
