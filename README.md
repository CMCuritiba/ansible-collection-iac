# Ansible Collection - cmcuritiba.iac

Documentation for the collection.

This is still a work in progress.

## Requirements

- Ansible 2.10.3 or higher
- Python 3.8.5 or higher

## Guia do ameba

- Opcional: crie um virtual env python e ative-o para instalar o Ansible.

1. Instalar o Ansible na máquina controladora. Sugestão, de acordo com [esta documentação](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-with-pip):

   ```bash
   sudo apt install python-is-python3 python3-pip
   sudo pip3 install ansible
   ```

   Para atualizar o Ansible:

   ```bash
   sudo pip3 install --upgrade ansible
   ```

1. Garanta o acesso do controlador ao _host_ (por exemplo, compartilhando chaves entre o controlador e os _hosts_)
1. Instalar a _collection_ [cmcuritiba.iac](https://github.com/CMCuritiba/ansible-cmc-servers).
   As alternativas de instalação são:
   1. Faça o download do projeto como `.zip` e descompacte em `./collections/ansible_collections/` ou `~/.ansible/collections/ansible_collections/`
   1. Clone o projeto localmente em `./collections/ansible_collections/` ou `~/.ansible/collections/ansible_collections/`
   1. Utilizando o galaxy para baixar o código do repositório através de um `requirements.yml`:

      ```yml
      ---
      collections:
        - name: https://github.com/CMCuritiba/ansible-cmc-servers.git#CMCuritiba/IaC/
          type: git
          version: issue17
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

1. Update existing playbooks to work with collection:
   1. Rename all roles referenced inside playbooks to begin with cmcuritiba.iac.
   1. Remove all references to `cmc_server_hostname`. `cmc_server_hostname` was replaced with ansible's `inventory_hostname_short` special variable.
1. Miscellaneous
   1. Please submit a pull request on so we can merge your roles into the collection.
