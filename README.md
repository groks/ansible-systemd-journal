systemd-journal
========

An [ansible role](https://galaxy.ansibleworks.com/) to configure the systemd
[journal](http://0pointer.de/blog/projects/systemctl-journal.html) to handle all
logging and more tightly limit it's log storage, suitable for an SSD on
a laptop.

This role will remove the rsyslog package on F19 (already the default on F20)
unless you tell it otherwise.

    ---
    - hosts: localhost

      roles:
        - groks.systemd-journal

Requirements
------------

A recent version of [Fedora](https://fedoraproject.org/get-fedora) Linux.

Role Variables
--------------

    vars:
      - systemd_journal_rsyslog_package_state: absent
      - systemd_journal_system_max_use: 500M
      - systemd_journal_system_max_file_size: 50M

The journal will be default use as much free space as it can get and then delete
old logs if other data fills a disk. That's not very friendly for SSD drives so
`systemd_journal_system_max_use` limits this to 500M by defaut, or whatever you
customise it to.

`systemd_journal_rsyslog_package_state` can be `absent` or `present` and if
`absent` (the default) the `rsyslog` package will be removed.

Dependencies
------------

None.

License
-------

BSD
