.. _shared_accounts:

<<<<<<< HEAD
Repo and Shared Accounts Permissions
====================================

Modify SSD Team Github Permissions:

* https://github.com/orgs/jules-lsm/teams/system-managers
* ​https://github.com/orgs/MetOffice/teams/ssdteam

The ssd team should propagate to all relevant repos, but also check the
permissions for all of,

* UM
* LFRic Apps
* LFRic Core
=======
Trunk and Shared Accounts Permissions
=====================================

.. warning::

    Incorrectly editing the svnperms.conf file can break all access to a repo

To update fcm repositories trunk access list (using UM as an example),

* First checkout the top level of the repo,

  .. code-block::

    fcm co --depth=files https://code.metoffice.gov.uk/svn/um

* Move into the working copy and make the required changes in the ``svnperms.conf`` file.
* Commit the change.

The above process needs doing for all of,

* UM
* LFRic Apps
>>>>>>> upstream/main
* Jules
* UKCA
* Casim
* Shumlib
* MOCI
<<<<<<< HEAD
* Socrates
* Mule
* um_meta
* um_aux
* um_doc
* git_playground (likely renamed)
=======

Modify SSD Team Github Permissions:

* https://github.com/orgs/jules-lsm/teams/system-managers
* ​https://github.com/orgs/MetOffice/teams/ssdteam
>>>>>>> upstream/main

Review account permissions in Active Directory for the following Shared Users:

* umadmin
* umtest
* julesadmin
* lfricadmin
* spackadmin
