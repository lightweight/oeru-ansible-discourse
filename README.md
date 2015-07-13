# oeru-ansible-discourse
An Ansible Playbook for installing Discourse on OERu's server - this (in theory) can be used on any Linux server with APT, although it's only been tested on servers running Ubuntu 14.04.

It uses a dual Docker container approach:
1. the webserver and most of the important app-related configuration  (including SMTP) and
2. the data container for both PostgreSQL (database) and Redis (queue).

The goal is to have
* the web app in a Docker container, talking to
* the data sources (PostgreSQL and Redis), with
* nginx on the underlying host (localhost) proxying the relevant forwarded port (usually 8080) on port 80 (eventually 443 instead) in response to the designated domain name (canonical: community.oeru.org)

Prerequisite:
* install Ansible:
sudo aptitude install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible

Assumes a system user "discourse":
sudo adduser --system --home /home/www/discourse --ingroup docker --disabled-password discourse

To run this from the Ansible git repo top level:
ansible-playbook site.yml
