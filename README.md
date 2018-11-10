Ansible Role: Percona Server
=========

[![Build Status](https://travis-ci.org/CarlosLongarela/ansible-role-percona.svg?branch=master)](https://travis-ci.org/CarlosLongarela/ansible-role-percona)
[![Percentage of issues still open](http://isitmaintained.com/badge/open/CarlosLongarela/ansible-role-percona.svg)](http://isitmaintained.com/project/CarlosLongarela/ansible-role-percona "Percentage of issues still open")
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/CarlosLongarela/ansible-role-percona.svg)](http://isitmaintained.com/project/CarlosLongarela/ansible-role-percona "Average time to resolve an issue")

Install Percona Server, basic security options and utils for database tuning and backups with cron tasks.

Requirements
------------

None.

Changes
------------

Deleted PhpMyAdmin installation, now PhpMyAdmin has it's own role in Galaxy: [CarlosLongarela.phpmyadmin](https://galaxy.ansible.com/CarlosLongarela/phpmyadmin/)

Role Variables
--------------

    percona_version: 5.7

    percona_service_name: mysql
    percona_secure_installation: True

    percona_root_password: changeme

    percona_server_path_utiles: /root/utiles

    percona_path_backups: /home/db_backups/

    percona_databases: []
    # delete [] and define databases
    # - database1
    # - database2

    percona_users: []
    # delete [] and define databases
    # user1:
    #    name: "usuario1"
    #    password: "clave1"
    #    priv: "*.*:ALL"
    # user2:
    #    name: "usuario2"
    #    password: "clave2"
    #    priv: "db.table:priv1,priv2"
    # user3:
    #    name: "usuario3"
    #    password: "clave3"
    #    priv: "bdpruebas.*:ALL"

    percona_options:
      bind_address: '127.0.0.1'
      performance_schema: on
      skip_name_resolve: 1
      max_connections: 100
      connect_timeout: 2
      max_allowed_packet: 10M
      innodb_buffer_pool_instances: 1
      innodb_buffer_pool_size: 100M
      innodb_log_file_size: 25M
      table_open_cache: 500
      tmp_table_size: 50M
      max_heap_table_size: 50M
      query_cache_limit: 256K
      query_cache_type: 0
      query_cache_size: 0
      query_cache_min_res_unit: 2k
      join_buffer_size: 2M
      sort_buffer_size: 256K
      read_buffer_size: 128K
      read_rnd_buffer_size: 4M
      key_buffer_size: 500M
      slow_query_log: true
      long_query_time: 5
      log_slow_admin_statements: true
      log_queries_not_using_indexes: true

      percona_utiles_bd: false
      percona_cron_backup: false
      percona_cron_optimizacion: false

    percona_cron_backup_db:
      minute: "15"
      hour: "3"
      day: "*"
      weekday: "*"

    percona_cron_optimiza_db:
      minute: "1"
      hour: "3"
      day: "*"
      weekday: "0"

    aptget_update_cache_valid_time: 3600


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers

      gather_facts: no
      become: true

      vars:
        percona_root_password: cambiame

        percona_databases:
          - mydatabase

        percona_users:
          user1:
            name: "usuario1"
            password: "clave1"
            priv: "mydatabase.*:ALL"

        percona_utiles_bd: true
        percona_cron_backup: true
        percona_cron_optimizacion: true

       roles:
         - { role: CarlosLongarela.percona }

License
-------

GPLv2

Author Information
------------------

This role was created in 2018, November by [Carlos Longarela](mailto:carlos@longarela.eu), from [Taberna WordPress](https://tabernawp.com/).
