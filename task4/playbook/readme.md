# Execute those commands from the machine that run ansible.

## Configure Ansible
#  standard path to configuration file
#
#    $ sudo vi /etc/ansible/ansible.cfg
#
# you can use the file in your current directory:
# 
#    $ nano ./ansible.cfg
```
# uncomment this to disable SSH key host checking
host_key_checking = False
```

## Edit hosts file

    $ sudo vi /etc/ansible/hosts

# or in the current dir and using nano:
#   $ nano ./my_hosts

```
[awsec2instances]
ec2-3-67-224-147.eu-central-1.compute.amazonaws.com
ec2-18-196-183-134.eu-central-1.compute.amazonaws.com
```


## Run ansible
# replace with your key' name
    $ chmod 600 my-key.pem   
    $ ansible-playbook --syntax-check --private-key my-key.pem -u ec2-user ansible_playbook-aws-install-docker-2021.yml
