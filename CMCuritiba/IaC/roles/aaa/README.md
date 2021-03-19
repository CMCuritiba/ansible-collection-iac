# AAA

Role para configurar AAA em servidores debian para o ambiente produtivo da CMC.

Serviços inclusos:

1. AAA (LDAP + sudo + acct)

## Requirements

<!-- Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required. -->

Nenhum.

## Role Variables

<!-- A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. -->

Descrição das variáveis que devem ser passadas para esta role.

Obrigatórias:

- `cmc_aaa_ldap_bindpw`: senha para bind no LDAP (vide [_vault_](https://docs.ansible.com/ansible/latest/user_guide/vault.html))
- `cmc_aaa_ldap_server`: servidor LDAP (hostname, FQDN ou IPv4)
- `cmc_aaa_ldap_dn`: raiz da árvore de diretórios
- `cmc_aaa_ldap_binddn`: usuário para bind no LDAP

Opcionais:

Nenhuma.

## Dependencies

Roles:

<!-- A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles. -->

- [nss-pam-ldap-configure](https://galaxy.ansible.com/andrewrothstein/nss-pam-ldap-configure)

## Example Playbook

<!-- Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: -->

Exemplo de playbook:

```yaml
---
- hosts: foo-servers
  roles:
    - role: CMCuritiba.IaC.aaa
      cmc_aaa_ldap_bindpw: mypassword
      cmc_aaa_ldap_server: "192.168.0.1"
      cmc_aaa_ldap_dn: "dc=example,dc=com"
      cmc_aaa_ldap_binddn: "binduser"
```

## License

GPL-3.0-or-later

## Author Information

[Divisão de Arquitetura de Serviços](mailto:arquitetura-ti@cmc.pr.gov.br)

[Câmara Municipal de Curitiba](https://cmc.pr.gov.br)

<!-- An optional section for the role authors to include contact information, or a website (HTML is not allowed). -->
