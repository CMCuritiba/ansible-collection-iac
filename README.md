# Ansible Collection - CMCuritiba.IaC

Documentation for the collection.

This is still a work in progress.

## Requirements

- Ansible 2.10.3 or higher
- Python 3.8.5 or higher

## Instructions for installing CMCuritiba.IaC

- Optional: Create a python virtual environment and activate it before executing subsequent steps.

1. Install the following packages (use the latest available version):
   1. Ansible
1. Install collection using ansible galaxy (**TODO**):
   1. Example command to install:
      `ansible-galaxy collection install CMCuritiba.IaC`
   1. Example command to upgrade to the latest version:
      `ansible-galaxy collection install CMCuritiba.IaC --force`
1. Update existing playbooks to work with collection:
   1. Rename all roles referenced inside playbooks to begin with CMCuritiba.IaC.
   1. Remove all references to `cmc_server_hostname`. `cmc_server_hostname` was replaced with ansible's `inventory_hostname_short` special variable.
1. Miscellaneous
   1. Please submit a pull request on so we can merge your roles into the collection.

## Guia do ameba

1. Instalar o Ansible na máquina controladora. Sugestão, de acordo com [esta documentação](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-with-pip):

   ```bash
   sudo apt install python-is-python3 python3-pip
   sudo pip3 install ansible
   ```

1. Garanta o acesso do controlador ao _host_ (por exemplo, compartilhando chaves entre o controlador e os _hosts_)
1. Instalar a _collection_ [CMCuritiba.IaC](https://github.com/CMCuritiba/ansible-cmc-servers).
   As alternativas de instalação são:
   1. Faça o download do projeto como `.zip` e descompacte em `./collections/ansible_collections/` ou `~/.ansible/collections/ansible_collections/`
   1. Clone o projeto localmente em `./collections/ansible_collections/` ou `~/.ansible/collections/ansible_collections/`
   1. Utilizando o galaxy para baixar o código do repositório através de um `requirements.yml`:

      ```yml
      - src: git+https://github.com/CMCuritiba/ansible-cmc-servers.git
        version: issue17
        name: CMCuritiba.IaC
      ```

      Instale com:

      ```bash
      ansible-galaxy install -r requirements.yml
      ```

1. Verifique se o(s) _host(s)_ estão no ar:

   ```bash
   ansible -m ping -u root dhcp
   ansible -m ping all
   ```

1. Testando um _playbook_ (_dry run_):

   ```bash
   ansible-playbook -u root playbook.yml --check --diff
   ansible-playbook -u root playbook.yml --check
   ```

1. Aplicando um _playbook_:

   ```bash
   ansible-playbook -K playbook.yml
   ansible-playbook -u nome.sobrenome -K playbook.yml
   ansible-playbook -u root playbook.yml
   ```
