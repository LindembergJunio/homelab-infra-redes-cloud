# ROADMAP v2.0 — Homelab: Infraestrutura, Redes e Cloud

> **Filosofia central:** Aprenda fazendo na mão. Quebre. Conserte. Entenda. Só depois automatize.
> O laboratório nunca é reiniciado — ele apenas cresce.

---

## Trilha de evolução

```
Suporte N3 (ERP)
    ↓
Virtualização (VirtualBox → Proxmox)
    ↓
Redes (switching, VLANs, RouterOS, firewall)
    ↓
Linux (administração, serviços, hardening)
    ↓
Docker + Serviços de Infraestrutura
    ↓
Monitoramento + PostgreSQL
    ↓
Automação (Ansible → Terraform)
    ↓
Cloud (AWS/Azure — hybrid)
    ↓
Kubernetes
    ↓
Projeto Final (infraestrutura corporativa completa)
```

---

## Mapa de fases

| # | Fase | Tecnologias | Status |
|---|---|---|---|
| 00 | Virtualização base | VirtualBox, redes virtuais, snapshots | ✅ Concluída |
| 01 | Fundamentos de redes | OSI, TCP/IP, subnetting, Wireshark | ✅ Concluída |
| 02 | Switching e VLANs | Open vSwitch, 802.1Q, segmentação L2 | 🔄 Em andamento |
| 03 | RouterOS (MikroTik) | CHR, VLANs, roteamento, firewall básico | ⏳ Pendente |
| 04 | Linux administração | Debian/Ubuntu, SSH, systemd, permissões, logs | ⏳ Pendente |
| 05 | Serviços de infraestrutura | DHCP, DNS (BIND9), NTP, Nginx, proxy reverso | ⏳ Pendente |
| 06 | Docker | Containers, imagens, volumes, redes, compose | ⏳ Pendente |
| 07 | Monitoramento | Zabbix, Prometheus, Grafana, syslog, alertas | ⏳ Pendente |
| 08 | PostgreSQL | Instalação, backup/restore, replicação, monitoramento | ⏳ Pendente |
| 09 | Proxmox VE | Hypervisor tipo 1, templates, backup, migração | ⏳ Pendente |
| 10 | Windows Server + AD | Active Directory, GPO, DNS, RDS (complementar) | ⏳ Pendente |
| 11 | Ansible | Playbooks, roles, vault, idempotência | ⏳ Pendente |
| 12 | Firewall e VPN | pfSense/OPNsense, OpenVPN, IPsec, Suricata | ⏳ Pendente |
| 13 | Terraform | IaC, providers, state, módulos | ⏳ Pendente |
| 14 | Cloud (AWS/Azure) | VPC, EC2, IAM, hybrid VPN, CloudWatch | ⏳ Pendente |
| 15 | Kubernetes | Pods, deployments, services, ingress, Helm | ⏳ Pendente |
| 16 | Projeto Final | Infraestrutura corporativa completa integrada | ⏳ Pendente |

---

## Por que essa ordem?

### VirtualBox antes de Proxmox
VirtualBox é mais simples e roda no seu Windows atual sem dedicar hardware. Você aprende os conceitos de virtualização sem precisar de uma máquina dedicada. Proxmox entra na Fase 09, quando você já sabe o que está fazendo e pode aproveitá-lo como plataforma real de produção do lab.

### Redes antes de Linux
Você precisa entender como os hosts se comunicam antes de administrar os hosts em si. Quando chegar no Linux, já vai saber por que está configurando IP, rota e firewall — não vai ser decoreba.

### RouterOS na Fase 03
Depois de entender VLANs no nível do sistema operacional (OVS), você vai para o RouterOS e vê os mesmos conceitos numa CLI de equipamento real de mercado. A sequência é: conceito → implementação em SO → implementação em equipamento.

### Linux (Fase 04) antes de Windows Server (Fase 10)
Linux é o sistema dominante em servidores, cloud e containers. Windows Server é importante como conhecimento complementar para ambientes corporativos brasileiros, mas não é a base — é o complemento. Inverter essa prioridade em relação ao plano original foi a mudança mais significativa desta v2.0.

### Docker (Fase 06) antes de Kubernetes (Fase 15)
Kubernetes orquestra containers Docker. Tentar entender Kubernetes sem dominar Docker é como tentar administrar um cluster de servidores sem saber administrar um servidor individual. A distância entre as fases é intencional.

### Automação (Ansible/Terraform) depois de tudo manual
Você precisa saber fazer na mão antes de automatizar. Se você automatizar algo que não entende, vai ter um script que funciona mas que você não sabe depurar quando quebrar. A automação é a recompensa de quem dominou o manual.

### Cloud depois de infraestrutura local sólida
Cloud é infraestrutura remota. Se você não entende infraestrutura local (rede, firewall, servidor, banco, monitoramento), vai usar cloud como "aluguel de máquina virtual cara" em vez de entender o que está fazendo. A base local torna o aprendizado de cloud muito mais rápido e profundo.

---

## Topologia final do laboratório

```
                    [Internet]
                         |
              ┌──────────────────────┐
              │  FW01 — pfSense      │  Firewall/Router de borda
              │  WAN: NAT VirtualBox │
              │  LAN: 10.0.0.1/24    │
              └──────────┬───────────┘
                         |
           VirtualBox Internal Network "LAB-CORE"
                         |
     ┌──────────┬─────────┴──────────┬──────────────┐
     │          │                    │              │
┌────┴───┐ ┌───┴────┐ ┌─────────────┴──┐ ┌────────┴───────┐
│ROUTEROS│ │LINUX   │ │   MON01         │ │   PG-DB01      │
│  CHR   │ │SRV01   │ │ Zabbix/Grafana  │ │  PostgreSQL    │
│MikroTik│ │Debian  │ │                 │ │                │
│10.0.0.2│ │10.0.0.3│ │   10.0.0.30     │ │   10.0.0.40    │
└────────┘ └────────┘ └─────────────────┘ └────────────────┘
     │
┌────┴───────────────────────────────────────────────────┐
│  PROXMOX01 (Fase 09 em diante)                          │
│  Hypervisor que substitui/complementa o VirtualBox      │
│  Hospeda VMs adicionais internamente                    │
└─────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│  AWS/Azure (Fase 14)                                    │
│  VPC conectada ao lab via Site-to-Site VPN              │
└─────────────────────────────────────────────────────────┘
```

---

## Estrutura do repositório

```
homelab-infra-redes-cloud/
├── README.md                        ← Capa: narrativa, diagrama, índice
├── ROADMAP.md                       ← Este arquivo
├── COMO_ESTUDAR.md                  ← Filosofia, rotina, dicas de estudo
├── docs/
│   ├── 00-virtualizacao/
│   ├── 01-fundamentos-redes/
│   ├── 02-switching-vlans/
│   ├── 03-routeros/
│   ├── 04-linux/
│   ├── 05-servicos-infra/
│   ├── 06-docker/
│   ├── 07-monitoramento/
│   ├── 08-postgresql/
│   ├── 09-proxmox/
│   ├── 10-windows-server/
│   ├── 11-ansible/
│   ├── 12-firewall-vpn/
│   ├── 13-terraform/
│   ├── 14-cloud/
│   ├── 15-kubernetes/
│   └── 16-projeto-final/
├── diagrams/                        ← Arquivos draw.io + exports PNG
├── ansible/                         ← Playbooks e roles (Fase 11+)
├── terraform/                       ← Módulos e configs (Fase 13+)
├── docker/                          ← Dockerfiles e compose (Fase 06+)
├── scripts/                         ← Scripts auxiliares bash/python
└── incident-reports/                ← Troubleshooting documentado
```

---

## Padrão de documentação por fase

Cada fase dentro de `docs/` deve seguir esta estrutura no README:

```markdown
# Fase XX — Nome da Fase

## Objetivo
Por que estou estudando isso. Onde aparece no mercado. Como será usado nas próximas fases.

## Competências ao concluir
O que sou capaz de fazer após esta fase (verbos de ação: configurar, diagnosticar, implementar...).

## Teoria necessária
Apenas o mínimo necessário — não um livro.

## Ambiente desta fase
VMs adicionadas, IPs, topologia atualizada.

## Projeto prático
O que foi construído, passo a passo relevante, decisões tomadas.

## Cenário real
Empresa fictícia onde esse conhecimento seria aplicado.

## Problemas encontrados
Formato: Sintoma → Investigação → Causa raiz → Solução → Prevenção.

## Exercícios de troubleshooting
Problemas simulados, raciocínio de diagnóstico.

## Perguntas de entrevista
O que um recrutador técnico poderia perguntar sobre este tema.

## Checklist de conclusão
- [ ] Item 1
- [ ] Item 2

## Critério de conclusão
Como saber que realmente concluí esta fase (não "li sobre", mas "fiz e funciona").
```

---

## Padrão de incident report

Sempre que resolver um problema real durante o lab, documente em `incident-reports/`:

```markdown
# Incident: [título curto e descritivo]
**Data:** DD/MM/AAAA
**Fase:** XX
**Ambiente:** [VM/serviço afetado]
**Severidade:** Baixa / Média / Alta

## Sintoma
O que foi observado. Como o problema se manifestou.

## Investigação
Passos seguidos. Comandos usados. Hipóteses testadas e descartadas.

## Causa raiz
O que de fato causou o problema.

## Solução
O que foi feito para resolver.

## Prevenção
O que mudou para não repetir. O que foi aprendido.
```

---

## Trilha de evolução profissional

```
Suporte N3 ERP (hoje)
│   Você já tem: troubleshooting estruturado, PostgreSQL básico,
│   Windows, certificados digitais, TSPlus/RDP
│
↓ Fases 00-03 (Virtualização + Redes + RouterOS)
│
Infraestrutura Jr.
│   Adiciona: redes, switching, VLANs, firewall básico, MikroTik
│   Vagas: Analista de Suporte Infraestrutura, NOC Jr.
│
↓ Fases 04-05 (Linux + Serviços)
│
Analista de Infraestrutura
│   Adiciona: Linux server, DHCP/DNS/NTP, web server, proxy
│   Vagas: Analista de Infraestrutura Jr./Pleno
│
↓ Fases 06-09 (Docker + Monitoramento + PostgreSQL + Proxmox)
│
Analista de Infraestrutura Pleno
│   Adiciona: containers, observabilidade, banco em infra, hypervisor enterprise
│   Vagas: Analista de Infraestrutura Pleno, SysAdmin
│
↓ Fases 10-13 (Windows + Ansible + Firewall/VPN + Terraform)
│
Analista de Redes / Cloud Support
│   Adiciona: AD, automação, IaC, VPN, segurança de perímetro
│   Vagas: Analista de Redes, Cloud Support, SRE Jr.
│
↓ Fases 14-16 (Cloud + Kubernetes + Projeto Final)
│
Cloud Engineer / DevOps Jr.
    Adiciona: AWS/Azure, orquestração de containers, projeto integrado
    Vagas: Cloud Engineer, DevOps Jr., Platform Engineer Jr.
```

---

## Como usar este roadmap no dia a dia

1. **Consulte o mapa de fases** para saber onde está e para onde vai
2. **Siga a ordem** — cada fase prepara a próxima deliberadamente
3. **Documente enquanto faz**, não depois — a documentação é parte do aprendizado
4. **Quebre coisas de propósito** — os exercícios de troubleshooting são obrigatórios, não opcionais
5. **Só avance quando o checklist estiver completo** — "entendi a teoria" não conta, "funciona e eu sei por quê" conta
6. **Não pule para automação** enquanto não fizer manualmente com confiança

---

*Última atualização: Julho 2026 — v2.0*
*Status atual: Fase 02 em andamento*
