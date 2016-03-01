DPDK Release 16.04
==================


**Read this first**

The text below explains how to update the release notes.

Use proper spelling, capitalization and punctuation in all sections.

Variable and config names should be quoted as fixed width text: ``LIKE_THIS``.

Build the docs and view the output file to ensure the changes are correct::

   make doc-guides-html

   firefox build/doc/html/guides/rel_notes/release_16_04.html


New Features
------------

* **ethdev: define a set of advertised link speeds.**

  Added functionality to Allow defining a set of advertised speeds for
  auto-negociation, explicitely disabling link auto-negociation (single speed)
  and full auto-negociation.

* **ethdev: add speed_cap bitmap for link speed capabilities.**

  ``struct rte_eth_dev_info`` has now ``speed_cap`` bitmap, which allows the
  application to recover the supported speeds for that ethernet device.


This section should contain new features added in this release. Sample format:

* **Add a title in the past tense with a full stop.**

  Add a short 1-2 sentence description in the past tense. The description
  should be enough to allow someone scanning the release notes to understand
  the new feature.

  If the feature adds a lot of sub-features you can use a bullet list like this.

  * Added feature foo to do something.
  * Enhanced feature bar to do something else.

  Refer to the previous release notes for examples.

* **Enabled bulk allocation of mbufs.**

  A new function ``rte_pktmbuf_alloc_bulk()`` has been added to allow the user
  to allocate a bulk of mbufs.

* **Virtio 1.0.**

  Enabled virtio 1.0 support for virtio pmd driver.

* **Supported virtio offload in vhost-user.**

  Add the offload and negotiation of checksum and TSO between vhost-user and
  vanilla Linux virtio guest.

* **Added vhost-user live migration support.**


Resolved Issues
---------------

* **ethdev: Fixed link_speed overflow in rte_eth_link for 100Gbps.**

  100Gbps in Mbps (100000) exceeds 16 bit max value of ``link_speed`` in
  ``rte_eth_link``.

This section should contain bug fixes added to the relevant sections. Sample format:

* **code/section Fixed issue in the past tense with a full stop.**

  Add a short 1-2 sentence description of the resolved issue in the past tense.
  The title should contain the code/lib section like a commit message.
  Add the entries in alphabetic order in the relevant sections below.

* **examples/vhost: Fixed frequent mbuf allocation failure.**

  vhost-switch often fails to allocate mbuf when dequeue from vring because it
  wrongly calculates the number of mbufs needed.


EAL
~~~


Drivers
~~~~~~~

* **aesni_mb: Fixed wrong return value when creating a device.**

  cryptodev_aesni_mb_init() was returning the device id of the device created,
  instead of 0 (when success), that rte_eal_vdev_init() expects.
  This made impossible the creation of more than one aesni_mb device
  from command line.


Libraries
~~~~~~~~~

* New API call, ``rte_eth_speed_to_bm_flag`` in ethdev to, map numerical speeds
  to bitmap fields.


Examples
~~~~~~~~


Other
~~~~~


Known Issues
------------

This section should contain new known issues in this release. Sample format:

* **Add title in present tense with full stop.**

  Add a short 1-2 sentence description of the known issue in the present
  tense. Add information on any known workarounds.


API Changes
-----------

This section should contain API changes. Sample format:

* Add a short 1-2 sentence description of the API change. Use fixed width
  quotes for ``rte_function_names`` or ``rte_struct_names``. Use the past tense.


ABI Changes
-----------

* The ethdev ``rte_eth_link`` and ``rte_eth_conf`` structures were changed to
  support the new link API, as well as ``ETH_LINK_HALF``/``FULL_DUPLEX``.

* The ethdev ``rte_eth_dev_info`` was changed to support device speed
  capabilities.


* Add a short 1-2 sentence description of the ABI change that was announced in
  the previous releases and made in this release. Use fixed width quotes for
  ``rte_function_names`` or ``rte_struct_names``. Use the past tense.


Shared Library Versions
-----------------------

Update any library version updated in this release and prepend with a ``+`` sign.

The libraries prepended with a plus sign were incremented in this version.

.. code-block:: diff

     libethdev.so.2
     librte_acl.so.2
     librte_cfgfile.so.2
     librte_cmdline.so.1
     librte_distributor.so.1
     librte_eal.so.2
     librte_hash.so.2
     librte_ip_frag.so.1
     librte_ivshmem.so.1
     librte_jobstats.so.1
     librte_kni.so.2
     librte_kvargs.so.1
     librte_lpm.so.2
     librte_mbuf.so.2
     librte_mempool.so.1
     librte_meter.so.1
     librte_pipeline.so.2
     librte_pmd_bond.so.1
     librte_pmd_ring.so.2
     librte_port.so.2
     librte_power.so.1
     librte_reorder.so.1
     librte_ring.so.1
     librte_sched.so.1
     librte_table.so.2
     librte_timer.so.1
     librte_vhost.so.2
