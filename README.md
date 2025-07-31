```markdown
# Backup Automático de Configurações Cisco com Ansible

Este projeto realiza o **backup automático** das configurações de switches Cisco utilizando o **Ansible** e salvando os arquivos em um servidor **TFTP**.

## 📌 Funcionalidades
- Testa a conectividade SSH antes de iniciar o backup.
- Gera arquivos com data e hora no formato `SW-HOSTNAME-AAAAMMDD-HHMM.txt`.
- Suporte a execução com ou sem VRF `management`.
- Salva backups diretamente no servidor TFTP especificado.

## ⚙️ Pré-requisitos
1. **Ansible** instalado no controlador.
2. Servidor **TFTP** acessível pelos switches.
3. Acesso SSH aos switches Cisco.

## 📂 Estrutura do Projeto

├── playbook.yml         # Playbook principal          
└── roles/
    └── network_backup_switches_cisco/
        └── tasks/
            └── main.yml
        └── vars/
            └── main.yml      # Variáveis sensíveis 

## 🔹 Configuração
Edite o arquivo **`vars/main.yml`** antes de executar:

```yaml
ftp_server_ip: "XXX.XXX.XXX.XXX"    # IP do servidor TFTP
ssh_username: "USUARIO_SSH"         # Usuário SSH
ssh_password: "SENHA_SSH"           # Senha SSH
```

No inventário do Ansible, adicione seus switches:

```ini
[cisco_switches]
10.10.10.1
10.10.10.2
```

## ▶️ Execução
Para rodar o playbook:
```bash
ansible-playbook -i inventario.ini playbook.yml
```

## 🛡️ Segurança
- **Nunca** versione `vars.yml` com senhas reais no GitHub.
- Use **Ansible Vault** para criptografar credenciais:
```bash
ansible-vault encrypt vars.yml
```
