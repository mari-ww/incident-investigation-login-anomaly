# 🧾 Relatório Técnico: Incidente em Host Windows

📅 **Data simulada**: 2025-04-21  
👤 **Analista**: Mari WW

---

## 🧠 Resumo Técnico

Foi identificada uma série de atividades anômalas em um host Windows, incluindo login suspeito, manipulação de arquivos do sistema, shell remota e extração de credenciais. Todas as evidências indicam comprometimento por ameaça persistente controlando o host.

---

## 🚨 Alerta Inicial

SIEM detectou login fora do horário usual, seguido por modificações em arquivos sensíveis (`hosts`) e abertura de porta não usual (`1337`).

---

## 🔍 Evidências Coletadas

### 1. Login Anômalo
- Log indica login fora do horário padrão
- Usuário aparentemente legítimo
- Indica uso de credencial comprometida

📷 `images/login-log.png`

---

### 2. Extração de Senhas com Mimikatz
- Ferramenta flagrada em execução
- Dump de senhas presente na memória

📷 `images/mimikatz.png`

---

### 3. Shell Remota via JSP
- Arquivo `.jsp` presente em `C:\inetpub\wwwroot`
- Tipo de shell comumente usado em ataques web

📷 `images/jsp-file.png`

---

### 4. Porta Aberta via Regra Suspeita
- Regra: “Allow outside connections for development”
- Porta aberta: `1337`

📷 `images/firewall-rule.png`

---

### 5. DNS Spoofing
- `hosts` aponta google.com → IP malicioso
- Técnica usada para camuflar C2

📷 `images/hosts-file.png`

---

## ⚔️ Análise

🛑 **Comportamento malicioso confirmado**  
O conjunto de ações indica comprometimento total da máquina. O invasor teve persistência e controle remoto do host.

---

## 🧬 TTPs MITRE ATT&CK

| Técnica | Descrição | ID |
|--------|-----------|----|
| 🧪 Credential Dumping | Uso do Mimikatz para obter senhas | [T1003](https://attack.mitre.org/techniques/T1003) |
| 🌐 Command and Control | Comunicação via IP spoofado no hosts | [T1071.001](https://attack.mitre.org/techniques/T1071/001) |
| 📁 File Deployment | JSP Webshell instalada | [T1059.004](https://attack.mitre.org/techniques/T1059/004) |

---

## 🛡️ Ações Sugeridas

- Reset de todas as senhas do host
- Isolamento da máquina na rede
- Reinstalação limpa ou restauração de backup
- Reforço de regras de firewall
- Alerta ao time de segurança e usuários impactados

---

## ✅ Conclusão

🟥 **Incidente confirmado.**  
➡️ Origem: **Credencial comprometida + persistência via webshell.**

📌 Recomendado ativar monitoramento contínuo de alterações no `hosts`, uso de ferramentas como Mimikatz e portas abertas dinamicamente.

