.. _section-role-timesynced:

Role **timesynced**
================================================================================

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/timesynced>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-timesynced>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-timesynced>`__

Main purpose of this role is to provide time synchronization feature via NTP service.
It takes care of following tasks:

* Installation of all necessary system packages.
* Management of the NTP service configuration file.
* Turning the service on/off and enabling/disabling service after startup.

**Table of Contents:**

* :ref:`section-role-timesynced-installation`
* :ref:`section-role-timesynced-dependencies`
* :ref:`section-role-timesynced-usage`
* :ref:`section-role-timesynced-variables`
* :ref:`section-role-timesynced-files`
* :ref:`section-role-timesynced-author`

This role is part of the `MSMS <https://github.com/honzamach/msms>`__ package.
Some common features are documented in its :ref:`manual <section-manual>`.


.. _section-role-timesynced-installation:

Installation
--------------------------------------------------------------------------------

To install the role `honzamach.timesynced <https://galaxy.ansible.com/honzamach/timesynced>`__
from `Ansible Galaxy <https://galaxy.ansible.com/>`__ please use variation of
following command::

    ansible-galaxy install honzamach.timesynced

To install the role directly from `GitHub <https://github.com>`__ by cloning the
`ansible-role-timesynced <https://github.com/honzamach/ansible-role-timesynced>`__
repository please use variation of following command::

    git clone https://github.com/honzamach/ansible-role-timesynced.git honzamach.timesynced

Currently the advantage of using direct Git cloning is the ability to easily update
the role when new version comes out.


.. _section-role-timesynced-dependencies:

Dependencies
--------------------------------------------------------------------------------

This role is not dependent on any other role.

No other roles have direct dependency on this role.


.. _section-role-timesynced-usage:

Usage
--------------------------------------------------------------------------------

Example content of inventory file ``inventory``::

    [servers_timesynced]
    your-server

Example content of role playbook file ``role_playbook.yml``::

    - hosts: servers_timesynced
      remote_user: root
      roles:
        - role: honzamach.timesynced
      tags:
        - role-timesynced

Example usage::

    # Run everything:
    ansible-playbook --ask-vault-pass --inventory inventory role_playbook.yml

It is recommended to follow these configuration principles:

* Create/edit file ``inventory/group_vars/all/vars.yml`` and within define some sensible
  defaults for all your managed servers::

        # You are probably using same NTP time servers for all your managed servers.
        hm_timesynced__ntp_servers:
          - { name: "tak6.cesnet.cz", address: "2001:718:1:101::144:238"}
          - { name: "tik.cesnet.cz",  address: "195.113.144.201"}
          - { name: "tak.cesnet.cz",  address: "195.113.144.238"}

* Use files ``inventory/host_vars/[your-server]/vars.yml`` to customize settings
  for particular servers. Please see section :ref:`section-role-timesynced-variables`
  for all available options.


.. _section-role-timesynced-variables:

Configuration variables
--------------------------------------------------------------------------------


Internal role variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. envvar:: hm_timesynced__install_packages

    List of packages defined separately for each linux distribution and package manager,
    that MUST be present on target system. Any package on this list will be installed on
    target host. This role currently recognizes only ``apt`` for ``debian``.

    * *Datatype:* ``dict``
    * *Default:* (please see YAML file ``defaults/main.yml``)
    * *Example:*

    .. code-block:: yaml

        hm_timesynced__install_packages:
          debian:
            apt:
              - ntp
              - ...

.. envvar:: hm_timesynced__ntp_servers

    List of default NTP servers. The list should contain objects with *name* and
    optionally *address* attributes.

    * *Datatype:* ``list of dictionaries``
    * *Default:* (please see YAML file ``defaults/main.yml``)
    * *Example:*

    .. code-block:: yaml

        hm_timesynced__ntp_servers:
          - { name: "server 0.debian.pool.ntp.org" }
          - { name: "tik.cesnet.cz",  address: "195.113.144.201"}


Built-in Ansible variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:envvar:`ansible_lsb['codename']`

    Linux distribution codename. It is used for :ref:`template customizations <section-overview-role-customize-templates>`.


.. _section-role-timesynced-files:

Managed files
--------------------------------------------------------------------------------

.. note::

    This role supports the :ref:`template customization <section-overview-role-customize-templates>` feature.

This role manages content of following files on target system:

* ``/etc/ntp.conf`` *[TEMPLATE]*


.. _section-role-timesynced-author:

Author and license
--------------------------------------------------------------------------------

| *Copyright:* (C) since 2019 Honza Mach <honza.mach.ml@gmail.com>
| *Author:* Honza Mach <honza.mach.ml@gmail.com>
| Use of this role is governed by the MIT license, see LICENSE file.
|
