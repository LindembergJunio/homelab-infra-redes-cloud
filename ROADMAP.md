# ROADMAP — Homelab: Infraestrutura, Redes e Cloud

> **Filosofia central:** Aprenda fazendo na mão. Quebre. Conserte. Entenda. Só depois automatize.
>
> O laboratório evolui conforme novos conhecimentos são adquiridos. Cada etapa aproveita o que foi construído anteriormente.

## Trilha de evolução

```text
Virtualização
    ↓
Fundamentos de Redes
    ↓
Switching, VLANs e Roteamento
    ↓
RouterOS (MikroTik)
    ↓
Linux e Serviços de Infraestrutura
    ↓
Docker e Monitoramento
    ↓
PostgreSQL e Virtualização de Servidores
    ↓
Windows Server e Administração de Ambientes
    ↓
Firewall, VPN e Segurança
    ↓
Automação (Ansible e Terraform)
    ↓
Cloud (AWS/Azure)
    ↓
Kubernetes (aprofundamento)
    ↓
Projeto Final
```

A sequência serve como orientação, não como regra rígida. Algumas tecnologias poderão ser estudadas em paralelo ou antecipadas conforme a necessidade dos projetos.

---

## Mapa de fases

| # | Fase | Principais conhecimentos | Status |
|---|---|---|---|
| 00 | Virtualização base | VirtualBox, máquinas virtuais, redes virtuais e snapshots | ✅ Concluída |
| 01 | Fundamentos de Redes | OSI, TCP/IP, IPv4, subnetting e Wireshark | ✅ Concluída |
| 02 | Switching e VLANs | Switching, VLANs, trunk 802.1Q, roteamento entre VLANs | 🔄 Em andamento |
| 03 | RouterOS (MikroTik) | CHR, VLANs, roteamento e firewall básico | ⏳ Pendente |
| 04 | Linux administração | Debian/Ubuntu, SSH, systemd, permissões e logs | ⏳ Pendente |
| 05 | Serviços de infraestrutura | DHCP, DNS, NTP, Nginx e proxy reverso | ⏳ Pendente |
| 06 | Docker | Containers, imagens, volumes, redes e Compose | ⏳ Pendente |
| 07 | Monitoramento | Zabbix, Prometheus, Grafana, syslog e alertas | ⏳ Pendente |
| 08 | PostgreSQL | Instalação, backup/restore, replicação e monitoramento | ⏳ Pendente |
| 09 | Proxmox VE | Virtualização, templates, armazenamento e backup | ⏳ Pendente |
| 10 | Windows Server | Active Directory, GPO, DNS e administração de domínio | ⏳ Pendente |
| 11 | Ansible | Playbooks, roles, inventários e idempotência | ⏳ Pendente |
| 12 | Firewall e VPN | pfSense/OPNsense, OpenVPN, IPsec e segurança de rede | ⏳ Pendente |
| 13 | Terraform | Infraestrutura como código, providers e state | ⏳ Pendente |
| 14 | Cloud (AWS/Azure) | VPC, EC2, IAM, redes e conectividade híbrida | ⏳ Pendente |
| 15 | Kubernetes | Pods, deployments, services, ingress e Helm | ⏳ Pendente |
| 16 | Projeto Final | Infraestrutura corporativa integrada | ⏳ Pendente |

---

## Direcionamento das etapas

### 00–01 — Fundamentos

Construir a base necessária para compreender virtualização, comunicação entre dispositivos, endereçamento IP e funcionamento das redes.

### 02–03 — Redes e roteamento

Aprofundar switching, VLANs, segmentação de redes, roteamento e configuração de equipamentos.

O aprendizado será realizado inicialmente com simuladores, como Packet Tracer, e posteriormente com MikroTik e outras tecnologias.

### 04–05 — Sistemas e serviços

Aprender administração Linux e implementar serviços comuns em ambientes corporativos, como DHCP, DNS, NTP e servidores web.

### 06–08 — Containers, monitoramento e banco de dados

Trabalhar com containers, monitoramento de infraestrutura e administração de PostgreSQL, incluindo backup, restauração e análise de desempenho.

### 09–10 — Virtualização e ambientes corporativos

Aprofundar virtualização com Proxmox e administração de ambientes Windows Server, incluindo Active Directory e políticas de grupo.

### 11–13 — Automação e segurança

Introduzir automação de tarefas, gerenciamento de configurações, infraestrutura como código, firewall e VPN.

A automação será estudada depois de compreender os processos manualmente.

### 14–15 — Cloud e orquestração

Aplicar os conhecimentos de redes, servidores, segurança e automação em ambientes AWS/Azure. Posteriormente, aprofundar Kubernetes conforme a necessidade e o direcionamento profissional.

### 16 — Projeto Final

Construir uma infraestrutura corporativa integrando os conhecimentos adquiridos ao longo do laboratório.

---

## Diretrizes de implementação

Algumas decisões orientam a evolução do laboratório:

- **VirtualBox antes de Proxmox:** começar com virtualização acessível e evoluir para uma plataforma dedicada.
- **Conceitos antes das ferramentas:** compreender redes, roteamento e serviços antes de automatizar configurações.
- **Linux como prioridade:** aprofundar administração Linux antes de avançar para serviços mais complexos.
- **Prática antes de automação:** realizar configurações manualmente antes de utilizar Ansible ou Terraform.
- **Infraestrutura local antes de Cloud:** compreender os fundamentos de redes, servidores e segurança antes de trabalhar com ambientes híbridos.
- **Evolução incremental:** aproveitar os projetos anteriores sempre que tecnicamente possível, sem impedir mudanças necessárias na arquitetura.

---

## Padrão de documentação dos projetos

Cada fase deverá ter uma documentação proporcional ao que foi desenvolvido.

Quando aplicável, registrar:

1. **Objetivo:** o que será aprendido e implementado.
2. **Ambiente:** ferramentas, máquinas virtuais, equipamentos e topologia.
3. **Implementação:** configurações e etapas relevantes.
4. **Testes:** comandos, resultados e validações.
5. **Troubleshooting:** problemas encontrados, investigação e soluções.
6. **Conclusão:** o que foi aprendido e o que ainda precisa ser aprofundado.

Não é necessário preencher todos os tópicos em projetos pequenos. O importante é registrar o que realmente foi realizado e permitir que outra pessoa compreenda a implementação.

---

## Registro de incidentes

Problemas relevantes encontrados durante os laboratórios poderão ser documentados separadamente em `incident-reports/`.

Modelo sugerido:

```markdown
# [Título do problema]

**Data:** DD/MM/AAAA
**Fase:** XX
**Ambiente:** [VM, serviço ou equipamento]

## Sintoma
O que aconteceu?

## Investigação
Quais testes foram realizados?
Quais hipóteses foram descartadas?

## Causa raiz
O que provocou o problema?

## Solução
Como foi resolvido?

## Aprendizado
O que foi aprendido e como evitar o problema?
```

---

## Critérios de conclusão

Uma fase não será considerada concluída apenas por ter sido estudada teoricamente.

Sempre que aplicável, será necessário:

- [ ] Implementar o ambiente ou recurso proposto.
- [ ] Validar seu funcionamento por meio de testes.
- [ ] Investigar e resolver pelo menos alguns problemas.
- [ ] Compreender as configurações realizadas.
- [ ] Documentar a implementação e os principais aprendizados.

O nível de profundidade será proporcional à complexidade de cada fase.

---

## Acompanhamento

O status das fases deverá ser atualizado conforme o avanço dos estudos e dos projetos práticos.

O roadmap é um planejamento vivo: poderá ser reorganizado, ampliado ou simplificado conforme os conhecimentos adquiridos, as tecnologias utilizadas e os objetivos profissionais.

**Status atual:** Fase 02 — Switching e VLANs em andamento.

*Última atualização: Novembro de 2026.*
