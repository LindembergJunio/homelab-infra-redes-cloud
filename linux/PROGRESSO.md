## Sessão 1 — Preparação da VM Ubuntu Server

**Data:** 20/11/2026

**Assuntos estudados:** Ubuntu Server LTS, dimensionamento da VM, redes NAT e interna no VirtualBox, interfaces de rede no Linux, IPv6 link-local (visão geral).

**Comandos utilizados:**
- `hostnamectl`: identifica o sistema, kernel e tipo de virtualização.
- `ip -br a`: lista interfaces e IPs (resumido).
- `ip -br link`: lista interfaces e MACs, mesmo sem IP.
- `df -h /`: mostra uso do disco da partição raiz.
- `sudo poweroff`: desliga o sistema de forma limpa.

**Atividades concluídas:**
- Ubuntu Server 26.04.1 LTS instalado (20 GB, 2 adaptadores).
- Evidências coletadas: versão do sistema, disco (20 GB, 21% usado) e interfaces `enp0s3` (NAT, 10.0.2.15/24) e `enp0s8` (LAB-CORE, sem IPv4).
- Troubleshooting: Adaptador 2 estava desabilitado no VirtualBox. Diagnóstico por camadas: `ip -br link` mostrou só 1 interface, logo o defeito estava abaixo do SO.
- Snapshots: `instalacao-limpa` (1 adaptador) e `instalacao-limpa-2-adaptadores`.

**Dificuldades:** conversão de MAC em IPv6 EUI-64 (inversão do 7º bit). Compreendi a divisão do MAC e a inserção de `ff:fe`; o passo da inversão ficou pendente. Decidi pular essa etapa por enquanto.

**Próxima atividade:** Fase 1, navegação no sistema de arquivos (`pwd`, `ls`, `cd`) e estrutura de diretórios do Linux.
