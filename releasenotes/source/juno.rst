=========================
Juno Series Release Notes
=========================

Release Overview
================

The Juno release cycle brings a significant update to the user experience;
numerous stability improvements; support for Sahara; and significant
enhancements in feature support for networking, volumes, databases and images.
The community continues to grow and gain speed. Read on for more details.

Highlights
==========

New Features
------------

Sahara
~~~~~~

The OpenStack Data Processing project (Sahara) was formally included into the
integrated release in Juno and Horizon includes broad support for managing your
data processing. You can specify and build clusters to utilize several data
types with user specified jobs while tracking the progress of those jobs.

Neutron
~~~~~~~

Neutron added several new features in Juno, including:

* DVR (Distributed Virtual Routing)
* L3 HA support
* IPv6 subnet modes

Horizon provides support for these new features with the Juno release. These
features provide much greater flexibility in specifying software defined
networks.

An existing feature in Neutron that Horizon now supports is the MAC learning
extension.

Glance
~~~~~~

In Juno, Glance introduced the ability to manage a catalog of metadata
definitions where users can register the metadata definitions to be used on
various resource types including images, volumes, aggregates, and flavors.
Support for viewing and editing the assignment of these metadata tags is
included in Horizon.

Cinder
~~~~~~

In a continued effort to provide more complete API support, several
additional features of the Cinder API are now supported in Horizon in the
Juno release.

Some of these features include:
* Creating and restoring volume backups
* Enabling resetting the state of a snapshot
* Enabling resetting the state of a volume
* Supporting upload-to-image
* Volume retype
* QoS (quality of service) support.

Trove
~~~~~

Trove supports using multiple types of datastores, e.g., mysql, redis, mongodb.
Users can now select from the list of datastores supported by the cloud operator
when creating their database instances.

Another addition is support for utilizing and restoring from incremental
database backups.

To improve support for Neutron based clouds, when creating a database instance,
the user can now specify the NIC for the database instance on creation allowing
direct access to the instance by the user.

Nova
~~~~

The new Nova instance actions view provides a list of all actions taken on
all instances in the current project allowing users to view resulting errors or
actions taken by other users on those instances.

Administrators now have the ability to evacuate hosts off hypervisors which can
aid in system maintenance by providing a mechanism to migrate all instances to
other hosts.

Improved Plugin Support
~~~~~~~~~~~~~~~~~~~~~~~

The plugin system in Horizon continued to improve in the Juno release.
Some of those improvements:

* Support for adding plugin specific AngularJS modules
* Support for adding static files, e.g., CSS, JS, images
* Ability to add exceptions
* Fixing ordering issues
* Numerous other bug fixes

Enhanced RBAC support
~~~~~~~~~~~~~~~~~~~~~

In an ongoing effort to support richer role based access control (RBAC) in
Horizon, the views for several more services were enhanced with RBAC checks to
determine user access to actions.  The newly supported services are compute,
network and orchestration. These changes allow operators to implement finer
grained access control than just "member" and "admin".

The identity panels (domains, projects, users, roles, groups) have also been
converted to support RBAC at the view level. The identity panels have been
moved from the admin dashboard into their own 'Identity' dashboard and
accessibility is determined by policies alone. This is the first step toward
consolidating the near duplicate content of the project and admin dashboards
into single views supporting a wide range of roles.

UX Changes
~~~~~~~~~~

In Juno, Horizon transitioned to utilizing Bootstrap v3. Horizon had been
pinned to an older version of Bootstrap for several releases. This change now
allows Horizon to pick up numerous bug fixes and overall improvements in the
Bootstrap framework. The look and feel remains mainly consistent with the
Icehouse release.

Under the Hood
--------------

Improved Translatability
~~~~~~~~~~~~~~~~~~~~~~~~

In an effort to improve the translations for Horizon, updates to remove
concatenations and better handle tense were made.

JavaScript Libraries Extracted
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As part of the Horizon team's ongoing efforts to split the repository into more
logical pieces, all the 3rd party JavaScript libraries that Horizon depends on
have been removed from the Horizon code base and python xstatic packages have
been utilized instead. The xstatic format allows for easy consumption by the
Django framework Horizon is built on. Now JavaScript libraries are utilized
like any other python dependency in Horizon.

Conversion from LESS to SCSS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The supported stylesheets in Horizon have been converted to utilize SCSS rather
than LESS. The change was necessary due to a prevalent lack of support for LESS
compilers in python. This change also allowed us to upgrade to Bootstrap 3, as
parts of the Bootstrap 3 LESS stylesheets were not supported by existing python
based LESS compilers.

Known Issues and Limitations
============================

Rendering issues in extensions
------------------------------
The conversion to utilizing Bootstrap v3 can cause content extensions written
on top of Horizon to have rendering issues. Most of these are fixed by a simple
CSS class name substitutions. These issues are primarily seen with buttons and
panel content widths.

Online Compression
------------------
With the move to SCSS, there may be issues with utilizing online compression in
non-DEBUG mode in Horizon. Offline compression continues to work as in previous
releases.

https://bugs.launchpad.net/horizon/+bug/1379761

Neutron L3 HA
-------------
The HA property is updateable in the UI, however, Neutron API does not allow the
update operation because toggling HA support does not work.

https://bugs.launchpad.net/horizon/+bug/1379761
