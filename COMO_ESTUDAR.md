# Como Estudar — Filosofia e Rotina do Homelab

## A regra mais importante

> **Faça na mão primeiro. Quebre. Conserte. Entenda. Só depois automatize.**

Nenhuma ferramenta de automação substitui entender o que está acontecendo por baixo. Se você não sabe fazer manualmente, não sabe depurar quando o script falha.

---

## Rotina diária (~1h/dia)

| Dia | Foco |
|---|---|
| Segunda | Teoria do tópico da semana (vídeo/leitura, 20-30 min) + anotações |
| Terça | Implementação prática no lab |
| Quarta | Implementação prática (continuação) |
| Quinta | Exercício de troubleshooting |
| Sexta | Documentação (README, diagrama, commit) |
| Sábado | Buffer — imprevistos ou adiantamento |
| Domingo | Revisão leve ou descanso |

**Regra de ouro:** se uma fase prevista para 2 semanas levar 3, não tem problema.
Profundidade importa mais que velocidade.

---

## Como estudar teoria

- Assista o suficiente para entender **o que vai fazer e por quê** — não para "dominar o assunto"
- Pause o vídeo e refaça os exemplos na mão
- Anote dúvidas para resolver na prática, não antes
- O entendimento real vem da prática, não da leitura

---

## Como documentar

Documente **enquanto faz**, não depois. A documentação tem três funções:

1. **Portfólio** — recrutadores vão ler isso
2. **Referência futura** — você mesmo vai consultar quando esquecer
3. **Consolidação** — explicar por escrito força você a entender de verdade

### O que sempre documentar
- O que você fez e por quê (não só o comando, mas a decisão)
- O que não funcionou e como resolveu
- O que aprendeu que não estava no tutorial

### O que nunca fazer
- Copiar e colar tutorial sem entender
- Documentar só o que funcionou (os erros são a parte mais valiosa)
- Commitar tudo de uma vez no final da fase

---

## Como usar o Git no dia a dia

- **Commit ao fim de cada sessão de estudo** — mesmo que seja só documentação
- **Mensagem descritiva** sempre: `Configura IP estático na NET-A e valida conectividade`
- **Nunca commitar credenciais, senhas ou chaves** — use `.gitignore`
- **Commit frequente** prova que o projeto foi feito ao longo do tempo, não numa noite

---

## Como fazer troubleshooting

Quando algo não funciona, siga sempre essa ordem:

1. **Qual é o sintoma exato?** (mensagem de erro, comportamento observado)
2. **O que mudou antes do problema aparecer?**
3. **Isole a variável** — teste uma coisa de cada vez
4. **Verifique camada por camada** (física → rede → transporte → aplicação)
5. **Leia os logs** — o sistema sempre deixa rastro
6. **Documente a causa raiz**, não só a solução

---

## Como saber que realmente concluiu uma fase

Não é "li sobre o assunto". É:

- [ ] Implementei e está funcionando
- [ ] Quebrei de propósito e consertei
- [ ] Sei explicar o que fiz e por quê, sem consultar nada
- [ ] Documentei no GitHub com diagrama e problemas encontrados
- [ ] Completei o checklist da fase

---

## Gestão das VMs

- **Snapshot** após cada configuração funcional importante
- **Nunca delete** uma VM sem exportar `.ova` antes
- **Mantenha o inventário** de IPs atualizado em `docs/00-virtualizacao/topologia.md`
- **Desligue VMs** que não está usando — economiza RAM e prolonga o SSD

---

## Mensagem para o futuro você

Você vai travar. Vai ter dias que nada funciona. Isso é normal e é exatamente onde o aprendizado real acontece.

A diferença entre quem consegue a vaga e quem não consegue não é talento — é consistência. Uma hora por dia, todo dia, por 18-24 meses, constrói uma base que nenhuma certificação isolada substitui.

Cada problema que você resolve sozinho é uma história que você conta em entrevista. Cada incident report que você documenta é prova de que você pensa como profissional, não como estudante.

Continue.
