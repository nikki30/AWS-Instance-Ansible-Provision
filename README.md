
I used Playbook here to configure the servers according to a baseline, so they all are using the correct ssh config and central authentication. 

Then I used roles for specific server groups. Firing off the Playbook allows Ansible to install and configure the web server. It will make sure my database server allows connections from the new server, and then adds the new server to my network monitoring solution so that I am informed if the server suffers a failure in the future.

I was looking to build EC2 hosts with more consistency. I realized that using Ansible, it is easy to provision EC2 hosts and put some logic on it to adjust EC2 parameters based on the type of host to be built.

The easiest way to start is to create a playbook calling the ec2 module with the parameters we want to pass to AWS to create our host. This project is a ittle more scalable way to do this, where the parameters are variables and we can easily have multiple types of hosts sharing the same playbook and role.

The solution is organized in 3 parts:

* A generic Ansible role that uses ec2 module to provision
* Yaml files with variables that will be used as parameters for each type of EC2 host
* Playbook that combines the variables file with the role

Thus, to run this:
Create a variables file using *ec2_vars/sample.yml* as a template.

E.g. 

    cp ec2_vars/sample.yml ec2_vars/webservers.yml
    vi ec2_vars/webservers.yml
    
After setting all variables, run it:

    ansible-playbook -vv -i localhost, -e "type=webservers" provision-ec2.yml
    
