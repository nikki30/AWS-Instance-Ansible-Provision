# Problem solved: Managing many related AWS cloud services from a centralized computer
I was looking to build EC2 hosts with more consistency. I realized that using Ansible, it is easy to provision EC2 hosts and put some logic on it to adjust EC2 parameters based on the type of host to be built.

The easiest way to start is to create a playbook calling the ec2 module with the parameters we want to pass to AWS to create our host. This project is a little more scalable way to do this, where the parameters are variables and we can easily have multiple types of hosts sharing the same playbook and role.

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
    
