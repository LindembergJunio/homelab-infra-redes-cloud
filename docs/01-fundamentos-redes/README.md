# Fase 1 - Fundamentos de Redes (OSI, TCP/IP, Endereçamento)

## Objetivo
Entender redes na  prática: como dois hosts se enxergam, o que é um endereço IP, máscara de sub-rede, como ler isso no tráfego real. Como calcular sub-redes.

## VMs desta fase
Foi reaproveitada a VM criada anteriormente, aprendi na prática como clonar. Ambas configuradas como Rede Interna para comunicação apenas entre elas.

| VM | RAM | CPU | Disco | Rede | Função |
|---|---|---|---|---|---|
| NET-A | 1 GB | 1 vCPU | 8 GB | LAB-CORE(IP estático) | Host de teste |
| NET-B | 1 GB | 1 vCPU | 8 GB | LAB-CORE(IP estático) | Host de teste |

## Subnetting calculado
No exercicio, foi solicitado calcular três subredes derivadas da rede principal 10.0.0.0/24.Sendo:
- Para 4 hosts. Somando com mais 2 (Rede e Broadcast), foi definido uma rede /29 para comportar 8 hosts. 10.0.0.8/29 com mascára 255.255.255.248
- Para 30 hosts. Somando com mais 2 (Rede e Broadcast), foi definido uma rede /27 para comportar 32 hosts. 10.0.0.32/27 com mascára 255.255.255.224
- Para 100 hosts. Somando com mais 2 (Rede e Broadcast), foi definido uma rede /25 para comportar 128 hosts. 10.0.0.128/25 com mascára 255.255.255.128

## Implementação
Após definido os IPs e máscaras, foi configurado o IP de cada uma das máquinas: 
- NET-A - 10.0.0.11 máscara 255.255.255.0
- NET-B - 10.0.0.12 máscara 255.255.255.0

Logo após fiz os testes de comunicação via PING para capturar os pacotes e entender o processo.

## Análise da captura de pacotes (Wireshark)
Foi gerado o arquivo com a captura dos pacotes e depois aberto ele com o Wireshark. Pude verificar o tamanho dos pacotes, os MACs de origem e destino, bem como o IP de origem e destino. Também observei o protocolo ARP em funcionamento, buscando o proprietário do IP na rede. 

## Problemas encontrados e soluções

### Problema 1 - VMS isoladas da rede. 
- Para instalar pacotes no Linux(Debian) foi preciso adicionar um adaptador temporário em NAT, tentei do jeito mais fácil apenas adicionando o adaptador e ligando a VM, porém não funcionou. Após uma pesquisa, foi preciso editar o arquivo de interface de rede via linha de comando (sudo nano /etc/network/interfaces) e adicionar o adaptador, assim consegui comunicação com a rede.

### Problema 2 - Erro na instalação dos pacotes (padrão usando CDROM mas não tinha midia).
- Após conseguir comunicação com a rede, o repositório estava com problema, foi preciso editar o arquivo de fontes do apt (sudo nano /etc/apt/sources.list) e adicionar o link de novos repositórios.

### Problema 3 - Erro para compartilhar arquivo da VM para o Host.
- Depois de gerado a captura do pacote para analisar no wireshark, não estava conseguindo criar uma pasta compartilhada na VM para pegar o arquivo. Com uma breve pesquisa encontrei outra solução criando um Servidor HTTP temporário usando a porta 8080, onde bastou acessar o IP da VM no navegador e baixar o arquivo.

## Exercícios de troubleshooting

- Derrubar a interface de NET-A e tentar pingar nela pela NET-B. Foi verificado o erro ***Destination Host Unreachable*** que indica que o protocolo ARP tentou encontrat NET-A, mas como estava com a interface down, ninguém respondeu, gerando o erro.
- Com a NET-A Down, tentar pigar para a NET-B. Foi gerado o erro ***Rede fora de alcance*** que indica que o pacote nem saiu de NET-A pois não sabe para onde ir já que não encontrou nenhuma interface ativa.
- A diferença principal é que no "Destination Host Unreachable" o pacote chegou a sair da máquina de origem, enquanto no "Network unreachable" ele nem saiu — a própria máquina identificou que não tinha caminho disponível

## Aprendizados

- Como calcular rede de acordo com a quantidade de hosts.
- Como é o processo de clonar uma VM.
- Como analisar pacotes no wireshark.
- Nem tudo dá certo na primeira tentativa, os erros que ocorreram mostraram bem isso.
