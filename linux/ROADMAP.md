# ROADMAP — Laboratório Linux

Plano de aprendizado prático de administração Linux Server, parte do meu projeto de estudos de Infraestrutura, Redes e Cloud.

> **Filosofia:** Aprenda fazendo. Quebre. Investigue. Corrija. Entenda. Só depois automatize.

**Documentos relacionados:** `INSTRUCOES_CLAUDE.md` (regras do laboratório) · `PROGRESSO.md` (onde paramos)

---

## 1. Visão geral

### Status atual

| Item | Situação |
|---|---|
| Fase atual | **Fase 1 — Instalação e fundamentos** |
| Última sessão concluída | Sessão 1 — Preparação da VM (20/11/2026) |
| **Próxima atividade** | **Sessão 2 — Navegação no sistema de arquivos (`pwd`, `ls`, `cd`) e estrutura de diretórios do Linux** |

### Ambiente

| Item | Valor |
|---|---|
| Host | Linux, AMD Ryzen 7 5700X, 32 GB RAM |
| Virtualização | VirtualBox |
| Armazenamento do homelab | ~100 GB |
| VM atual | `UbuntuServerLab` — Ubuntu Server 26.04.1 LTS, 2 vCPU, 2 GB RAM, 20 GB de disco |
| Adaptador 1 (`enp0s3`) | NAT — acesso à internet (`10.0.2.15/24`) |
| Adaptador 2 (`enp0s8`) | Rede interna `LAB-CORE` — sem IPv4 até a Fase 3 |
| Snapshots | `instalacao-limpa` e `instalacao-limpa-2-adaptadores` |

### Regras de ouro do laboratório

- Trabalhar **dentro das VMs**. Não alterar o host sem necessidade.
- **Não modificar a `LAB-CORE`** sem discussão prévia e **não usar a rede física de casa** para testes de infraestrutura.
- **Snapshot antes de qualquer mudança importante**, e com a VM desligada sempre que possível.
- Uma etapa por vez: comando → resultado → análise.
- Uma atividade só está concluída com **evidência** (saída de comandos e testes), não apenas por ter executado os comandos.
- Erros são investigados antes de corrigidos.
- Não avançar de fase sem avaliar o aprendizado (ver critérios de cada fase).

### Método de troubleshooting (usado em todas as fases)

```
Sintoma → Coleta de evidências → Identificação da camada → Hipóteses → Teste → Conclusão → Correção
```

Camadas de referência: **física/virtual** (VM, adaptador, cabo virtual) → **camada 2** (interface, MAC, link) → **camada 3** (IP, rota, gateway) → **serviço** (processo, porta, firewall, logs).

> Lição da Sessão 1: se `ip -br link` não mostra a interface, o problema está **abaixo** do IP (VM, adaptador ou driver). O Adaptador 2 estava desabilitado no VirtualBox.

### Formato de cada sessão (25 a 40 minutos)

1. Objetivo
2. Explicação curta do conceito
3. Atividade prática guiada
4. Teste de funcionamento
5. Pequeno desafio
6. Revisão do aprendizado
7. Atualização do `PROGRESSO.md`

---

## 2. Mapa das fases

| Fase | Tema | Status |
|---|---|---|
| 1 | Instalação e fundamentos | 🟡 Em andamento |
| 2 | Administração do sistema | ⚪ Pendente |
| 3 | Redes no Linux | ⚪ Pendente |
| 4 | Serviços de infraestrutura | ⚪ Pendente |
| 5 | Segurança e automação | ⚪ Pendente |
| 6 | Integração com o homelab | ⚪ Pendente |

Legenda: ✅ concluída · 🟡 em andamento · ⚪ pendente

---

## Fase 1 — Instalação e fundamentos 🟡

**Objetivo:** ter um servidor Linux funcionando e conseguir se mover nele com segurança pelo terminal.

### Etapas

- [x] **1.1 Preparar e instalar a VM Ubuntu Server LTS** — *concluída em 20/11/2026*
  - Evidências: `hostnamectl` (Ubuntu 26.04.1 LTS), `df -h /` (20 GB), `ip -br a` e `ip -br link` (duas interfaces).
  - Troubleshooting resolvido: Adaptador 2 desabilitado no VirtualBox.
  - Snapshots criados.
- [ ] **1.2 Navegação no sistema de arquivos** ← **PRÓXIMA ATIVIDADE**
- [ ] **1.3 Estrutura de diretórios do Linux**
- [ ] **1.4 Manipulação de arquivos e diretórios**
- [ ] **1.5 Comandos de consulta e leitura de arquivos**
- [ ] **1.6 Uso do manual e da ajuda**
- [ ] **1.7 Revisão e mini-projeto da fase**

### Conceitos

- Terminal vs shell; prompt; caminho absoluto e relativo.
- Hierarquia do sistema de arquivos (FHS): `/`, `/etc`, `/var`, `/home`, `/usr`, `/tmp`, `/dev`, `/proc`.
- Tudo é arquivo; arquivos ocultos; extensões não definem tipo.
- Redirecionamento (`>`, `>>`) e pipe (`|`) de forma introdutória.

### Atividades práticas

| Etapa | Comandos | Para que serve |
|---|---|---|
| 1.2 | `pwd`, `ls`, `ls -la`, `cd`, `cd ..`, `cd -`, `cd ~` | Saber onde estou, listar e navegar |
| 1.3 | `ls /`, `tree` (se instalado), `file`, `stat` | Reconhecer o papel de cada diretório |
| 1.4 | `mkdir`, `touch`, `cp`, `mv`, `rm`, `rmdir` | Criar, copiar, mover e apagar (com cuidado) |
| 1.5 | `cat`, `less`, `head`, `tail`, `grep`, `wc`, `find` | Ler e procurar informações |
| 1.6 | `man`, `--help`, `type`, `which`, `apropos` | Aprender sozinho a usar um comando |

> ⚠️ **Cuidado com `rm`:** nunca usar `rm -rf` sem entender o caminho. Praticar apenas dentro de um diretório de estudo (ex.: `~/lab`). Snapshot antes de qualquer exercício com remoção.

### Desafios

- Descobrir, sem dica, em qual diretório ficam os arquivos de configuração do sistema e justificar.
- Criar uma estrutura `~/lab/{docs,scripts,logs}`, mover arquivos entre elas e provar com `ls -R`.
- Usar apenas `man` (sem internet) para descobrir uma opção nova do `ls`.
- Encontrar o maior arquivo dentro de `/var/log` usando `ls`/`find`.

### Critério para avançar

Consigo, sem ajuda: navegar com caminhos absolutos e relativos, explicar a função dos diretórios principais, criar/copiar/mover/apagar com segurança e achar informações com `man`, `grep` e `find`.

---

## Fase 2 — Administração do sistema ⚪

**Objetivo:** administrar usuários, permissões, pacotes, processos, serviços e logs, e monitorar a saúde do servidor.

### Etapas

- [ ] 2.1 Usuários e grupos
- [ ] 2.2 Permissões, proprietários e grupos
- [ ] 2.3 `sudo` e o princípio do menor privilégio
- [ ] 2.4 Gerenciamento de pacotes (`apt`)
- [ ] 2.5 Processos
- [ ] 2.6 Serviços e `systemd`
- [ ] 2.7 Inicialização do sistema
- [ ] 2.8 Logs com `journalctl`
- [ ] 2.9 Monitoramento de CPU, memória e disco
- [ ] 2.10 Revisão e mini-projeto da fase

### Conceitos

- UID/GID, `/etc/passwd`, `/etc/group`; usuário comum vs `root`.
- Permissões `rwx` em notação simbólica e octal; dono, grupo e outros.
- Repositórios, cache de pacotes, dependências, atualização vs atualização de versão.
- Processo, PID, sinais; serviço, unit e alvo (`target`) do `systemd`.
- Logs do sistema como fonte principal de diagnóstico.

### Atividades práticas

| Etapa | Comandos | Para que serve |
|---|---|---|
| 2.1 | `id`, `whoami`, `adduser`, `usermod`, `groups`, `passwd` | Gerenciar contas e grupos |
| 2.2 | `ls -l`, `chmod`, `chown`, `chgrp`, `umask` | Controlar quem acessa o quê |
| 2.4 | `apt update`, `apt upgrade`, `apt install`, `apt search`, `apt show`, `dpkg -l` | Instalar e manter software |
| 2.5 | `ps aux`, `top`, `htop`, `kill`, `pgrep` | Ver e controlar processos |
| 2.6 | `systemctl status/start/stop/enable/disable`, `systemctl list-units` | Controlar serviços |
| 2.8 | `journalctl`, `journalctl -u`, `-p err`, `--since`, `-f` | Investigar eventos |
| 2.9 | `free -h`, `df -h`, `du -sh`, `uptime`, `vmstat` | Medir consumo de recursos |

### Cenários reais de infraestrutura

- Criar contas para uma "equipe de suporte" e outra "equipe de desenvolvimento", com uma pasta compartilhada que só o grupo certo escreve.
- Um serviço não sobe após atualização: ler o `journalctl -u` e achar a causa.
- O disco encheu: descobrir com `du` quem consumiu o espaço.

### Quebre e investigue (laboratório de falhas)

> Sempre com snapshot antes.

- Tirar a permissão de um arquivo necessário e observar o erro (`Permission denied`) até achar a causa.
- Parar um serviço e identificar o impacto.
- Gerar uso alto de CPU de forma controlada e localizá-lo com `top`.

### Critério para avançar

Consigo criar usuários e grupos, definir permissões corretas para um cenário, instalar e remover pacotes entendendo dependências, ler logs de um serviço com falha e dizer onde está o gargalo de CPU, memória ou disco.

---

## Fase 3 — Redes no Linux ⚪

**Objetivo:** configurar e diagnosticar a rede do servidor, aproveitando a base de redes que já tenho (IP, VLANs, roteamento).

### Etapas

- [ ] 3.1 Interfaces de rede (revisitar `enp0s3` e `enp0s8`)
- [ ] 3.2 Endereçamento IPv4 e DHCP no Linux
- [ ] 3.3 IP estático com `netplan`
- [ ] 3.4 Rotas e gateway
- [ ] 3.5 DNS e resolução de nomes
- [ ] 3.6 Testes de conectividade (`ping`, `traceroute`)
- [ ] 3.7 Portas e conexões (`ss`)
- [ ] 3.8 Diagnóstico de conectividade por camadas
- [ ] 3.9 Firewall com UFW
- [ ] 3.10 Revisão e mini-projeto da fase

### Conceitos

- Diferença entre `ip link` (camada 2) e `ip addr` (camada 3).
- Endereço IP, máscara/CIDR, gateway, tabela de rotas.
- NAT do VirtualBox vs rede interna `LAB-CORE` (sem DHCP, sem saída para a internet).
- Resolução de nomes e `systemd-resolved`.
- Portas, protocolos TCP/UDP, estado `LISTEN`.
- Firewall com política padrão (negar entrada, permitir saída) e regras explícitas.
- IPv6 link-local e EUI-64 (**revisitar aqui**, no contexto de endereçamento).

### Atividades práticas

| Etapa | Comandos | Para que serve |
|---|---|---|
| 3.1 | `ip -br link`, `ip -br a`, `ip -s link` | Ver estado e estatísticas das interfaces |
| 3.3 | `netplan get`, `netplan try`, `netplan apply` | Configurar IP persistente com reversão segura |
| 3.4 | `ip route`, `ip route get` | Entender por onde o tráfego sai |
| 3.5 | `resolvectl status`, `dig`/`nslookup` | Verificar DNS |
| 3.6 | `ping`, `traceroute`/`tracepath` | Testar alcance e caminho |
| 3.7 | `ss -tulpn` | Ver portas abertas e processos |
| 3.9 | `ufw status verbose`, `ufw allow/deny`, `ufw enable` | Controlar tráfego de entrada |

### Laboratórios (dentro da `LAB-CORE`)

> A configuração da `enp0s8` na `LAB-CORE` será **discutida antes de ser feita**. Os testes exigem uma segunda VM, a ser criada nesta fase.

- Criar uma **segunda VM Linux** (clone da primeira ou instalação mínima) apenas para ter par de comunicação.
- Definir um endereçamento para a `LAB-CORE` (ex.: uma /24 reservada ao laboratório, a combinar) e configurar IPs estáticos nas duas VMs.
- Provar a comunicação: `ping` entre as VMs e `ip neigh` mostrando a tabela de vizinhos.
- Entender que a `enp0s3` (NAT) dá internet e a `enp0s8` (`LAB-CORE`) é só rede interna: **qual rota é usada para cada destino?**

### Quebre e investigue

- IP duplicado na mesma rede.
- Máscara errada em um dos lados.
- Gateway inexistente ou rota padrão apontando para a interface errada.
- DNS quebrado (ping por IP funciona, por nome não).
- Regra de firewall bloqueando o `ping`.

### Critério para avançar

Consigo configurar IP estático com segurança, explicar a tabela de rotas, diagnosticar "sem rede" separando física, camada 2, camada 3, DNS e firewall, e liberar/bloquear portas com UFW sem perder o acesso administrativo.

---

## Fase 4 — Serviços de infraestrutura ⚪

**Objetivo:** subir serviços comuns de ambientes corporativos, entendendo portas, processos, logs e acesso.

### Etapas

- [ ] 4.1 Conceito de serviço, porta e processo "escutando"
- [ ] 4.2 SSH e administração remota
- [ ] 4.3 Servidor web Nginx
- [ ] 4.4 Compartilhamento de arquivos
- [ ] 4.5 DNS (introdução)
- [ ] 4.6 DHCP (introdução)
- [ ] 4.7 Análise de logs e troubleshooting de serviços
- [ ] 4.8 Revisão e mini-projeto da fase

### Conceitos

- Cliente/servidor; porta de serviço; o que significa "escutar" em uma interface.
- SSH: acesso remoto, chaves públicas e privadas.
- Servidor web: arquivos de configuração, *server blocks*, logs de acesso e erro.
- Compartilhamento de arquivos: permissões do sistema vs permissões do compartilhamento. *(A ferramenta será definida na hora, conforme a necessidade do laboratório.)*
- DNS: resolução e tipos de registro básicos. DHCP: concessão de endereços e escopo.

### Atividades práticas

| Etapa | Foco | Evidência de conclusão |
|---|---|---|
| 4.2 | Acessar a VM via SSH a partir do host ou de outra VM | Login remoto funcionando e registrado em log |
| 4.3 | Instalar o Nginx e publicar uma página própria | Página acessada de outra máquina + `ss` mostrando a porta |
| 4.4 | Compartilhar uma pasta entre duas VMs | Arquivo criado em uma máquina e lido na outra |
| 4.5 | Resolver um nome interno do laboratório | Consulta respondendo pelo servidor do lab |
| 4.6 | Servidor DHCP na `LAB-CORE` (**discutir antes**, para não conflitar com a rede existente) | Segunda VM recebendo IP do servidor |

### Cenários reais

- "O site da empresa saiu do ar": percorrer o caminho do diagnóstico (serviço ativo? porta escutando? firewall? logs?).
- Novo funcionário precisa de acesso remoto seguro ao servidor.

### Quebre e investigue

- Erro de sintaxe na configuração do Nginx: ler a mensagem de teste e corrigir.
- Serviço rodando, mas inacessível por causa do firewall.
- Porta já em uso por outro processo.
- Permissão errada na pasta do site (erro 403).

### Critério para avançar

Consigo instalar, configurar, iniciar e testar um serviço de ponta a ponta, e diante de uma falha sei seguir a cadeia: processo → porta → firewall → permissões → logs.

---

## Fase 5 — Segurança e automação ⚪

**Objetivo:** proteger o servidor com boas práticas básicas e automatizar tarefas que já entendo manualmente.

### Etapas

- [ ] 5.1 Hardening básico
- [ ] 5.2 Atualizações e gerenciamento de segurança
- [ ] 5.3 Controle de acesso SSH
- [ ] 5.4 Auditoria de logins e tentativas de acesso
- [ ] 5.5 Bash básico: variáveis, condições, laços
- [ ] 5.6 Scripts administrativos
- [ ] 5.7 Agendamento com `cron`
- [ ] 5.8 Revisão e mini-projeto da fase

### Conceitos

- Superfície de ataque: o que não precisa rodar, não deve rodar.
- Menor privilégio; autenticação por chave; desabilitar login direto como root.
- Atualizações de segurança; janela de manutenção.
- Idempotência e segurança em scripts (validar antes de apagar, registrar o que foi feito).

### Atividades práticas

- Revisar serviços e portas abertas e remover o desnecessário (`ss`, `systemctl`, UFW).
- Configurar SSH por chave e restringir usuários permitidos. **Sempre manter uma sessão aberta e testar o acesso em outra antes de fechar a primeira.**
- Ativar atualizações de segurança automáticas e verificar o resultado.
- Ler `/var/log/auth.log`/`journalctl` e identificar tentativas de login falhas.
- Criar scripts, por exemplo:
  - relatório de saúde do servidor (uptime, disco, memória, serviços);
  - backup simples de uma pasta com data no nome;
  - rotina que alerta quando o disco passa de um limite.
- Agendar os scripts com `cron` e **provar** que rodaram, pelo log.

### Quebre e investigue

- Trancar o acesso SSH de propósito (em snapshot) e recuperar pelo console da VM.
- Script que apaga mais do que devia: entender por que validação importa.
- Tarefa de `cron` que não executa: variáveis de ambiente, caminhos e permissões.

### Critério para avançar

Consigo explicar cada medida de hardening aplicada e o motivo, tenho acesso SSH seguro e testado, e meus scripts são legíveis, seguros e agendados com evidência de execução.

---

## Fase 6 — Integração com o homelab ⚪

**Objetivo:** usar o conhecimento de Linux como peça do laboratório maior de redes e infraestrutura. Esta fase **conecta** os dois projetos; o planejamento de redes (segmentação, equipamentos físicos, etc.) continua em seu próprio roadmap.

### Etapas

- [ ] 6.1 Planejar o papel de cada VM Linux no laboratório
- [ ] 6.2 Integrar as VMs às redes virtuais do homelab
- [ ] 6.3 Firewall e segmentação (com pfSense, quando essa etapa do homelab chegar)
- [ ] 6.4 Serviços Linux consumidos por outras VMs
- [ ] 6.5 Backup, snapshots e recuperação
- [ ] 6.6 Documentação da infraestrutura funcional

### Conceitos

- Cada VM com uma função clara (servidor de serviços, cliente de teste, etc.).
- Segmentação: máquinas em redes diferentes e o firewall decidindo o que passa.
- Dependências entre serviços (DNS e DHCP sustentam o resto).

### Atividades práticas

- Mapear a topologia final em um diagrama e documentar IPs, portas e funções.
- Colocar o servidor Linux atrás do firewall do homelab e liberar apenas o necessário.
- Fazer outra VM consumir um serviço do servidor Linux (web, DNS ou arquivos) atravessando o firewall.
- Executar um **exercício de recuperação**: restaurar um serviço a partir de snapshot e de backup, medindo o tempo.

### Entregável final

Um repositório com a documentação da infraestrutura: diagrama, tabela de endereçamento, serviços ativos, procedimentos de backup e recuperação e um *runbook* de troubleshooting por camadas.

### Critério de conclusão

Consigo reconstruir o ambiente a partir da documentação e diagnosticar uma falha induzida em outra pessoa de forma metódica.

---

## 3. Próximos passos imediatos

1. **Sessão 2 (próxima):** estrutura de diretórios e navegação (`pwd`, `ls`, `cd`) — Etapas 1.2 e 1.3.
2. **Sessão 3:** criar, copiar, mover e apagar com segurança (`mkdir`, `touch`, `cp`, `mv`, `rm`).
3. **Sessão 4:** ler e procurar (`cat`, `less`, `grep`, `find`) e usar o `man`.
4. **Sessão 5:** revisão e mini-projeto da Fase 1, com avaliação para liberar a Fase 2.

---

## 4. Pontos fora do plano principal (decisões em aberto)

- **EUI-64 / IPv6 link-local:** estudo pausado na Sessão 1 por decisão minha. Será retomado na Fase 3 (endereçamento), não bloqueia nada antes.
- **Endereçamento da `LAB-CORE`:** a ser definido em conjunto antes da Fase 3.
- **Ferramenta de compartilhamento de arquivos (Fase 4):** a definir conforme o laboratório.

---

## 5. Registro de revisões do roadmap

| Data | Alteração |
|---|---|
| 20/11/2026 | Criação do roadmap. Etapa 1.1 (instalação da VM) marcada como concluída. |
