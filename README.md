Role Name
=========

This role will will secure the sshd service. By securing it will do the following:
 - disable password authentication
 - disable root login via sshd

It will also allow you to use the "fbsd_sshd_base_directives" variable to add additional directives to configure the sshd service.

Requirements
------------

None.

Role Variables
--------------
######################################################################
#
# defaults file for fbsd_sshd
#
######################################################################

# if true, we're configuring sshd for a jail
fbsd_sshd_jail_it: false

# name of the jail, used to restart the sshd service for the jail
fbsd_sshd_jail_name: 

# The path to the jail, this will be added to the path of the config file(s)
fbsd_sshd_jail_prepath: ""

# base sshd dirctives go here
fbsd_sshd_base_directives:
  - directive_name:
    directive_value:

# security directives go there
fbsd_sshd_security_directives:
  - directive_name: KbdInteractiveAuthentication
    directive_value: "no"
  - directive_name: PasswordAuthentication
    directive_value: "no"
  - directive_name: PubkeyAuthentication
    directive_value: "yes"
  - directive_name: PermitRootLogin
    directive_value: "no"


# disable directives in the sshd_config file
fbsd_sshd_security_lines_to_disable:
  - directive_line: "KbdInteractiveAuthentication yes"
  - directive_line: "PasswordAuthentication yes"
  - directive_line: "PermitRootLogin yes"

######################################################################
#
# vars file for fbsd-sshd
#
######################################################################

# root group for FreeBSD
fbsd_sshd_root_group: wheel

# SSHD service name
fbsd_sshd_svc: sshd

# custom config directory
fbsd_sshd_config_directory: /etc/ssh/sshd_config.d

# name of the custom base config file
fbsd_sshd_base_filename: 10-base.conf

# name of the custom security-based config file
fbsd_sshd_security_filename: 20-hardening.conf

# main sshd config filepath
fbsd_sshd_main_config_filepath: /etc/ssh/sshd_config

Dependencies
------------

None.

Example Playbook
----------------

Example of non-jailed configuration


- hosts: servers

  vars:

    fbsd_sshd_jail_it: false
 
  roles:
    - name: fbsd-sshd


Example of jailed configuration

- hosts: servers

  vars:

    fbsd_sshd_jail_it: true
    fbsd_sshd_jail_prepath: /jails/apache_jail
    fbsd_sshd_jail_name: apache_jail
 
  roles:
    - name: fbsd-sshd

License
-------

BSD

Author Information
------------------

rich ohara
