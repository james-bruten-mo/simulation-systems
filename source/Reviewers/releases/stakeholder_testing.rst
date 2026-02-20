.. -----------------------------------------------------------------------------
    (c) Crown copyright Met Office. All rights reserved.
    The file LICENCE, distributed with this code, contains details of the terms
    under which the code may be used.
   -----------------------------------------------------------------------------

.. _stakeholder_testing:

Stakeholder Testing
===================

This is intended to allow LFRic and UM stakeholders to determine if there are
any undetected problems with the head of the repositories before the release
process begins.

The pre-release testing period should be 72 hours (3 working days). All PRs
affecting the main source code should be committed (to all repos) but limited
scope changes, eg. to just the Met Office site, can still go on.

* Open a UM issue to track partner testing, using the partner testing issue
  template.
* Email the representatives at each UM partner site to them to test. A list of
  emails can be found at, `UM Partner Testing Emails
  <https://github.com/MetOffice/git_playground/wiki/SimSys-Pre%E2%80%90Release-Testing>`__
  (note, that page should remain private to the Met Office).

  * You may need to set the international options in advanced email sending
    options to use Unicode (UTF-8) as the preferred encoding for outgoing
    messages to ensure that all international partners receive the email.
    Change this setting if you receive bounced emails during partner testing.


.. important::

    Now is also a good time to ask for the Jules release notes. This is usually
    done by a member of the Jules community, so email them advising them of the
    likely release date. Ask the team for their details if unsure.
