WARNING: This role is no longer maintained !!!
==============================================

You are strongly encouraged to switch to the new roles stack on https://github.com/ElaoInfra
--------------------------------------------------------------------------------------------

By the way, this role will remain available on https://github.com/ElaoLegacy
----------------------------------------------------------------------------


Ansible Role - Cron
===================

A Cron role to add cron jobs on elao symfony standard vagrant box


Requirements
------------

This role only run on elao symfony standard vagrant box. See https://vagrantcloud.com/elao/symfony-standard-debian


Role Handlers
-------------

cron restart


Role Variables
--------------

 Variable  | Required | Default  | Choices        | Comments
 --------  | -------- | -------- | -------------- | --------------------------
 name      | yes      |          |                | Description of crontab entry. Must be unique.
 job       | *        |          |                | The command to execute. Required if state=present
 minute    | no       | *        |                | Minute when the job should run (0-59, *, */2, etc)
 hour      | no       | *        |                | Hour when the job should run (0-23, *, */2, etc)
 day       | no       | *        |                | Day of the month the job should run (1-31, *, */2, etc)
 month     | no       | *        |                | Month of the year the job should run (1-12, *, */2, etc)
 weekday   | no       | *        |                | Day of the week that the job should run (0-6 for Sunday-Saturday, *, etc)
 cron_file | no       |          |                | If specified, uses this file in cron.d instead of an individual user's crontab.
 user      | no       |          |                | The specific user whose crontab should be modified.
 state     | no       | present  | present,absent | Whether to ensure the job is present or absent.
 
Example Playbook
----------------
```yml
- hosts: servers
  vars:
    elao_cron_jobs:
      # Ensure a job that runs at 2 and 5 exists.
      # Creates an entry like "0 5,2 * * ls -alh > /dev/null"
      - name:   check dirs
        minute: 0
        hour:   "5,2"
        job:    "ls -alh > /dev/null"
      # Ensure an old job is no longer present. Removes any job that is prefixed
      # by "#Ansible: an old job" from the crontab
      - name:  an old job
        state: absent
 roles:
  - { role: elao.cron }
```

License
-------

MIT


Author Information
------------------

http://www.elao.com/
