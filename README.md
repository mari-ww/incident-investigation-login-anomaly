# 🕵️‍♀️ Investigação de Incidente - Login Anômalo e Persistência

Este projeto simula uma investigação real de incidente usando um ambiente forense Windows (TryHackMe - Investigating Windows). A análise foca na identificação de comportamento malicioso, persistência, técnicas de acesso remoto e desvio de DNS.

🔎 **Objetivo:** Simular uma investigação de SOC após atividade suspeita, validando TTPs e IoCs usados por atacantes.

📅 **Situação:** Um login em horário incomum foi detectado. A partir disso, realizamos uma investigação completa no sistema.

---

## 📸 Evidências Coletadas

As imagens estão na pasta `images/`, cada uma com legenda explicando sua relevância.

| Evidência                      | Descrição                                                                 |
|-------------------------------|---------------------------------------------------------------------------|
| `login-log.png`               | Logon bem-sucedido fora do horário padrão (Event ID 4624)                 |
| `mimikatz.png`                | Execução do Mimikatz para extração de credenciais da memória             |
| `jsp-file.png`                | Webshells `.jsp` no servidor IIS (ponto de persistência)                 |
| `firewall-rule.png`           | Regra de firewall criada manualmente, liberando porta 1337               |
| `hosts-file.png`              | Arquivo hosts adulterado redirecionando `google.com` para IP interno     |
| `ping-google.png` (extra)     | Ping mostra IP falso, confirmando falsificação de DNS local              |

---

## 🧠 Análise Técnica

### 🔍 Indicadores observados
- Login suspeito em horário incomum
- Execução de ferramenta de credential dumping (`mimikatz`)
- Criação de shell remota (`.jsp`) no servidor web
- Liberação de porta não padrão (1337)
- Modificação local do DNS via arquivo `hosts`

### ⚙️ Técnicas MITRE ATT&CK

| Tática                    | Técnica                                                   |
|--------------------------|------------------------------------------------------------|
| Initial Access           | `T1190` - Exploit Public-Facing Application                |
| Credential Access        | `T1003.001` - LSASS Memory (Mimikatz)                      |
| Persistence              | `T1505.003` - Web Shell                                    |
| Defense Evasion          | `T1036` - Masquerading                                     |
| Command and Control      | `T1071.001` - Web Protocols / `T1071.004` - DNS            |
| Execution                | `T1059` - Command and Scripting Interpreter                |

---

## 🧰 Relatório Técnico

👉 O relatório completo da investigação está em [`report.md`](report.md)

📝 Inclui:
- Linha do tempo do ataque
- Análise de cada evidência
- Técnicas utilizadas
- Recomendação de resposta

---

## 🧬 Conclusão

Este projeto demonstra:
✅ Capacidade de correlacionar evidências  
✅ Reconhecimento de atividades fora do comportamento normal  
✅ Uso de TTPs reais com base em MITRE ATT&CK  
✅ Análise forense prática e simulação de ambiente SOC realista

---

## 🗂️ Estrutura do Projeto

```bash
├── images/                      # Prints das evidências
├── report.md                    # Relatório técnico (Markdown)
├── relatorio_final.pdf          # (Opcional, versão bonita em PDF)
├── README.md                    # Apresentação do projeto estilo
```
