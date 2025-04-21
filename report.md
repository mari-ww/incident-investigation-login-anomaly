# 🧾 Relatório Técnico de Incidente – Host Windows

📅 **Data Simulada:** 2025-04-21  
👤 **Analista Responsável:** Mari WW

---

## 🧠 Resumo Técnico

Durante uma verificação em ambiente Windows, foi identificado um login suspeito, seguido por execução de ferramentas de ataque conhecidas, manipulação de DNS, e possível instalação de shell remota.

---

## 🚨 Alerta Inicial

- **Fonte:** Monitoramento interno / TryHackMe Lab
- **Descrição:** Login fora do padrão com possível persistência pós-comprometimento

📷 `images/login-log.png`

---

## 🔍 Evidências Coletadas

### 1. Login Anômalo
📍 Local: Logs do Event Viewer  
🕒 Login em horário fora do normal  
👤 Usuário legítimo, sem justificativa plausível

📷 `images/login-log.png`

---

### 2. Execução de Mimikatz
📍 Local: Diretório temporário  
📄 Arquivo: `mimikatz.exe`  
⚠️ Dump de credenciais exibido em tela

📷 `images/mimikatz.png`

---

### 3. JSP Webshell
📍 Local: `C:\inetpub\wwwroot\`  
📄 Arquivo: `cmd.jsp`  
🛠 Acesso remoto via navegador

📷 `images/jsp-file.png`

---

### 4. Regra de Firewall Customizada
📍 Ferramenta: Painel de Firewall  
⚠️ Regra: “Allow outside connections for development”  
🛑 Porta aberta: 1337

📷 `images/firewall-rule.png`

---

### 5. DNS Spoofing via arquivo `hosts`
📍 Arquivo: `C:\Windows\System32\drivers\etc\hosts`  
➡️ google.com → IP 192.168.1.101  
🎯 Indício de comunicação com C2

📷 `images/hosts-file.png`

---

## 🧬 MITRE ATT&CK TTPs

| Tática                | Técnica                         | ID       |
|----------------------|----------------------------------|----------|
| Credential Access     | Credential Dumping (Mimikatz)    | [T1003](https://attack.mitre.org/techniques/T1003) |
| Command and Control   | Application Layer Protocol       | [T1071.001](https://attack.mitre.org/techniques/T1071/001) |
| Execution             | Command via Webshell (.jsp)      | [T1059.004](https://attack.mitre.org/techniques/T1059/004) |
| Defense Evasion       | Modify System Configuration      | [T1562.001](https://attack.mitre.org/techniques/T1562/001) |

---

## 🛡️ Ações Sugeridas

1. 🚫 Isolar máquina afetada imediatamente
2. 🔄 Resetar todas as credenciais do host
3. 🔍 Verificar logs de acesso remoto recentes
4. 🛠 Remover webshell e regra de firewall
5. 🧼 Reinstalação limpa recomendada
6. 🔔 Alerta ao time de resposta e ao usuário

---

## ✅ Conclusão

🟥 **Incidente Confirmado**

- Origem: Comprometimento de credencial
- Impacto: Controle remoto via webshell + extração de senhas
- Estado Atual: Host comprometido

🔁 Recomendado reforçar monitoramento de logs de login e uso de ferramentas como Mimikatz.
