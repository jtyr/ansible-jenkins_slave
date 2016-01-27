jenkins_slave
=============

Ansile role which helps to configure Jenkins Slave server usable
exclusively via Jenkins' built-in SSH client.

Please report any issues or send PR.


Usage
-----

```
# Example of how to set up this role with password authentication
- name: Jenkins Slave
  hosts: jenkins-slave1
  vars:
    # User's password (the password here's "jenkins")
    jenkins_slave_user_password: $6$EMHNyscZCxOH6KmN$1d4nk/cJ6Tt0JBsuusjlgpN4dwZsKirxMRZI0x8rtrpW3CvSw6legf2E5WEJ8wmwjWFQSYRxbb5rXMtF81hoy/
  roles:
    - jenkins_slave

# Example of how to set up this role with SSH key authentication
- name: Jenkins Slave
  hosts: jenkins-slave2
  vars:
    # Public SSH key
    jenkins_slave_user_authorized_key: ssh-rsa AAAAN3Bza1Cyc2EDAAAAAQABAAABAQCyUc0AMSzOwG6HL8N0EajmjMFONVu99S1qnfgfzxhntN0/Yh3v+7aVfSd3nmSPfEmp8I4YMUk0pSigp2iYHOtth3vmpOkUtSO6ISkPnwsCSBcdvDTBudJfAjgm1YAlg0ObnuS5geHUZ5vShnCbjxC1oRTciXT0pl00iqVSkPGBmoPzyWDTT9oCsalWkxa78gFCIo0xyVwLM5ZpcBsa+0XNO/DKaOhJ4gZ5uttrw52yqCXigWP4pj3FXTyvBjLNxLBly3gSU1hq/5JqV04f7Fw6kFa4zafFsSe6zbwYbhswaRkXPR81XXkUtWjJjbtLHgZfd17faPeuAt0eV65/6rJf
  roles:
    - jenkins_slave

# Example of how to set different remote root directory
- name: Jenkins Slave
  hosts: jenkins-slave3
  vars:
    # User's password (the password here's "jenkins")
    jenkins_slave_user_password: $6$EMHNyscZCxOH6KmN$1d4nk/cJ6Tt0JBsuusjlgpN4dwZsKirxMRZI0x8rtrpW3CvSw6legf2E5WEJ8wmwjWFQSYRxbb5rXMtF81hoy/
    # New user name
    jenkins_slave_user_name: jenkinsci
    # New user home directory
    jenkins_slave_user_home: /opt/{{ jenkins_slave_user_name }}
  roles:
    - jenkins_slave
```


Role variables
--------------

```
# Jenkins user name
jenkins_slave_user_name: jenkins

# Jenkins user group
jenkins_slave_user_group: "{{ jenkins_slave_user_name }}"

# Jenkins user ID
jenkins_slave_user_uid: 498

# Jenkins user group ID
jenkins_slave_user_gid: 498

# Additional Jekins user groups
jenkins_slave_user_groups: ''

# Jenkins used home directory
jenkins_slave_user_home: /home/jenkins

# Jenkins user pasword
# (use `grub-crypt --sha-512` to generate one)
jenkins_slave_user_password: ''

# Jenkins user authorized SSH key
jenkins_slave_user_authorized_key: ''

# List of packages which should be installed - mainly Java (exact version can be specified here)
# (set this to empty list if using another role for the Java installation)
jenkins_slave_pkgs:
  - java-openjdk
```


Dependencies
------------

- [`jenkins_master`](http://github.com/jtyr/ansible-jenkins_master) (optional)


License
-------

MIT


Author
------

Jiri Tyr
