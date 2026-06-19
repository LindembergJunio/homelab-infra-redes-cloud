# Fase 0 — Preparação do Ambiente

## Objetivo
Configurar o ambiente de virtualização (VirtualBox) e validar que a rede de laboratório está corretamente isolada antes de iniciar a construção do homelab.

## Ambiente do host
- CPU: AMD Ryzen 7 5700X
- RAM: 32 GB
- Armazenamento reservado para o lab: ~100 GB (SSD)
- Hypervisor: Oracle VirtualBox

## Decisões tomadas

### Rede: Internal Network (LAB-CORE)
Optei por usar uma **Internal Network** chamada `LAB-CORE`, em vez de Bridged ou NAT, porque:
- Bridged conectaria as VMs diretamente à minha rede doméstica real, o que não é desejado em um ambiente de laboratório.
- Internal Network garante isolamento total: as VMs só se comunicam entre si, sem acesso à internet ou à rede do host, salvo configuração explícita (que será feita a partir da Fase 3, com o pfSense).

## VM criada: TEST-VM01

| Especificação | Valor |
|---|---|
| Sistema | Debian 13 |
| RAM | 1024 MB |
| CPU | 1 vCPU |
| Disco | 20 GB (dinamicamente alocado) |
| Rede | Internal Network (LAB-CORE) |
| IP configurado | 192.168.0.10/24 (manual, sem DHCP) |
| Hostname | test-vm01 |

## Validação de isolamento de rede

Após a instalação, foram realizados testes para confirmar que a rede `LAB-CORE` está isolada como esperado:

| Teste | Comando | Resultado |
|---|---|---|
| Acesso à internet | `ping -c 4 8.8.8.8` | Destination Host Unreachable |
| Acesso ao host físico | `ping -c 4 192.168.0.1` | Destination Host Unreachable |

**Conclusão:** a rede está isolada com sucesso. A VM não possui rota para a internet nem para a rede do computador host, comportamento esperado de uma Internal Network do VirtualBox.

## Snapshot

Foi criado o snapshot `pos-instalacao-limpa` imediatamente após a instalação do sistema e validação de rede, antes de qualquer configuração adicional. O processo de criação/restauração do snapshot foi testado manualmente (criação de um arquivo de teste, restauração do snapshot, confirmação de que o arquivo não persistiu).

## Aprendizados desta fase

- Diferença entre os modos de rede do VirtualBox (NAT, Bridged, Internal Network, Host-only).
- Snapshot não é backup: ele depende da existência da VM e é perdido se ela for excluída. Para arquivamento de longo prazo, o correto é exportar a VM como appliance (`.ova`).
- Convenção de nomenclatura técnica (hostname, nomes de VM/snapshot): minúsculo, sem acento, sem espaço.
