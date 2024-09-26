Hi, ![](https://user-images.githubusercontent.com/18350557/176309783-0785949b-9127-417c-8b55-ab5a4333674e.gif)my name is Serhii Shypylov
=========================================================================================================================================

💛 I am a Linux System administrator engineer with DevOps practices. I have several certificates in Linux, Docker, Ansible and Terraform and continue to learn more. I like everything related to Docker, containers and IT technologies in general. I love solving complex IT solutions.
-------------------------------

* 💼 Looking for a job
* 🌍 I'm based in Poznan
* 🖥️ See my [LinkedIn](https://github.com/Shipssv83) profile 
* 👾 Chat with IT pros on [Discord](https://discord.com/shipssv_19055)\
* 📧 Reach me at ships@ukr.net
* 🧠 I'm learning DevOps Practices

### Socials

<p align="left"> <a href="https://github.com/Shipssv83" target="_blank" rel="noreferrer"> <picture> <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/github-dark.svg" /> <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/github.svg" /> <img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/github.svg" width="32" height="32" /> </picture> </a> <a href="https://www.linkedin.com/in/sergey-shipilov-7262a31b4/" target="_blank" rel="noreferrer"> <picture> <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/linkedin-dark.svg" /> <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/linkedin.svg" /> <img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/linkedin.svg" width="32" height="32" /> </picture> </a></p>

# Ansible Playbook: Create Users on Linux (Ubuntu Server)

This Ansible playbook automates the process of creating and managing users, groups, and SSH keys on Ubuntu servers. It includes tasks to create users, assign groups, configure SSH keys, manage user profiles, and grant sudo privileges.

## Requirements

- Ansible version 2.9 or higher
- Target machines running Ubuntu or other Unix-based systems
- SSH access to target machines

## Playbook Structure

### Roles
This playbook includes the `roles/system-users` role to handle user and group management. Tasks for creating users and groups are executed within this role.

### Tasks
The key tasks handled by this playbook include:
- Creating user groups
- Per-user group creation (optional)
- Creating users
- Assigning SSH keys to users
- Setting up user profiles
- Managing sudo access
- Removing users, groups, and home directories

## Variables

You need to define the following variables:

- `hosts`: The target hosts where the playbook will be applied.
- `users`: A list of users to be created.
- `groups_to_create`: A list of groups to be created.
- `users_deleted`: A list of users to be removed.

### Example Variables
```yaml
vars:
  users:
    - username: "john"
      name: "John Doe"
      password: "$6$random_salt$encrypted_password"
      groups: ["sudo", "developers"]
      shell: "/bin/bash"
      priv: "john ALL=(ALL) NOPASSWD:ALL"
      ssh_key:
        - "ssh-rsa AAAAB3Nza..."
      profile: "export PATH=$PATH:/usr/local/bin"
    - username: "alice"
      name: "Alice Smith"
      password: "$6$random_salt$encrypted_password"
      shell: "/bin/zsh"
  groups_to_create:
    - name: "developers"
      gid: 1001
  users_deleted:
    - username: "olduser"
```

# Run the Playbook create user
Run the playbook by specifying your inventory file and variable file:

user root
```
ansible-playbook -i hosts --user root --limit "hostname-server" playbooks/users_main_playbook.yml --tags dev
```

user ubuntu
```
ansible-playbook -i hosts --user ubuntu  --limit "hostname-server" playbooks/users_main_playbook.yml --tags dev
```

License
This project is licensed under the MIT License