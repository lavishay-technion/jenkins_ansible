# Ansible Jenkins Pipeline

Creates Jenkins multi-branch pipeline that takes password, sshkey, NGINX. 
All the details will be used to setup the remote host with all the provided data to pipeline via ansible playbooks/roles

### Steps

- First Branch : User Creation
    - Takes Parameters:
        - Hosts from the hosts file (File exists on every branch with a playbook)
        - Username - user that suppose to be create, if it does not exists
        - Password - password for that user, saved in jenkins
        - Ansible Credentials - Used for the ansible playbook
    - steps:
        - Using the parameters, creating a user on every host mentioned in hosts.ini file

- Second Branch : Golden SSH Key for Passwordless connection
    - Takes Parameters:
        - Hosts from the hosts file (File exists on every branch with a playbook)
        - Golden ssh key for future remote connection
        - Ansible Credentials - Used for the ansible playbook
    - steps:
        - Creating .ssh file under root's home user, in case it doesn't exist
        - Creating authorized_keys file, if doesn't exist
        - Adding the golden_ssh_key.pub's text into authorized_keys file
        - Copying the private key locally to the worker for testing(To test the ssh passwordless connection

- Third Branch: Installations
    - Takes Parameters:
        - Hosts from the hosts file (File exists on every branch with a playbook)
        - Port(The port NGINX will be operating on)
        - index file(The basic HTML file that will be displayed by nginx)
        - server(Hostname of the server that will host the html file)
        - title(Text that will be displayed in the HTML file)
        - Ansible Credentials - Used for the ansible playbook
    - steps:
        - Installation of Nginx on both Rocky and Debian hosts and starting the service
        - Removing existing NGINX configuration file, and index.html file in /var/www/html (If exists)
        - Copying new NGINX conf and html file using jinja templates
        - restarting NGINX

### Notes

- Ansible plugin for jenkins requires additional configuration, please RTFM


