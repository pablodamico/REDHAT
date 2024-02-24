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

#### Red Hat family OS

The service should be started and restarted via the old service command:
$ sudo service auditd start
$ sudo service auditd restart

This is not done via systemd as this will record a user ID value properly as explained in the [Red Hat Documentation](https://www.redhat.com/sysadmin/configure-linux-auditing-auditd)


To enable the service you can use the systemctl commands:
$ systemctl enable auditd


#### Ubuntu Family

In the Ubuntu Family, you can do everything using systemctl commands:
$ sudo systemctl start auditd
$ sudo systemctl restart auditd
$ sudo systemctl enable auditd

#### To summarize:

| OS Family           | Commands                          | 
|-----------|----------------------------------|
| Red HAT   | $ sudo service auditd start<br>$ sudo service auditd restart<br>$ sudo systemctl enable auditd |
| Debian    | $ sudo systemctl start auditd<br>$ sudo systemctl restart auditd<br>$ sudo systemctl enable auditd |


### Auditd configuration and logs files

- Auditd has 2 main configuration files:
   * /etc/audit/auditd.conf  
   * /etc/audit/auditd.rules  
     
- The logs files are stored by default in:  
   * /var/log/audt/audit.log  
  
- It's worth to mention that we can also store our rules in:  
   * /etc/audit/rules.d/

The management of these files will be explained later, but I believe it is important at this point to know and to check them to start being familiar with them and where they are located.

#### To summarize:

| Files and folders        | Description                     |
|--------------------------|------------------------|
| /etc/audit/auditd.conf   | Auditd configuration file, where we will configure differnt options like log sizes, logs file location, etc  |
| /etc/audit/auditd.rules  | Rules condiguration file, where we will add rules to persiste them over reboots, here we will save the rules about what we want to audit |
| /etc/audit/rules.d       | In this folder we will save rules as well, with the same purpose of the previous file. |
| /var/log/audit/audit.log | Default place where audit logs are stored |



