# 🛡️ Incident Report — Login Anomaly & Credential Dump

## 📅 Timeline do Incidente

| Data/Hora            | Evento                                                                 |
|----------------------|------------------------------------------------------------------------|
| 03/02/2019 16:04     | Login anômalo detectado (Event ID 4624)                                |
| --                   | Execução da ferramenta Mimikatz                                        |
| --                   | Upload de arquivos .jsp suspeitos no servidor web                     |
| --                   | Criação de regra de firewall liberando porta externa (1337)            |
| --                   | Manipulação do arquivo `hosts` para redirecionar tráfego DNS           |

---

## 🔍 Evidências Coletadas

### 📌 1. Login Anômalo

🖼️ **`images/login-log.png`**  
🕵️ *Logon bem-sucedido em horário fora do padrão, indicando possível uso indevido de credencial legítima.*

🗂️ **Fonte**: Event Viewer → Windows Logs → Security  
🔢 **Event ID**: 4624  
🕒 **Horário**: 03/02/2019 16:04:47

---

### 📌 2. Execução do Mimikatz

🖼️ **`images/mimikatz.png`**  
🕵️ *Ferramenta de credential dumping (Mimikatz) flagrada em execução, com extração de senhas da memória.*

---

### 📌 3. Webshell JSP

🖼️ **`images/jsp-file.png`**  
🕵️ *Presença de arquivos `.jsp` em diretório de servidor web indica possível webshell para acesso remoto.*

📁 Local: `C:\inetpub\wwwroot\`  
🧩 Arquivos suspeitos: `shell.jsp`, `reverse.jsp`, `img.gif`

---

### 📌 4. Regra de Firewall Suspeita

🖼️ **`images/firewall-rule.png`**  
🕵️ *Regra personalizada libera porta 1337 para conexões externas — potencial canal de comando e controle (C2).*

---

### 📌 5. Arquivo hosts adulterado

🖼️ **`images/hosts-file.png`**  
🕵️ *Redirecionamento DNS no arquivo hosts, alterando google.com para um IP interno malicioso (spoofing DNS).*

🧠 IP falso: `76.32.97.132`

---

### 📌 6. Confirmação via ping

🖼️ **`images/ping-google.png`**  
🕵️ *Resultado do comando `ping google.com` mostra IP falso, confirmando adulteração local no DNS.*

---

## 🧬 Técnicas MITRE ATT&CK (Mapping)

| Fase             | Técnica                            | ID         | Descrição                                                      |
|------------------|-------------------------------------|------------|----------------------------------------------------------------|
| Acesso Inicial   | Valid Accounts                     | T1078      | Uso de credenciais legítimas para acessar o sistema            |
| Execução         | Command and Scripting Interpreter  | T1059.001  | Execução de comandos via linha de comando                      |
| Credential Access| Credential Dumping (Mimikatz)      | T1003.001  | Extração de senhas da memória                                  |
| Persistência     | Web Shell                          | T1505.003  | Webshell JSP no diretório wwwroot                              |
| Defesa Evasão    | Modify System Configuration        | T1562.001  | Manipulação do arquivo `hosts`                                 |
| Comunicação C2   | Non-Standard Port                  | T1571      | Porta 1337 liberada no firewall para C2 externo                |

---

## 🧠 Análise

- **Login** fora do horário padrão pode indicar **uso indevido de credenciais válidas**.
- Uso do **Mimikatz** confirma foco em **movimentação lateral e persistência**.
- Presença de **webshell** mostra tentativa clara de **controle remoto contínuo**.
- Manipulação do **arquivo hosts** mostra **técnica de DNS spoofing local**.
- Liberação da **porta 1337** sugere **canal alternativo de C2**.

---

## 🔐 Recomendações

- 🚫 **Revogar credenciais** utilizadas no login anômalo
- 🔎 Realizar **varredura completa** por artefatos maliciosos
- 🛑 Bloquear o IP malicioso `76.32.97.132` no firewall
- 📋 Auditar outras máquinas para **mecanismos de persistência**
- 📁 Restaurar configurações do arquivo `hosts`
- 📬 Configurar alerta para alterações de regras de firewall

---

📌 *Este relatório foi gerado como parte de simulação investigativa no laboratório “Investigating Windows” (TryHackMe).*
