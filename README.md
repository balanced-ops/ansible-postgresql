# Ansible PostgreSQL playbook

[![Build Status](https://travis-ci.org/balanced-ops/ansible-postgresql.svg)](https://travis-ci.org/balanced-ops/ansible-postgresql)

This is an Ansible playbook for deploying PostgreSQL 9.1, 9.2 or 9.3.

This playbook was tested on Ubuntu 12.04 x86_64.

## Features

* Install PostgreSQL
* Install development headers (optional)
* Install [wal-e](https://github.com/wal-e/wal-e) (optional)
* Install [repmgr](https://github.com/2ndQuadrant/repmgr) (optional)

## Requirements

This playbook requires Ansible 1.6 or higher.

Supported PostgreSQL versions:

* `9.1`
* `9.2`
* `9.3`

## Running playbook

```bash
ansible-playbook -i ansible.host ./tasks/main.yml
```

## Operational maintenance

When using WAL-E the DB will store WAL logs on S3. In our experience these are
quicker to restore from than using repmgr because you do not need to use rsync
to copy the data across. YMMV.

#### Setup a repmgr cluster

TODO

#### Backing up a cluster

Via WAL-E

`ansible-playbook -i ansible.inventory ./ops.yml -e ops_command=wal-e-backup`

Otherwise run the regular pgdump commands.

#### Cloning a master DB

Via WAL-E

`ansible-playbook -i ansible.inventory ./ops.yml -e ops_command=wal-e-clone -e ops_wal_e_path=s3://balanced-wal-e/cluster-name`

Via Repmgr

`ansible-playbook -i ansible.inventory ./ops.yml -e ops_command=repmgr-clone -e ops_repmgr_master=10.3.20.30`

#### Failing over to a new master

`ansible-playbook -i ansible.inventory ./ops.yml -e ops_command=promote`

## See also

You'll probably want to put a [pgbouncer](https://github.com/balanced-ops/ansible-pgbouncer)
instance in front of Postgres, this makes server maintenance much easier.

## License

This playbook is distributed under the
[Apache 2.0 license](http://www.apache.org/licenses/LICENSE-2.0.html).
