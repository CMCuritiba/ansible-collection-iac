# Ansible Collection - CMCuritiba.IaC

Coleção de roles para configurar servidores debian para o ambiente produtivo da CMC.

## Roles

### servers

Configura servidores com pacotes básicos.

Serviços inclusos:

1. NTP
1. exim4 (MTA)
1. unattended-upgrades
1. rsync
1. ufw (permite inicialmente apenas SSH da rede DTIC)  

### aaa

Configura AAA.

Serviços inclusos:

1. AAA (LDAP + sudo + acct)

## Example Playbook

<!-- Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: -->

Exemplo de playbook:

```yaml
---
- hosts: servidores
  roles:
    - role: ansible-cmc-servers
      cmc_dtic_network: 192.168.0.0/24
      cmc_dtic_vpn_network: 192.168.1.0/24
      cmc_template_ip: '^192\.168\.0\.1'
      cmc_ntp_servers:
        - 192.168.0.4
        - a.ntp.br
      cmc_ldap_bindpw: senha
      cmc_install_docker: true
```

## References

- [Migrating Roles to Roles in Collections on Galaxy](https://docs.ansible.com/ansible/latest/dev_guide/migrating_roles.html)

## License

GPL-3.0-or-later

## Author Information

[Divisão de Arquitetura de Serviços](mailto:arquitetura-ti@cmc.pr.gov.br)

[Câmara Municipal de Curitiba](https://cmc.pr.gov.br)

<!-- An optional section for the role authors to include contact information, or a website (HTML is not allowed). -->
