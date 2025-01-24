## README для роли postgres

### postgres Role

An Ansible role for installing and configuring postgresql on a Linux server, creating databases and users, and managing
access controls.

### Requirements

• Ansible 2.9+ is required.

• Target system must be Ubuntu or Debian.

### Role Variables

| Variable                        | Default Value                                                                               |
|---------------------------------|---------------------------------------------------------------------------------------------|
| postgres_version                | 15                                                                                          |
| postgres_support_packages       | - gnupg   - python3-psycopg2                                                                |
| postgres_packages               | - "postgresql-{{ postgres_version }}" - "postgresql-contrib-{{ postgres_version }}"         |
| postgres_repo_key               | https://www.postgresql.org/media/keys/ACCC4CF8.asc                                          |
| postgres_repo                   | "deb http://apt.postgresql.org/pub/repos/apt/ {{ ansible_distribution_release }}-pgdg main" |
| postgres_repo_filename          | pgdg                                                                                        |
| postgres_password               | pw                                                                                          |
| postgres_data_dir               | "/var/lib/postgresql/{{ postgres_version }}"                                                |
| postgres_config_dir             | "/etc/postgresql/{{ postgres_version }}/main"                                               |
| postgres_new_data_dir           | /tmp/postgresql                                                                             |
| postgres_users_hba_method       | md5                                                                                         |
| postgres_replication_hba_method | md5                                                                                         |
| postgres_users                  | name: jusmad  password: jusmad encrypted: true role_attr_flags: SUPERUSER port: 5432        |
| postgres_databases              | name: just_mad_db   port: 5432  roles: jusmad  privs: ALL                                   |
| postgres_master_address         | 192.168.56.201                                                                              |
| postgres_replica_address:       | 192.168.56.202                                                                              |


### Templates

This role includes templates:

- pg_hba.conf.j2 - Client authentication configuration file.

### Dependencies

This role has no dependencies on other roles.
