# Ansible Collection - cmcuritiba.iac

Coleção de roles para configurar servidores debian para o ambiente produtivo da CMC.

Este é um trabalho em curso.

## Requisitos

- Ansible 2.10.3 ou maior
- Python 3.8.5 ou maior

## Roles

- [AAA](roles/aaa/README.md)
- [servers](roles/servers/README.md)

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
        - name: https://github.com/CMCuritiba/ansible-cmc-servers.git
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

1. Atualize _playbooks_ existentes para funcionar com a coleção:
   1. Renomeie todas as referencias à _role_ original nos _playbooks_ para iniciar com cmcuritiba.iac;
   1. Remova todas as referencias a `cmc_server_hostname`. `cmc_server_hostname` foi substituída com a variável especial do ansible `inventory_hostname_short`;
   1. Revise as variáveis obrigatórias e opcionais, em especial para LDAP e SMTP.
1. Miscelânea
   1. Please submit a pull request on so we can merge your roles into the collection.
