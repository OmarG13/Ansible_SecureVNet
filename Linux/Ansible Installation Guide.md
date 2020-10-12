Install docker.io on your Jump box.


sudo apt update
sudo apt install docker.io
sudo systemctl status docker 


If the Docker service is not running, start it:

* sudo systemctl start docker


Once Docker is installed, pull the container cyberxsecurity/ansible and start it.

* sudo docker pull cyberxsecurity/ansible.
* sudo docker run -ti cyberxsecurity/ansible bash (for first launch only)

Start and attach to an Ansible session and modify the hosts file and ansible.cfg
* sudo docker start {container ID}
* sudo docker attach {container ID}
* cd /etc/ansible/
* ansible.cfg: modify "remote_user = {username}"
* hosts file: modify the hosts section to include the machines onto which Elk will be deployed:
[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3
