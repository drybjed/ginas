## debops.mysql

[![Platforms](http://img.shields.io/badge/platforms-debian%20|%20ubuntu-lightgrey.svg)](#)

Install and manage a MySQL database. At the moment only database on
`localhost` is supported.

You can use this role as a dependency of another role to easily create
databases and users for a particular application (database and user
management is also available using Ansible inventory).

### Installation

To install `debops.mysql` using Ansible Galaxy, run:

    ansible-galaxy install debops.mysql

### Role dependencies

- `debops.secret`
- `debops.ferm`
- `debops.tcpwrappers`



### Role variables

List of default variables available in the inventory:

    ---
    
    # Length of randomly generated passwords (it's a string)
    mysql_password_length: '20'
    
    # Password for MySQL root user
    mysql_root_password: "{{ lookup('password', secret + '/credentials/' + ansible_fqdn + '/mysql/root/password length=' + mysql_password_length) }}"
    
    # Enable PHPMyAdmin? It will be installed on localhost with php5-fpm and nginx
    # See 'phpmyadmin' role for more configuration options
    mysql_phpmyadmin: False
    
    mysql_backup_mailaddr: 'backup'
    mysql_backup_doweekly: 6
    mysql_backup_latest: 'no'
    
    mysql_mysqld_bind_address: 'localhost'
    mysql_mysqld_port: 3306
    mysql_mysqld_max_connections: 100
    
    # List of MySQL databases to manage
    mysql_databases: []
      #- name: 'database_name'
      #  state: 'present,absent'        # optional
    
    # List of MySQL users to manage (defaults first)
    mysql_users: []
      #- name: 'user_name'              # required
      #  host: 'localhost'
      #  state: 'present,absent'
      #  password: ''                   # if not specified, random will be generated
      #                                 # and saved in the 'secret' storage
      #  priv: 'user_name.*:ALL'
      #  append_privs: 'no,yes'
    
    # Use this variable to set additional mysqld options
    #mysql_mysqld_options:
    #  key_buffer: '16M'
    #  skip-name-resolve:
    
    # This is a list of IP addresses or CIDR networks allowed to connect to MySQL
    # server from remote hosts. It will be applied in firewall (ferm) and
    # /etc/hosts.allow (tcpwrappers).
    # You will need to set mysql_mysqld_bind_address to 0.0.0.0 and restart MySQL
    # server for it to listen on all network interfaces.
    mysql_mysqld_allow: []





### Authors and license

`debops.mysql` role was written by:

- Maciej Delmanowski - [e-mail](mailto:drybjed@gmail.com) | [Twitter](https://twitter.com/drybjed) | [GitHub](https://github.com/drybjed)


License: [GNU General Public License v3](https://tldrlegal.com/license/gnu-general-public-license-v3-(gpl-3))


***

This role is part of the [DebOps](http://debops.org/) project. README generated by [ansigenome](https://github.com/nickjj/ansigenome/).

