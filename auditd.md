# Auditd

Auditd will let us between other things:

- Track access to files, being able to diferentiate between the different possitble access types (read, write, exectue and attribute changes)
- Track who, even not being autorized, tries t access the files.
- Track who logs or try to log into the system and what they do once inside of it.

It's important to remember that auditd works at Kernel level, making it harder to possible attackers.


## Auditd service install and management

In Red Hat family distributions, like Centos and AlamaLinux between others, it comes pre installed, however, in Debian family ones, you may need to install it manually.

Installing auditd service in Red Hat Family systems:

- sudo dnf install audit

Installing auditd service in Debian Family systems: (not for the exam but worth to know it)

- sudo apt install auditd

### Installing auditd service

| OS Family           | Command                          | 
| ------------------- | -------------------------------- |
| Red Hat             | $ sudo dnf install auditd        |
| Debian              | $ sudo apt install auditd        |


### Managing auditd service

In Red Hat family OS, the service should be started and restarted via the old service command:

$ sudo service auditd start
$ sudo service auditd restart

This is not done via systemd as this will record a user ID value properly as explained in the [Red Hat Documentation](https://www.redhat.com/sysadmin/configure-linux-auditing-auditd)