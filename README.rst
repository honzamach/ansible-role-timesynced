.. _section-role-timesynced:

Role **timesynced**
================================================================================

Ansible role for enabling time synchronization via NTP service.

* `Ansible Galaxy page <https://galaxy.ansible.com/honzamach/timesynced>`__
* `GitHub repository <https://github.com/honzamach/ansible-role-timesynced>`__
* `Travis CI page <https://travis-ci.org/honzamach/ansible-role-timesynced>`__


Description
--------------------------------------------------------------------------------


Main purpose of this role is to provide time synchronization feature. It takes
care of following tasks:

* Installation of all necessary system packages.
* Management of the NTP service configuration file.
* Turning the service on/off and enabling/disabling service after startup.


Requirements
--------------------------------------------------------------------------------

This role does not have any special requirements.


Dependencies
--------------------------------------------------------------------------------

This role is not dependent on any other role.

No other roles have direct dependency on this role.


Managed files
--------------------------------------------------------------------------------

This role directly manages content of following files:

* ``/etc/ntp.conf``


Internal variables
--------------------------------------------------------------------------------


.. envvar:: hm_timesynced__package_list

	List of role-related packages, that will be installed on target system.

	* *Datatype:* ``list of strings``
    * *Default value:* ``["ntp"]``

.. envvar:: hm_timesynced__ntp_enabled

    Turn NTP time synchronization on/off and also enable/disable NTP daemon at startup.

    * *Datatype:* ``boolean``
    * *Default value:* ``true``

.. envvar:: hm_timesynced__ntp_servers

    List of default NTP servers. The list should contain objects with *name* and
    *address* attributes.

    * *Datatype:* ``list of dictionaries``
    * *Default value:* (please see YAML file ``defaults/main.yml``)


Usage and customization
--------------------------------------------------------------------------------

This role is (attempted to be) written according to the `Ansible best practices <https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html>`__. The default implementation should fit most users,
however you may customize it by tweaking default variables and providing custom
templates.


Variable customizations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most of the usefull variables are defined in ``defaults/main.yml`` file, so they
can be easily overridden almost from `anywhere <https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable>`__.


Template customizations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This roles uses *with_first_found* mechanism for all of its templates. If you do
not like anything about built-in template files you may provide your own custom
templates. For now please see the role tasks for list of all checked paths for
each of the template files.


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


Example Playbook
--------------------------------------------------------------------------------

Example content of inventory file ``inventory``::

    [servers-timesynced]
    localhost

Example content of role playbook file ``playbook.yml``::

    - hosts: servers-timesynced
      remote_user: root
      roles:
        - role: honzamach.timesynced
      tags:
        - role-timesynced

Example usage::

    ansible-playbook -i inventory playbook.yml


License
--------------------------------------------------------------------------------

MIT


Author Information
--------------------------------------------------------------------------------

Honza Mach <honza.mach.ml@gmail.com>
