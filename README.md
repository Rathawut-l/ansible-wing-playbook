Infrastructure as a code with Ansible + Docker
===========================================================================

This repository is the skeleton to do infrastructure as a code with Ansible + Docker. You will have
- Ansible playbooks in all yml files on root repository
- Sample inventory files for each service in ```inventories``` directory
- Sample variable files with heavily comment for each service in ```vars``` directory
- Sample configuration files for each service in ```files``` directory
- Documents how to use each role and tutorial in ```docs``` directory
- Roles that will separate into each Ansible Galaxy repository. You can see all the roles in ```galaxy-requirements.yml```

Pre-requisites
---------------------------------------------------------------------------

- Docker 1.12 or up
- Docker Machine 0.8.0 or up
- Ansible 2.1 (with patch) or up
- Make sure that you can ssh to target machine

Tutorial
---------------------------------------------------------------------------

- [Getting started](docs/tutorials/01_getting_started.md)

How to Use
---------------------------------------------------------------------------

- Fork this repository and make your own configuration from example files
- You can see all my galaxy role in ```galaxy-requirements.yml``` file. To install or update all roles, run the command

```bash
# Use -f to force reinstall roles
ansible-galaxy install -f -r galaxy-requirements.yml
```

- You shouldn't have to edit any file in this repository. This make you easier to maintain and update playbook from upstream
- If you find yourself that you have to edit any file in this repository so it means that you have to send that pull request to me :P
- To update playbook from upstream. Run below commands

```bash
# http://stackoverflow.com/questions/7244321/how-do-i-update-a-github-forked-repository
# Add the remote, call it "upstream":
git remote add upstream https://github.com/winggundamth/ansible-wing-playbook.git

# Fetch all the branches of that remote into remote-tracking branches,
# such as upstream/master:
git fetch upstream

# Merge upstream/master to your forked repository
git merge upstream/master
```

Variable priority
---------------------------------------------------------------------------

According to [Variable Precedence: Where Should I Put A Variable?](http://docs.ansible.com/ansible/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable). Order of variable priority would be (The last listed variables win)

- roles/*/default/main.yml
- group_vars/all
- group_vars/group_name
- host_vars/all
- host_vars/group_name
- vars/*.yml (as specific vars_file in inventory file)
- extra vars with -e with ```ansible-playbook``` command

So from above priority. In use case you want to specific something like the memeory of elastic search and will be difference on each cluster. You should create default allocate memory variable in ```group_vars/all``` file and specific memory for each cluster in ```group_vars/group_name```. Don't forget to change *group_name* file name to your group name. And don't forget to remove or comment that variable in ```vars/*.yml``` since it will overwrite and win the priority.

Playbooks list
---------------------------------------------------------------------------

- [Host preparation](docs/host_preparation.md)
- [Install Docker](docs/install_docker.md)
- [Install New Relic agent](docs/newrelic.md)
- [Manage Docker Machine](docs/docker_machine.md)
- [Manage nginx container](docs/nginx_container.md)
- [Install Docker Compose](docs/docker_compose.md)
- [Run apt-cacher-ng container](docs/apt_cacher_ng_container.md)
- [Manage Mongo container](docs/mongo_container.md)
- [Manage ElasticSearch container](docs/elasticsearch_container.md)
- [Manage Graylog container](docs/graylog_container.md)
- [Manage PostgreSQL container](docs/postgresql_container.md)
- [Manage Redis container](docs/redis_container.md)
- [Manage GitLab container](docs/gitlab_container.md)
- [Manage Docker Registry container](docs/docker_registry_container.md)

License
-------

The MIT License (MIT)
