Ansible Role: systemd-timesyncd
===============================

An Ansible role that configures **systemd-timesyncd**.


Table of Contents
-----------------

<!-- toc -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
  * [Time Zone](#time-zone)
  * [NTP Servers](#ntp-servers)
  * [Purge Legacy Packages](#purge-legacy-packages)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Top-Level Playbook](#top-level-playbook)
  * [Role Dependency](#role-dependency)
- [Tags](#tags)
- [License](#license)
- [Author Information](#author-information)

<!-- tocstop -->

Requirements
------------

- Ansible 2+


Role Variables
--------------

### Time Zone

Set the system time zone. There is no default. The prefix is `system_` on
purpose, so this variable can be used across different roles that also set the
time zone.

```yml
system_timezone: Europe/Berlin
```

### NTP Servers

NTP servers are the preferred servers. They should be set to your networks
internal NTP servers.

```yml
ntp_servers:
  - ntp1.domain.org
  - ntp2.domain.org
  - ntp3.domain.org
```

Use regional pools for fallback servers:

```yml
ntp_fallback_servers:
  - 0.europe.pool.ntp.org
  - 1.europe.pool.ntp.org
  - 2.europe.pool.ntp.org
  - 3.europe.pool.ntp.org
```

### Purge Legacy Packages

Remove legacy timesync packages (ntp, chrony):

```yml
systemd_timesyncd_purge_legacy_packages: yes
```


Dependencies
------------

None.


Example Playbook
----------------

Add to `requirements.yml`:

```yml
---

- src: idiv-biodiversity.systemd_timesyncd

...
```

Download:

```console
$ ansible-galaxy install -r requirements.yml
```

### Top-Level Playbook

Write a top-level playbook:

```yml
---

- name: head server
  hosts: head

  roles:
    - role: idiv-biodiversity.systemd_timesyncd
      tags:
        - systemd
        - systemd-timesyncd
        - timesync

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: idiv-biodiversity.systemd_timesyncd
    tags:
      - systemd
      - systemd-timesyncd
      - timesync

...
```

Tags
----

With these tags, only specific parts of the role can be triggered:

- `timezone`: just set the time zone
- `systemd-timesyncd`: configure `/etc/systemd/timesyncd.conf` and restart the
  service if changed
- `service`, `service-timesyncd` and `timesyncd-service`: enable and start the
  service; the purpose of the plain `service` tag is that you can enable and
  start all services across roles by using this tag, e.g. `ansible-playbook
  site.yml -t service`

The tags from the [Example Playbook](#example-playbook) are `timesyncd` and
`timesync`. In case you switch from different time synchronization roles, the
`timesync` tag should come in handy, in case these roles also use this tag.


License
-------

MIT


Author Information
------------------

This role was created in 2017 by [Christian Krause][author] aka [wookietreiber
at GitHub][wookietreiber], HPC cluster systems administrator at the [German
Centre for Integrative Biodiversity Research (iDiv)][idiv].


[author]: https://www.idiv.de/groups_and_people/employees/details/eshow/krause-christian.html
[idiv]: https://www.idiv.de/
[wookietreiber]: https://github.com/wookietreiber
