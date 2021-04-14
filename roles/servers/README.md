# Servers

Role para configurar servidores debian para o ambiente produtivo da CMC.

Serviços inclusos:

1. AAA (LDAP + sudo + acct)
1. NTP
1. exim4 (MTA)
1. unattended-upgrades
1. rsync
1. ufw (permite inicialmente apenas SSH da rede DTIC)  
   **OBS**: aparentemente não é necessário liberar as portas dos serviços
   disponibilizados em containers, o docker já gerencia as portas via
   `iptables`.

## Requirements

<!-- Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required. -->

Nenhum.

## Role Variables

<!-- A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. -->

Descrição das variáveis que devem ser passadas para esta role.

Obrigatórias:

- `cmc_dtic_network`: faixa de rede da DTIC (IPv4 address block)
- `cmc_ntp_servers`: lista de servidores NTP (lista de FQDNs e endereços IPv4)

Opcionais:

- `cmc_install_docker`: `boolean` indicando se o docker deve ser instalado, o _default_ é `false`
- `cmc_enable_ssh_agent`: `boolean` indicando se o _agent forwarding_ deve ser habilitado, o _default_ é `false`
- `cmc_dtic_vpn_network`: faixa de rede de acesso VPN da DTIC (IPv4 address block)
- `cmc_template_ip`: _regex_ com o IP de template dos servidores
- `cmc_smtp_server`: servidor SMTP (FQDN ou IPv4). **Importante**: se o servidor SMTP não for informado o envio de e-mails não será configurado.
- `cmc_ldap_server`: servidor LDAP (hostname, FQDN ou IPv4). **Importante**: se o servidor LDAP não for informado a autenticação via LDAP não será configurado.  
  Caso o servidor LDAP seja informado, as seguinte variáveis adicionais serão necessárias:
  - `cmc_ldap_dn`: raiz da árvore de diretórios
  - `cmc_ldap_binddn`: usuário para bind no LDAP
  - `cmc_ldap_bindpw`: senha para bind no LDAP (vide [_vault_](https://docs.ansible.com/ansible/latest/user_guide/vault.html))

## Dependencies

Roles:

<!-- A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles. -->

- [ontic.exim](https://galaxy.ansible.com/ontic/exim)

## Example Playbook

<!-- Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: -->

Exemplo de playbook:

```yaml
---
- hosts: foo-servers
  roles:
    - role: cmcuritiba.iac.servers
      cmc_dtic_network: 192.168.0.0/24
      cmc_dtic_vpn_network: 192.168.1.0/24
      cmc_template_ip: '^192\.168\.0\.1'
      cmc_smtp_server: "mx.example.com"
      cmc_ntp_servers:
        - 192.168.0.4
        - a.ntp.br
      cmc_ldap_server: "192.168.0.1"
      cmc_ldap_dn: "dc=example,dc=com"
      cmc_ldap_binddn: "binduser"
      cmc_ldap_bindpw: senha
      cmc_install_docker: true
```

## License

GPL-3.0-or-later

## Author Information

<!-- An optional section for the role authors to include contact information, or a website (HTML is not allowed). -->

[Divisão de Arquitetura de Serviços](mailto:arquitetura-ti@cmc.pr.gov.br)

[Câmara Municipal de Curitiba](https://cmc.pr.gov.br)
