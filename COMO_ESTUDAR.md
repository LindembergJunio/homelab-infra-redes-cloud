# Como Estudar — Filosofia e Rotina do Homelab

## 1. Filosofia de aprendizado

> **Faça na mão primeiro. Quebre. Conserte. Entenda. Só depois automatize.**

O objetivo do laboratório é desenvolver conhecimentos práticos em infraestrutura, redes e cloud.

A prioridade não é avançar rapidamente pelas fases, mas compreender o funcionamento das tecnologias, implementar soluções e desenvolver capacidade de troubleshooting.

O laboratório deve acompanhar a rotina de estudos, não competir com a faculdade ou comprometer os períodos de descanso.

---

## 2. Organização do tempo

O homelab é desenvolvido em paralelo à graduação em Tecnologia de Redes de Computadores e às demais responsabilidades da rotina.

Por isso, não existe obrigação de estudar todos os dias.

### Rotina semanal sugerida

| Período | Atividade | Tempo |
|---|---|---|
| 2 dias durante a semana | Implementação prática no laboratório | 60–90 min |
| 1 dia durante a semana | Teoria, revisão ou troubleshooting | 30–60 min |
| Sábado | Reserva para pendências ou atividades adicionais | Opcional |
| Domingo | Descanso | Livre |

Os dias podem ser ajustados conforme a carga de atividades da faculdade e os compromissos pessoais.

### Prioridade dos estudos

1. **Faculdade:** provas, trabalhos, PTIs e atividades com prazo.
2. **Homelab:** continuidade dos projetos práticos de infraestrutura e redes.
3. **Estudos complementares:** livros, cursos e aprofundamento em tecnologias relacionadas.

Durante semanas de avaliações ou entregas importantes, o ritmo do homelab poderá ser reduzido.

Não é necessário compensar todas as horas posteriormente.

### Regra de continuidade

- Duas sessões produtivas na semana já representam um bom avanço.
- Uma semana mais tranquila pode permitir atividades adicionais.
- Uma semana mais ocupada pode ter apenas uma sessão.
- Pausas não significam abandonar o projeto.

**A consistência deve ser medida pela evolução ao longo dos meses, não pela quantidade de dias estudados.**

---

## 3. Como estudar teoria

A teoria deve preparar para a prática, e não se tornar uma atividade interminável.

- Estude o necessário para compreender o que será implementado.
- Procure entender por que determinada configuração é utilizada.
- Refaça exemplos e comandos em seu próprio ambiente.
- Anote dúvidas que possam ser investigadas durante a implementação.
- Consulte documentação oficial quando necessário.

Evite consumir muitos tutoriais sobre o mesmo assunto sem colocar o conhecimento em prática.

O objetivo é conseguir implementar e explicar o funcionamento da tecnologia estudada.

---

## 4. Como desenvolver os projetos

O aprendizado será organizado por projetos práticos, que poderão crescer conforme novas tecnologias forem estudadas.

Exemplo: projeto de rede segmentada por VLANs.

1. Planejar a topologia.
2. Montar o ambiente no Packet Tracer.
3. Configurar os dispositivos.
4. Validar a comunicação entre as redes.
5. Simular problemas e investigar as causas.
6. Documentar a implementação e os resultados.

Cada etapa deve aproveitar os conhecimentos anteriores.

Não é necessário concluir todo o projeto em uma única semana. Ele poderá ser desenvolvido em várias sessões.

---

## 5. Como documentar

A documentação deve ser produzida durante o desenvolvimento dos projetos, sem transformar cada sessão em uma obrigação de escrever relatórios extensos.

O GitHub tem três objetivos:

1. **Portfólio:** demonstrar conhecimentos e projetos desenvolvidos.
2. **Referência:** registrar configurações e procedimentos para consultas futuras.
3. **Aprendizado:** consolidar o conhecimento explicando o que foi implementado.

### O que registrar

- O que foi implementado e por quê.
- Tecnologias e configurações utilizadas.
- Testes realizados e resultados obtidos.
- Problemas encontrados e como foram investigados.
- Decisões técnicas importantes.

### O que evitar

- Copiar tutoriais sem compreender.
- Documentar informações que não foram validadas.
- Repetir explicações teóricas em vários arquivos.
- Criar documentação extensa sem necessidade.
- Registrar senhas, tokens, chaves ou outras informações sensíveis.

A documentação deve ser suficiente para que outra pessoa compreenda o projeto e consiga reproduzir os principais procedimentos.

---

## 6. Como utilizar o Git e o GitHub

O Git será utilizado para acompanhar a evolução do laboratório.

Boas práticas:

- Realizar commits após alterações relevantes.
- Utilizar mensagens curtas e descritivas.
- Separar alterações de assuntos diferentes quando possível.
- Manter o README e o roadmap atualizados.
- Nunca enviar credenciais ou informações sensíveis.
- Revisar os arquivos antes de publicar alterações.

Exemplos de mensagens:

```text
Adiciona configuração de VLANs no Packet Tracer
Documenta implementação de trunk 802.1Q
Atualiza topologia da rede virtual
Documenta testes de conectividade entre VLANs
Corrige informações sobre endereçamento IP
```

Não é necessário realizar um commit em toda sessão. O importante é manter um histórico organizado das alterações efetivamente realizadas.

---

## 7. Como fazer troubleshooting

Quando algo não funcionar, utilizar uma sequência estruturada de investigação.

1. **Identificar o sintoma:** qual comportamento foi observado?
2. **Verificar alterações recentes:** o que mudou antes do problema?
3. **Formular hipóteses:** quais causas podem explicar o comportamento?
4. **Isolar variáveis:** testar uma hipótese por vez.
5. **Investigar por camadas:** verificar conectividade, endereçamento, roteamento, portas e aplicação conforme o problema.
6. **Consultar logs:** procurar evidências que ajudem a identificar a causa.
7. **Validar a solução:** repetir os testes após a correção.
8. **Registrar o aprendizado:** documentar a causa raiz e como o problema foi resolvido.

Evite alterar várias configurações simultaneamente sem saber qual delas está relacionada ao problema.

O objetivo é desenvolver raciocínio técnico, não apenas encontrar comandos que façam o ambiente funcionar.

---

## 8. Gestão do laboratório e das máquinas virtuais

Alguns cuidados para preservar o ambiente:

- Criar snapshots antes de alterações importantes.
- Identificar e documentar as configurações relevantes das VMs.
- Manter o inventário de máquinas, endereços IP e redes atualizado.
- Desligar máquinas virtuais que não estão sendo utilizadas.
- Verificar o espaço disponível antes de criar snapshots ou exportações.
- Manter backups dos dados importantes.

Snapshots ajudam a retornar a estados anteriores, mas não substituem backups.

Antes de excluir uma VM, verificar se existem dados ou configurações importantes que precisam ser preservados.

---

## 9. Critérios para concluir uma fase

Uma fase não será considerada concluída apenas por ter sido estudada teoricamente.

Sempre que aplicável, verificar:

- [ ] O ambiente ou recurso foi implementado.
- [ ] Os testes de funcionamento foram realizados.
- [ ] Consigo explicar as principais configurações.
- [ ] Consegui investigar e resolver problemas.
- [ ] A documentação apresenta o que foi desenvolvido.
- [ ] Os principais objetivos da fase foram alcançados.

Não é necessário dominar completamente uma tecnologia para avançar. O importante é possuir uma base prática consistente e saber identificar o que ainda precisa ser aprofundado.

---

## 10. Orientação geral

O homelab é um projeto de longo prazo.

Algumas fases serão mais rápidas, enquanto outras exigirão semanas de implementação e troubleshooting.

A evolução não deve ser medida pela quantidade de tecnologias estudadas, mas pela capacidade de construir, administrar, investigar e compreender ambientes de infraestrutura.

**Estudar com consistência, respeitando o tempo disponível, é mais importante do que tentar cumprir uma rotina impossível.
