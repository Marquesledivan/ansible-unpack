# ansible-unpack

yum install epel-release && yum install python2-pip -y

sudo easy_install pip==20.3.4

pip install ansible

mkdir .local && mv * .local

export PATH=/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/ledivan/.local/bin:/home/ledivan/bin

```
cat .ansible.cfg

[defaults]
ansible_python_interpreter=/usr/bin/python3
private_key_file = /Users/ledivan/.ssh/id_rsa
inventory = /Users/ledivan/temp/inventory
remote_user = ledivan
deprecation_warnings = False
command_warnings = False
host_key_checking = False
remote_port = 22

[privilege_escalation]
become=True
become_method=sudo
become_ask_pass=False
```

ANSIBLE_HOST_KEY_CHECKING=False ansible linux -i inventory -m shell -a 'ping 8.8.8.8 -c 4' -u root --ask-pass -b -K