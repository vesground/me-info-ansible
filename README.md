// SETUP OPTIONS
**1. Update vars/ip in "demo" and "prod" run files (site.retry)**
**2. Replace repo ssh keys configs in "files" directory on your own (Dont push it to repo)**
**3. Update all variables depend on your app in "group_vars" directory**
**4. Update "site.yml" depend on your dependencies (add new dependencies in "galaxyfile.yml" to install it later)**
**5. Write your own roles in "roles" directory (all configs of your app put into templates)**
**6. Install roles**
sudo ansible-galaxy install -r galaxyfile.yml --force

**7. Copy public ssh key to server**
ssh-copy-id user@domain -p port


// RUN OPTIONS
**Deploy with vagrant**
vagrant box add ubuntu/trusty64
vagrant up

**Deploy project to staging**
ansible-playbook site.yml -i staging --ask-sudo-pass

**Deploy project to production**
ansible-playbook site.yml -i production -e ansible_ssh_private_key_file=/home/user/.ssh/private_key



### Security precautions
1. Never place git key with write access in files. Always use only "Deployment keys".
2. Never attach deployment key to the repo with ansible-playbook. It can happen that your server (any staging or another) is compromised an attacker will be able to clone repos with ansible which can have important information (like host passwords, db password, security keys etc).
3. Do not place production keys in the repo (a lot of people usually have access to the repo beacuse the same repo is used for vagrant, staging etc). Another soultion is to encrypt security-sensetive data, ansible has built-in mechanism for this. http://docs.ansible.com/ansible/playbooks_vault.html
