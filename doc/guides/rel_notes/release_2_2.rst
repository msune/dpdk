DPDK Release 2.2
================

New Features
------------

* **ethdev: define a set of advertised link speeds.**

  Allowing to define a set of advertised speeds for auto-negociation,
  explicitely disable link auto-negociation (single speed) and full
  auto-negociation.

* **ethdev: add speed_cap bitmap to recover eth device link speed capabilities
  define a set of advertised link speeds.**

  ``struct rte_eth_dev_info`` has now speed_cap bitmap, which allows the
  application to recover the supported speeds for that ethernet device.

Resolved Issues
---------------

EAL
~~~

* **eal/linux: Fixed epoll timeout.**

  Fixed issue where the ``rte_epoll_wait()`` function didn't return when the
  underlying call to ``epoll_wait()`` timed out.


Drivers
~~~~~~~

* **ixgbe: Fixed issue with X550 DCB.**

  Fixed a DCB issue with x550 where for 8 TCs (Traffic Classes), if a packet
  with user priority 6 or 7 was injected to the NIC, then the NIC would only
  put 3 packets into the queue. There was also a similar issue for 4 TCs.

* **ixgbe: Removed burst size restriction of vector RX.**

  Fixed issue where a burst size less than 32 didn't receive anything.

* **i40e: Fixed base driver allocation when not using first numa node.**

  Fixed i40e issue that occurred when a DPDK application didn't initialize
  ports if memory wasn't available on socket 0.

* **vhost: Fixed Qemu shutdown.**

  Fixed issue with libvirt ``virsh destroy`` not killing the VM.


Libraries
~~~~~~~~~

* **hash: Fixed memory allocation of Cuckoo Hash key table.**

  Fixed issue where an incorrect Cuckoo Hash key table size could be
  calculated limiting the size to 4GB.

* **ethdev: Fixed link_speed overflow in rte_eth_link for 100Gbps.**

  100Gbps in Mbps (100000) exceeds 16 bit max value of ``link_speed`` in
  ``rte_eth_link``.


Examples
~~~~~~~~


Other
~~~~~


Known Issues
------------


API Changes
-----------

* The deprecated flow director API is removed.
  It was replaced by rte_eth_dev_filter_ctrl().

* The function rte_eal_pci_close_one() is removed.
  It was replaced by rte_eal_pci_detach().

* The deprecated ACL API ipv4vlan is removed.

* The deprecated hash function rte_jhash2() is removed.
  It was replaced by rte_jhash_32b().

* The deprecated KNI functions are removed:
  rte_kni_create(), rte_kni_get_port_id() and rte_kni_info_get().

* The deprecated ring PMD functions are removed:
  rte_eth_ring_pair_create() and rte_eth_ring_pair_attach().

* New API call, rte_eth_speed_to_bm_flag(), in ethdev to map numerical speeds
  to bitmap fields.

ABI Changes
-----------

* The EAL and ethdev structures rte_intr_handle and rte_eth_conf were changed
  to support Rx interrupt. It was already done in 2.1 for CONFIG_RTE_NEXT_ABI.

* The ethdev flow director entries for SCTP were changed.
  It was already done in 2.1 for CONFIG_RTE_NEXT_ABI.

* The ethdev rte_eth_link and rte_eth_conf structures were changed to
  support the new link API, as well as ETH_LINK_HALF/FULL_DUPLEX.

* The ethdev rte_eth_dev_info was changed to support device speed capabilities.

* The mbuf structure was changed to support unified packet type.
  It was already done in 2.1 for CONFIG_RTE_NEXT_ABI.

* The dummy malloc library is removed. The content was moved into EAL in 2.1.

* The LPM structure is changed. The deprecated field mem_location is removed.


Shared Library Versions
-----------------------

The libraries prepended with a plus sign were incremented in this version.

.. code-block:: diff

   + libethdev.so.2
   + librte_acl.so.2
     librte_cfgfile.so.1
     librte_cmdline.so.1
     librte_distributor.so.1
   + librte_eal.so.2
   + librte_hash.so.2
     librte_ip_frag.so.1
     librte_ivshmem.so.1
     librte_jobstats.so.1
   + librte_kni.so.2
     librte_kvargs.so.1
   + librte_lpm.so.2
   + librte_mbuf.so.2
     librte_mempool.so.1
     librte_meter.so.1
     librte_pipeline.so.1
     librte_pmd_bond.so.1
   + librte_pmd_ring.so.2
     librte_port.so.1
     librte_power.so.1
     librte_reorder.so.1
     librte_ring.so.1
     librte_sched.so.1
     librte_table.so.1
     librte_timer.so.1
     librte_vhost.so.1
