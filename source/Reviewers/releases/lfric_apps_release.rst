.. _lfric_apps_release:

LFRic Apps Release
==================

LFRic Inputs KGO Install
------------------------

<<<<<<< HEAD
* This can be done at any point once all tickets that change lfricinputs kgo
  have been committed.
* It's easiest to use the umtest nightly testing for this and will save having
  to run the suite twice.
* Alternatively, run ``cylc vip -z g=lfricinputs -S HOUSEKEEPING=false -n lfricinputs_kgo ./rose-stem``
  and wait for this to finish - all jobs should pass.
* Install the kgo by running
  ``$UMDIR/SimSys_Scripts/kgo_updates/meto_update_kgo.sh --new-release``
=======
* This can be done at any point once all tickets that change lfricinputs kgo have been committed.
* It's easiest to use the umtest nightly testing for this and will save having to run the suite twice.
* Alternatively, run ``rose stem --group=lfricinputs -S HOUSEKEEPING=false`` and wait for this to finish - all jobs should pass.
* Install the kgo by running ``$UMDIR/SimSys_Scripts/kgo_updates/meto_update_kgo.sh --new-release``
>>>>>>> upstream/main

  * The script will ask for a working copy path - this can be any lfric apps
    working copy as it will not be modified.
  * The version number and ticket number are not required, although an entry
    is required.
  * The kgo install directory must be updated to vnX.Y


LFRic Release
-------------

* Ensure you have a :ref:`fork <forking>` of both the ``lfric_apps`` and
  ``lfric_core`` repositories, and that the ``main`` branches in each are up to
  date with the upstream repository.
* In a clone of these forks, :ref:`create a branch <create_branch>` using the
  ``main`` branch as the parent.

.. important::

    Ensure you create branches from main, otherwise you will not include the
    changes from the past release.

* Move into the lfric apps clone
* Run the release script,
  ``$UMDIR/SimSys_Scripts/lfric_macros/release_lfric.py -o A.B -v X.Y -t
  TTTT -c /path/to/core``

  * ``A.B`` - the previous version
  * ``X.Y`` - the new version
  * ``TTTT`` - the apps release ticket number
  * ``/path/to/core`` - path to the lfric core clone

* Check the output looks sensible. It should:

  * Update the version number
  * Revert any changes to ``rose-stem/site/meto/variables_*.cylc``
  * Copy the ``HEAD`` metadata to ``vnX.Y``
  * Add a blank upgrade macro to all ``versions.py`` files
  * Apply the upgrade macro - rose apps should be updated to the new version
  * Add a ``version_ab_xy.py`` upgrade file - a copy of the versions.py file
  * Reset the ``versions.py`` file with no upgrade macros

* Tag other repositories and update dependencies.sh:

<<<<<<< HEAD
  * Add an ``appsX.Y`` tag to each of the feeder repositories

    * Casim
    * Jules
    * Socrates
    * UKCA

  * In dependencies.yaml:

    * Ensure the ``lfric_core`` ``source`` is pointing at the local clone of
      your branch.
    * Update ``ref`` for above repositories to be ``appsX.Y``
=======
  * :ref:`Tag <reference-tagging>` CASIM, JULES, SOCRATES and UKCA with ``appsX.Y=revision``
  * In dependencies.sh:

    * Make sure ``lfric_core_sources`` is pointing at the core working copy with ``lfric_core_rev`` blank
    * Update ``*_rev`` for all other repositories to be ``appsX.Y`` with ``*_sources`` blank
>>>>>>> upstream/main

* Commit your changes to both Apps and Core branches.

* Run the test suites

<<<<<<< HEAD
  * ``cylc vip -z g=all -n lfric_*X.Y ./rose-stem`` for both Apps and Core.

* Once testing is complete, update LFRic Core in ``dependencies.yaml``

  * ``source`` should be the MetOffice ssh url
  * ``ref`` should be ``coreX.Y``
=======
  * ``rose stem --group=all`` for both Apps and Core.

* Once testing is complete, update LFRic Core in ``dependencies.sh``

  * ``lfric_core_rev`` should be ``coreX.Y``
  * ``lfric_core_sources`` should be blank
>>>>>>> upstream/main

* Open a PR for each and with a reviewer, follow the
  :ref:`review process <github-releases>`
