ansible-cmc-servers
===================

Role para configurar servidores debian para o ambiente produtivo da CMC.

Serviços/pacotes inclusos:
1. sudo
1. NTP
1. exim4 (MTA)
1. unattended-upgrades
1. rsync

Requirements
------------

Nenhum.
<!-- Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required. -->

Role Variables
--------------

Descrição das variáveis que devem ser passadas para esta role.

Obrigatórias:
- `cmc_server_hostname`: nome do servidor (sem o domínio).

Opcionais:
- `ntp_server1`: Primeiro servidor NTP
- `ntp_server2`: Segundo servidor NTP
<!-- A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. -->

Dependencies
------------

Roles:
- [ontic.exim](https://galaxy.ansible.com/ontic/exim)
<!-- A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles. -->

Example Playbook
----------------

<!-- Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: -->
Exemplo de playbook:

```yaml
---
- hosts: servidores
  roles:
    - role: ansible-cmc-servers
      cmc_server_hostname: tauari
```

License
-------

BSD

Author Information
------------------

[Divisão de Arquitetura de Serviços](mailto:admin@cmc.pr.gov.br)

[Câmara Municipal de Curitiba](https://cmc.pr.gov.br)
<!-- An optional section for the role authors to include contact information, or a website (HTML is not allowed). -->
