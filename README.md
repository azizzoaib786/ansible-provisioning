# Automated Setup of fOS Machines

* Install Baseline Packages<br>
  `ansible-playbook playbook-install-baseline.yml -i hosts --become`
* Install Docker<br>
  `ansible-playbook playbook-docker-setup.yml -i hosts --become`
* Initialize Docker Swarm<br>
  `ansible-playbook playbook-docker-swarm-init.yml -i hosts --become`
