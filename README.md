# Ansible PostgreSQL playbook

[![Build Status](https://travis-ci.org/balanced-ops/ansible-postgresql.svg)](https://travis-ci.org/balanced-ops/ansible-postgresql)

This is an Ansible playbook for deploying PostgreSQL 9.1, 9.2 or 9.3.

This playbook was tested on Ubuntu 12.04 x86_64.

## Features

* Install PostgreSQL
* Install development headers (optional)
* Install wal-e (optional)
* Install repmgr (optional)

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

## See also

You'll probably want to put a [pgbouncer](https://github.com/balanced-ops/ansible-pgbouncer)
instance in front of Postgres, this makes server maintenance much easier.

## License

This playbook is distributed under the
[Apache 2.0 license](http://www.apache.org/licenses/LICENSE-2.0.html).
