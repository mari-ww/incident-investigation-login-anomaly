# 🕵️‍♀️ Investigação de Incidente: Windows - Credencial Comprometida

🔍 Projeto simula a investigação de um possível ataque a um host Windows, com login anômalo, extração de credenciais e uso de shell remota.

## ⚠️ Contexto do Alerta

Durante monitoramento de atividades suspeitas em um host Windows, foi detectado um login fora do horário padrão e regras de firewall alteradas.

## 🧪 O que foi investigado

- Logs de login suspeito
- Extração de senhas com Mimikatz
- Shell remota com extensão `.jsp`
- Regra de firewall abrindo a porta `1337`
- DNS spoofing apontando `google.com` para IP externo

## 🖼️ Evidências

### 🔑 Extração de senhas com Mimikatz
![mimikatz](images/mimikatz.png)
> Ferramenta usada pelo invasor para capturar credenciais do sistema.

### 🌐 IP suspeito no arquivo `hosts`
![hosts-file](images/hosts-file.png)
> O domínio google.com foi redirecionado para um IP malicioso (C2).

### 💻 Shell `.jsp` no servidor web
![jsp-shell](images/jsp-file.png)
> Arquivos JSP indicam possível webshell implantada no servidor.

### 🔥 Regra de firewall abrindo a porta 1337
![firewall-rule](images/firewall-rule.png)
> Regra "Allow outside connections for development" permite acesso remoto.

## 🛠️ Ferramentas usadas

- 🧪 TryHackMe - Lab Investigating Windows
- 🔎 Windows Event Viewer
- 🔥 Windows Firewall
- 📁 Explorer + Hosts File
- 🌐 Ping/Terminal

## ✅ Conclusão

🟥 Incidente confirmado: shell remota instalada + credenciais comprometidas.

🔗 Relatório técnico completo em: [`report.md`](./report.md)
