# First Branch : User Creation
### Takes Parameters:
- Hosts from the hosts file (File exists on every branch with a playbook)
- Username - user that suppose to be create, if it does not exists
- Password - password for that user, saved in jenkins
- Ansible Credentials - Used for the ansible playbook
### steps:
- Using the parameters, creating a user on every host mentioned in hosts.ini file
