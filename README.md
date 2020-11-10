# ansible-cmc-servers

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

1. Ter o `ansible_host` definido no arquivo de inventário:

   ```ini
   [server1_group]
   server1 ansible_host=111.222.333.444
   ```

<!-- Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required. -->

## Role Variables

Descrição das variáveis que devem ser passadas para esta role.

Obrigatórias:

- `cmc_server_hostname`: nome do servidor (sem o domínio)
- `cmc_dtic_network`: faixa de rede da DTIC (IPv4 address block)
- `cmc_ntp_servers`: lista de servidores NTP (lista de FQDNs e endereços IPv4)
- `cmc_ldap_server`: servidor LDAP (hostname, FQDN ou IPv4)
- `cmc_ldap_binddn`: usuário para bind no LDAP
- `cmc_ldap_bindpw`: senha para bind no LDAP (vide [_vault_](https://docs.ansible.com/ansible/latest/user_guide/vault.html))

Opcionais:

- `cmc_dtic_vpn_network`: faixa de rede de acesso VPN da DTIC (IPv4 address block)
- `cmc_template_ip`: _regex_ com o IP de template dos servidores
- `cmc_install_docker`: `boolean` indicando se o docker deve ser instalado. O _default_ é `false`.

<!-- A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well. -->

## Dependencies

Roles:

- [ontic.exim](https://galaxy.ansible.com/ontic/exim)
- [nss-pam-ldap-configure](https://galaxy.ansible.com/andrewrothstein/nss-pam-ldap-configure)

<!-- A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles. -->

## Example Playbook

<!-- Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: -->

Exemplo de playbook:

```yaml
---
- hosts: servidores
  roles:
    - role: ansible-cmc-servers
      cmc_server_hostname: foo-server
      cmc_dtic_network: 192.168.0.0/24
      cmc_dtic_vpn_network: 192.168.1.0/24
      cmc_template_ip: '^192\.168\.0\.1'
      cmc_ntp_servers:
        - 192.168.0.4
        - a.ntp.br
      cmc_ldap_bindpw: senha
      cmc_install_docker: true
```

## License

BSD

## Author Information

[Divisão de Arquitetura de Serviços](mailto:arquitetura-ti@cmc.pr.gov.br)

[Câmara Municipal de Curitiba](https://cmc.pr.gov.br)

<!-- An optional section for the role authors to include contact information, or a website (HTML is not allowed). -->
