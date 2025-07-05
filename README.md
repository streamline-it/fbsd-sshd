Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

######################################################################
#
# defaults file for fbsd_sshd
#
######################################################################

# if true, we're configuring sshd for a jail
fbsd_sshd_jail_it: false

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

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - fbsd-sshd

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

