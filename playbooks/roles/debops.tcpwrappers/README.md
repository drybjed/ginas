## debops.tcpwrappers

[![Platforms](http://img.shields.io/badge/platforms-debian%20|%20ubuntu-lightgrey.svg)](#)

This role can be used to manage [TCP
Wrappers](https://en.wikipedia.org/wiki/TCP\_Wrapper) rules located in
`/etc/hosts.allow` (by default all hosts will be denied access in
`/etc/hosts.deny`, but this can be disabled by a variable).

Other roles can use this role as a dependency to manage access to their own
services (for example, `debops.mysql`, `debops.sshd`).

By default, tcpwrappers will be configured to block access from everywhere
except `localhost` (relative to remote host) and Ansible Controller.

### Installation

To install `debops.tcpwrappers` using Ansible Galaxy, run:

    ansible-galaxy install debops.tcpwrappers




### Role variables

List of default variables available in the inventory:

    ---
    
    # Should Ansible manage tcpwrappers configuration?
    tcpwrappers: True
    
    # Deny access from all hosts/networks by default?
    tcpwrappers_deny_all: True
    
    # Lists of /etc/hosts.allow entries. Example entry below
    tcpwrappers_allow: []
    tcpwrappers_group_allow: []
    tcpwrappers_host_allow: []
    
      #- daemon: 'ALL'            # daemon to configure (sshd, mysqld, etc.)
      #  client: []               # list of host or network addresses.
                                  # If empty, entry will be removed
      #  weight: '10'             # filename prefix, helps with sorting, optional
      #  filename: ''             # custom filename, optional
      #  comment: ''              # comment, optional
    
      #- custom: |                  # custom, free-form text block (filename required)
      #    # Custom entry
      #    # Text block
      #  filename: 'custom_entry'
    
    # Access from localhost
    tcpwrappers_local_allow:
      - daemon: 'ALL'
        client: [ '127.0.0.0/8', '[::1]/128' ]
        comment: 'Access from localhost'
        filename: 'allow_localhost'
        weight: '06'





### Authors and license

`debops.tcpwrappers` role was written by:

- Maciej Delmanowski - [e-mail](mailto:drybjed@gmail.com) | [Twitter](https://twitter.com/drybjed) | [GitHub](https://github.com/drybjed)


License: [GNU General Public License v3](https://tldrlegal.com/license/gnu-general-public-license-v3-(gpl-3))


***

This role is part of the [DebOps](http://debops.org/) project. README generated by [ansigenome](https://github.com/nickjj/ansigenome/).

