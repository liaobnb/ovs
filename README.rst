.. NOTE(stephenfin): If making changes to this file, ensure that the line
   numbers found in 'Documentation/intro/what-is-ovs' are kept up-to-date.

============
Open vSwitch
============

.. image:: https://travis-ci.org/openvswitch/ovs.png
    :target: https://travis-ci.org/openvswitch/ovs
.. image:: https://ci.appveyor.com/api/projects/status/github/openvswitch/ovs?branch=master&svg=true&retina=true
    :target: https://ci.appveyor.com/project/blp/ovs/history


什么是OVS
---------------------
OVS 是一个开源的多层软件交换机。目的是部署一个高质量的可创造性的交换机平台，能够支持标准的接口管理和开放的转发函数，以实现可编程的扩展和控制。

OVS 在作为虚拟机环境下的虚拟交换机是一款非常合适的功能。除了对虚拟网络层，暴露标准的控制和接口，它被设计支持多个分布式的物理服务器的连接。OVS在多款基于linux的虚拟化技术兼容，包含：Xen/XenServer，KVM，和VirtualBox

OVS的大部分代码，由平台独立的C写出，容易移植到到其他的环境。当前版本的OVS支持下列的功能：

.. Open vSwitch is a multilayer software switch licensed under the open source
 Apache 2 license.  Our goal is to implement a production quality switch
 platform that supports standard management interfaces and opens the forwarding
 functions to programmatic extension and control.
 Open vSwitch is well suited to function as a virtual switch in VM environments.
 In addition to exposing standard control and visibility interfaces to the
 virtual networking layer, it was designed to support distribution across
 multiple physical servers.  Open vSwitch supports multiple Linux-based
 virtualization technologies including Xen/XenServer, KVM, and VirtualBox.
 The bulk of the code is written in platform-independent C and is easily ported
 to other environments.  The current release of Open vSwitch supports the
 following features:

- Standard 802.1Q VLAN model with trunk and access ports [`trunk与access <study/802.1Q-VLAN.md>`__.]
- NIC bonding with or without LACP on upstream switch  [`LACP <study/LACP.md>`__.]
- NetFlow, sFlow(R), and mirroring for increased visibility 
- QoS (Quality of Service) configuration, plus policing
- Geneve, GRE, VXLAN, STT, and LISP tunneling
- 802.1ag connectivity fault management
- OpenFlow 1.0 plus numerous extensions
- Transactional configuration database with C and Python bindings
- High-performance forwarding using a Linux kernel module

..The included Linux kernel module supports Linux 3.10 and up.
包含 linux 内核 模块 支持， linux 3.10 及以上的版本

ovs 能够 完全运行在 用户空间，不需要 内核 支持。 用户空间的 部署 更容易 port 。 在用户空间的ovs 能够 允许
Linux 内核 和 DPDK 设备。 注意： 有 datapath 的非DPDK的设备，被认为 在 性能上 开销 更大。

..Open vSwitch can also operate entirely in userspace without assistance from
 a kernel module.  This userspace implementation should be easier to port than
 the kernel-based switch. OVS in userspace can access Linux or DPDK devices.
 Note Open vSwitch with userspace datapath and non DPDK devices is considered
 experimental and comes with a cost in performance.

What's here?
------------

..The main components of this distribution are:
ovs的主要组成部分：

- ovs-vswitchd, a daemon that implements the switch, along with a companion
  Linux kernel module for flow-based switching.
- ovsdb-server, a lightweight database server that ovs-vswitchd queries to
  obtain its configuration.
- ovs-dpctl, a tool for configuring the switch kernel module.
- Scripts and specs for building RPMs for Citrix XenServer and Red Hat
  Enterprise Linux.  The XenServer RPMs allow Open vSwitch to be installed on a
  Citrix XenServer host as a drop-in replacement for its switch, with
  additional functionality.
- ovs-vsctl, a utility for querying and updating the configuration of
  ovs-vswitchd.
- ovs-appctl, a utility that sends commands to running Open vSwitch daemons.

..Open vSwitch also provides some tools:

ovs 提供的工具 如下：

- ovs-ofctl, a utility for querying and controlling OpenFlow switches and
  controllers.
- ovs-pki, a utility for creating and managing the public-key infrastructure
  for OpenFlow switches.
- ovs-testcontroller, a simple OpenFlow controller that may be useful for
  testing (though not for production).
- A patch to tcpdump that enables it to parse OpenFlow messages.

What other documentation is available?
--------------------------------------

.. TODO(stephenfin): Update with a link to the hosting site of the docs, once
   we know where that is

To install Open vSwitch on a regular Linux or FreeBSD host, please read the
`installation guide <Documentation/intro/install/general.rst>`__. For specifics
around installation on a specific platform, refer to one of the `other
installation guides <Documentation/intro/install/index.rst>`__

For answers to common questions, refer to the `FAQ <Documentation/faq>`__.

To learn about some advanced features of the Open vSwitch software switch, read
the `tutorial <Documentation/tutorials/ovs-advanced.rst>`__.

Each Open vSwitch userspace program is accompanied by a manpage.  Many of the
manpages are customized to your configuration as part of the build process, so
we recommend building Open vSwitch before reading the manpages.

License
-------

The following is a summary of the licensing of files in this distribution.
As mentioned, Open vSwitch is licensed under the open source Apache 2 license.
Some files may be marked specifically with a different license, in which case
that license applies to the file in question.


Files under the datapath directory are licensed under the GNU General Public
License, version 2.

File build-aux/cccl is licensed under the GNU General Public License, version 2.

The following files are licensed under the 2-clause BSD license.
    include/windows/getopt.h
    lib/getopt_long.c
    lib/conntrack-tcp.c

The following files are licensed under the 3-clause BSD-license
    include/windows/netinet/icmp6.h
    include/windows/netinet/ip6.h
    lib/strsep.c

Files under the xenserver directory are licensed on a file-by-file basis.
Refer to each file for details.

Files lib/sflow*.[ch] are licensed under the terms of either the
Sun Industry Standards Source License 1.1, that is available at:
        http://host-sflow.sourceforge.net/sissl.html
or the InMon sFlow License, that is available at:
        http://www.inmon.com/technology/sflowlicense.txt

Contact
-------

bugs@openvswitch.org
