# mheap.app-backup

Originally designed to back up WordPress installs, this should work for anything
that has a database and a single folder. It'll dump the database, take a copy of
all the files and download a zip file containing everything to your local 
directory.

This playbook has been tested on Ubuntu with the zip extension installed. It 
should work on any Linux, but is untested

### Usage

Create a `playbook.yml` that includes the role and a folder and database to
back up.

```yaml
---
- hosts: all
  gather_facts: false
  roles:
      - role: mheap.app-backup
        name: Nice Name
        working_dir: /var/www/site
        db_name: my_database
        db_user: username
        db_pass: password
```

Then run:

```
ansible-playbook -i /path/to/inventory playbook.yml
```

Your files will now be in the current directory.

### Advanced usage

If your `root` user has a `.my.cnf` that allows access to all databases without
a password, you can omit `db_user` and `db_pass` and the role will automatically
`sudo` and dump the databases. You'll need to run `ansible-playbook -K` if using
this functionality
