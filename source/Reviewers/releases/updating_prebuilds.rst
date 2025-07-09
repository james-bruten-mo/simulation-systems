.. _updating_prebuilds:

Mid-Release Prebuilds
=====================

These are instructions for updating UM prebuilds mid-way through a release cycle. Reasons for doing this include new builds being added, changes that mean the old prebuilds break (sometimes new/deleted files can do this), or because the prebuilds are so out of date they don't particularly help. An example ticket doing this can be seen in `UM:#7903 <https://code.metoffice.gov.uk/trac/um/ticket/7903>`_.

To update prebuilds:

* Open a new UM ticket, create a branch and check it out.
* In ``rose-stem/rose-suite.conf``:

  * Update the ``BASE_UM_REV`` variable to the latest version of the UM trunk.
  * Update any other ``BASE_*_REV`` variables if those trunks have more recent commits that the revision listed.

* In ``rose-stem/site/meto/variables.cylc``:

  * Update the prebuilds paths with the name, ``rXXXXXX_prebuilds`` where ``XXXXXX`` should match the ``BASE_UM_REV`` variable from earlier.

* Commit these changes to the branch.
* Login as ``umadmin`` and check out the branch (this will need to be from the mirror, so ensure it has updated).
* Install the prebuilds. First do the remote HPC's and after each, clean the suite manually on azure spice. Then do azure spice and the final HPC. Ensure the name of the suite matches the path that was set in the ``variables.cylc`` file.

.. code-block::

    ssh cazcron1 # Or cazcron2 if desired

    # First on EXCD
    rose stem --group=ex1a_fcm_make,ex1a_fcm_make_portio2b -n rXXXXXX_prebuilds --no-run-name -S MAKE_PREBUILDS=true -S USE_EXCD=true
    cylc play rXXXXXX_prebuilds


    # For each $HOME, $DATADIR and $SCRATCH only on Azspice:
    cd $HOME/cylc-run
    rm -rf vnX.Y_prebuilds

    # Next, on the EXZ
    rose stem --group=ex1a_fcm_make,ex1a_fcm_make_portio2b -n rXXXXXX_prebuilds --no-run-name -S MAKE_PREBUILDS=true -S USE_EXZ=true
    cylc play rXXXXXX_prebuilds


    # For each $HOME, $DATADIR and $SCRATCH only on Azspice:
    cd $HOME/cylc-run
    rm -rf vnX.Y_prebuilds

    # Finally on Spice and EXAB
    rose stem --group=prebuilds -n rXXXXXX_prebuilds --no-run-name -S MAKE_PREBUILDS=true -S USE_EXAB=true
    cylc play rXXXXXX_prebuilds



* Finally, ensure that prebuilds are enabled in ``rose-stem/rose-suite.conf`` and have the ticket reviewed and committed.
