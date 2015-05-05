======================================================
Cinder volume driver for Infortrend EonStor DS storage
======================================================

Include the URL of your launchpad blueprint:

https://blueprints.launchpad.net/cinder/+spec/infortrend-iscsi-fc-volume-driver

Add Cinder volume driver for Infortrend EonStor DS storage products. 
The driver will implement all APIs required to support both FC and iSCSI protocols.
It manages Infortrend EonStor DS storage by Infortrend CLI tool.

Problem description
===================

Currently no volume driver for Infortrend EonStor DS storage available in any release branch.

Use Cases
=========

Proposed change
===============

The new driver will add support for Infortrend DS storage products as backend storage in Cinder. 
The driver supports the following APIs:  

* Volume Create/Delete  

* Volume Attach/Detach  

* Snapshot Create/Delete  

* Create Volume from Snapshot  

* Get Volume Stats  

* Copy Image to Volume  

* Copy Volume to Image  

* Clone Volume  

* Extend Volume  


Driver will be implemented using three classes in separate files.

* class InfortrendCommon
   Main class common to FC and ISCSI driver classes.

* class InfortrendCLIISCSIDriver
   Driver specific for ISCSI protocol.

* class InfortrendCLIFCDriver
   Driver specific for FC protocol.

Alternatives
------------

None

Data model impact
-----------------

None

REST API impact
-----------------

None

Security impact
-----------------

None

Notifications impact
--------------------

None

Other end user impact
---------------------

User will be able to use Infortrend EonStor DS storage with Cinder.

Performance Impact
------------------

None

Other deployer impact
---------------------

The driver can be configured with the following parameters in cinder.conf:
* volume_driver - choose iscsi or fc driver  

* volume_backend_name - indicate this backend's property  

* san_ip - IP to CLI management interface on Infortrend  

* san_password - RAID password for better security concern  

* infortrend_pools_name - multiple pools support  

* infortrend_slots_a_channels_id - channel number used for openstack in slot A controller  

* infortrend_slots_b_channels_id - channel number used for openstack in slot B controller  

* infortrend_tiering - indicate the number of tiering  

* infortrend_iscsi_mcs - enable iscsi mcs flag  

* infortrend_fc_multipath - enable fc multipath flag  


Developer impact
----------------

None

Implementation
==============

Assignee(s)
-----------

Primary assignee:  

James Tsai

Other contributors:  

Jessy Lee  

RyanC 

Work Items
----------
Common driver:  

   common_cli.py  

   cli_factory.py  

   Driver code common to FC and ISCSI.  

   Done  

iSCSI driver:  

   infortrend_iscsi_cli.py  

   Driver code specific to ISCSI.  

   In progress.  Code complete, but Driver cert in progress.  

FC driver:  

   infortrend_fc_cli.py  

   Driver code specific to FC.  

   In progress.  Code complete, but Driver cert in progress.  

Unit test:  

   test_infortrend_common.py  

   test_infortrend_cli.py  

   Done  

CI environment will be setup, one for each driver type.

Dependencies
============

None

Testing
=======

Test using existing test infrastructure according to openstack cinder driver submission steps.

Documentation Impact
====================

Support Matrix needs to be updated to include Infortrend support.
https://wiki.openstack.org/wiki/CinderSupportMatrix

Block storage documentation needs to be updated to include Infortrend volume driver
information in the volume drivers section.
http://docs.openstack.org/

References
==========

None


