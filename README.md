# ansible-unpack

yum install epel-release && yum install python2-pip -y

sudo easy_install pip==20.3.4

pip install ansible

mv ansible-unpack .local

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

```
echo $PATH
export PATH=$PATH:~/.local/bin:~/bin

mkdir ~/.local/bin -p
mkdir ~/.local/lib/python2.7/site-packages -p

cp /bin/ansible-2.7 ~/.local/bin/ansible
cp /usr/bin/sshpass ~/.local/bin/

for i in "ansible" "jinja2"; do cp -r /usr/lib/python2.7/site-packages/$i ~/.local/lib/python2.7/site-packages/; done

for i in "yaml" "markupsafe"; do cp -r /usr/lib64/python2.7/site-packages/$i  ~/.local/lib/python2.7/site-packages/; done

tar -cf local.tar .local

tar -xf local.tar

export ANSIBLE_HOST_KEY_CHECKING=False
ansible linux -i inventory -m shell -a 'systemctl restart httpd' -u ledivan --ask-pass -b -K

```
ANSIBLE_HOST_KEY_CHECKING=False ansible linux -i inventory -m shell -a 'ping 8.8.8.8 -c 4' -u root --ask-pass -b -K
