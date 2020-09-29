# AnsibleAWSInfra
Creating AWS infrastructure using Ansible

	Installation of Ansible: (RHEL)
	1. $ Yum upgrade -y
	2. $ hostnamectl  --------provides the information and version of the linux installed
	3. $ cat /etc/redhat-release ---- provides the version of the rhel linux installed
	4. $ yum install python3  ---- installs python 3 
	5. $ sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm -y
	6. $ sudo yum install ansible
	7. $ ansible --version
	8. $ sudo useradd ansadmin  --- create user ansadmin
	9. $ sudo passwd ansadmin  --- password for ansadmin -- twice
	10. $ nano /etc/ssh/sshd_config  ------ PasswordAuthentication yes
	11. $ visudo 
		a. Add " $ ansadmin        ALL=(ALL)       NOPASSWD: ALL"
	12. $ pip3 --version  -- if not installed already , install pip
	13. $ sudo pip3 install boto boto3
	14. $ sudo pip3 install awscli
	15. -----"find / -type f -name "*.conf" --- to find any file across linux env
	16. Create an IAM role giving full access to EC2 and attach the role to the ec2 instance/ansible master.
	17. Create a directory in home of ansadmin 
		a. $ mkdir ANSConfig
	18. Create ansible vault for user access key and secret key
		a. Get the access key and secret key for ansadmin from AWS IAM
		b. Create dir group_vars/all inside ANSConfig
		c. $ ansible-vault create group_vars/all/pass.yml
		d. It asks for vault password -- provide the password twice
		e. It opens up the pass.yml file, copy and paste the access key and secret key in to the file using ":" colon instead of "="equals
		f. Save the file
		g. $ ansible-vault view group_vars/all/pass.yml -- it asks for password, once entered, the decrypted file will be shown
	19. Create hosts file 
		a. Add [webserver] in the file. Save it
	20. $ cp /etc/ansible/ansible.cfg ansible.cfg   --- copy the default cfg file to this dir.
		a. Change the hostname file to point to hosts in this dir
		b. In the cfg file, put "host_key_checking = False"
	21. Copy and paste the code into the playbook.yml file
	22. If you do not want to enter the password for vault everytime you run the playbook, you can use the vault file
		a. $ openssl rand -base64 2048 > vault.pass
		b. $ ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
		c. $ ansible-playbook playbook.yml --vault-password-file vault.pass   ----   instead of  " $ansible-playbook playbook.yml --ask-vault-pass"

	23. Run the following files :
		a. Ansible-playbook ec2-config.yml
		b. Ansible-playbook ec2-ssh-config.yml
