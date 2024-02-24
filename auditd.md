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


### Auditd rules

In the previous section, we mentioned 2 files, where we will store the rules about what we want to audit. In this section, I will explain what are the audit rules, what kind of audit rules we have. 

#### What is an audit rule?

An audit rule is a directive, that has a defined format, that we will used to specify what events we would like to montior and log by auditd, like auditing access to a file, auditing system calls, login attempts, etc.

#### Introduction of auditctl command

Before continuing with rules, I will introduce auditcl, as it is a command that will allow us to create ***non persistent*** auditd rules, that is, these rules won't persist after reboot.

It is very important to remember that ***rules created using auditctl will not be persistent***, as perisisting rules is what is required for the exam, however, auditctl will let us test rules before persisting them, which we will learning latter.

The basic usage of auditctl that we will need for now are:

$ auditctl <rule> ---> to create a non persistent rule
$ audictl -l      ---> to list the rules currently being applied

There are other uses that we will be discovering while we move forward.

#### Creating rules to audit files and folders

To audit files and directory access, incluiding read, write, execute and attribute change access we need to define a watch rule.

Watch rules follow the next pattern:

-w <path_to_file_or_directory> -p <permissions> -k <key_name>

Now lets break it down:

-w: to specify the path of the file or directory you would like to watch
-p: to specify the the permissions you would like to watch (r=read w=write x=execute a=modify attributes)
-k: to specify the key, which is just a string you define to easily identify the logged entries associated with this rule.

In the case of permissions, just add the letters corresponding to the permissions you would like to monitor (rwxa), with no spaces, for exmple, if you want to audit read and write opperations on the file, your permissions would be rw.

Example 1:
  Let's supose that we would like to monitor access to the file /secret-files/example1.txt and that we would like to monitor who tries to read and write it.

  To build the rule, following the pattern explained before:
   
    -w <path_to_file_or_directory> -p <permissiones> -k <key_name>
   
    -w /secret-files/example1.txt -p rw -k rw_example1.txt

  Now our rule is there, but, how do we apply it?

  For now, we will use auditctl to create the rule, later, I will show how to persist the rules.

```
  $ sudo auditctl -w /secret-files/example1.txt -p rw -k rw_example1.tx
```
  
```
$ sudo auditctl -l
-w /secret-files/example1.txt -p rw -k rw_example1.tx
```





