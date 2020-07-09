## at-client

[![Build Status](https://travis-ci.org/Oefenweb/ansible-at-client.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-at-client)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-at--client-blue.svg)](https://galaxy.ansible.com/Oefenweb/at-client/)

Set up a persistent channel for queuing commands (using `at`) in Debian-like systems (client side).

#### Requirements

* `openssh-client` (will not be installed)
* `bash` (will not be installed)

#### Variables

* `at_client_key_map`: [default: `[]`]: SSH key declarations
* `at_client_key_map.{n}.src`: [required]: The local path of the file to copy, can be absolute or relative (e.g. `../../../files/at/home/at/.ssh/id_rsa`)
* `at_client_key_map.{n}.dest`: [optional, default `src | basename`]: The remote path of the file to copy, relative to `/etc/at` (e.g. `id_rsa`)
* `at_client_key_map.{n}.owner`: [optional, default `root`]: The name of the user that should own the file
* `at_client_key_map.{n}.group`: [optional, default `owner`, `root`]: The name of the group that should own the file
* `at_client_key_map.{n}.mode`: [optional, default `0600`]: The mode of the file to copy

* `at_client_user`: [default: `at`]: Remote user for connection

## Dependencies

None

## Recommended

* `ansible-ssh-client` ([see](https://github.com/Oefenweb/ansible-ssh-client))
* `ansible-at-server` ([see](https://github.com/Oefenweb/ansible-at-server))

#### Example(s)

```yaml
---
- hosts: all
  roles:
    - at-client
  vars:
    at_client_key_map:
      - src: ../../../files/at-client/etc/at/id_rsa
```

You will be able to schedule a command on `example.com` using:

```bash
at-ssh -h example.com -i id_rsa now <<EOF
hostname -f;
EOF
```

or

```bash
echo 'hostname -f' | at-ssh -h example.com -i id_rsa now;
```

#### License

MIT

#### Author Information

Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-at-client/issues)!
