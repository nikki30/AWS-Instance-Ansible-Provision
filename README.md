
I used Playbook here to configure the servers according to a baseline, so they all are using the correct ssh config and central authentication. 

Then I used roles for specific server groups. Firing off the Playbook allows Ansible to install and configure the web server. It will make sure my database server allows connections from the new server, and then adds the new server to my network monitoring solution so that I am informed if the server suffers a failure in the future.

Thus, to run this:
Create a variables file using *ec2_vars/sample.yml* as a template.

E.g. 

    cp ec2_vars/sample.yml ec2_vars/webservers.yml
    vi ec2_vars/webservers.yml
    
After setting all variables, run it:

    ansible-playbook -vv -i localhost, -e "type=webservers" provision-ec2.yml
    
