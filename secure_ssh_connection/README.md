# Ansible Secure Connections with SSH RSA for Linux

**make sure you have openssh package**

    sudo apt-get install openssh-client

## Copy SSH files **manualy**

### step 1 execute this command in client machine to create new key:

    ssh-keygen -t rsa -b 4096 -v

### step 2 change its permissions

    chmod 700 ~/.ssh/id_rsa

### step 3 chnage id_rsa.pub name

    mv ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys

#### we must do this because its the address that sshd service will check it when we want to do login. you can change the address in

    /etc/ssh/sshd_config

#### search for AuthorizedKeysFile and change the address.

#### there is some other options in this file like

    PasswordAuthentication
    RSAAuthentication
    UsePAM
    PubkeyAuthentication

#### make sure UsePAM and RSAAuthentication is equal to yes.

#### if you changed the sshd configs you must restart ssh service

    #Debian base
    systemctl restart ssh

    #Redhat base
    systemctl restart sshd

### step 4 then change the authorized_keys file permissions

    chmod 600 authorized_keys

### step 5 after this we must copy ssh key to ansible server:

    scp ~/.ssh/id_rsa root@server_address:/some_address_to_manage_ansible_ssh_keys/

### step 6 then in host file we must add ansible_ssh_private_key_file variable in front of host address and give it the file address

ansible_ssh_private_key_file=address_of_file_in_ansible_server

after this steps the ansible will connect with rsa ssh files

## Copy SSH files with ssh-copy-id command

we execute this command from ansible server to all client machines to get permission to connect without passwords.

### step 1 get new ssh keys

    ssh-keygen -t rsa -b 4096 -v

### step 2 copy them to client one by one

    ssh-copy-id root@slave_node_address

then system asks us for password of client. after that we dont need to use password or ssh file in our ansible inventory file
