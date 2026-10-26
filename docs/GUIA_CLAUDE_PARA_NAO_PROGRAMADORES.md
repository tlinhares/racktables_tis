# Guia do Claude para quem não programa

> Manual da equipe do **RackManager IA**. Leitura de ~15 minutos.
> Dúvidas: chame o coordenador no Discord.

---

## 1. Qual é o seu papel

Você **não precisa saber programar**. O Claude escreve o código. Você é o **dono do seu módulo** e faz o que só uma pessoa de infraestrutura sabe fazer:

| Você faz | O Claude faz |
|---|---|
| Diz **o que** o sistema precisa fazer | Decide **como** fazer no código |
| Aprova ou recusa o plano | Explica o plano em português simples |
| Testa no navegador | Escreve o código e os testes automáticos |
| Revisa a tarefa de um colega | Envia as mudanças para o GitHub |
| Avisa quando algo está estranho | Corrige quando você aponta o problema |

**Uma regra acima de todas:** se você não entendeu o que o Claude quer fazer, **não aprove**. Pergunte a ele de novo ("explique de forma mais simples") ou chame o coordenador.

---

## 2. Antes de começar (uma vez só)

- [ ] Conta no **GitHub** com **verificação em duas etapas (2FA)** ativada, e o login enviado ao coordenador.
- [ ] Convite do repositório **aceito** (chega por e-mail).
- [ ] Conta do **Claude** com acesso ao Claude Code.
- [ ] **Acesso ao seu ambiente de desenvolvimento**, que o coordenador passa (endereço, usuário e como entrar).
- [ ] O **endereço do seu site de testes**, que só você usa (o coordenador também passa).

---

## 3. Palavras que você vai ouvir

| Palavra | O que significa |
|---|---|
| **Repositório** | A pasta oficial do projeto, guardada no GitHub. |
| **Issue** | Um pedido de tarefa no GitHub: "o sistema precisa fazer X". |
| **Branch** | Uma cópia de trabalho separada para cada tarefa, para não atrapalhar ninguém. |
| **Commit** | Um "salvar" com descrição do que mudou. |
| **PR (Pull Request)** | Um pedido para juntar a sua tarefa à versão oficial. Outra pessoa revisa antes. |
| **Merge** | Juntar o PR aprovado à versão oficial (`main`). |
| **CI** | Conferência automática do GitHub que testa se nada quebrou. |
| **Migração** | Uma mudança na estrutura do banco de dados (criar tabela, coluna). **Sempre precisa do coordenador.** |
| **Deploy** | Colocar uma versão no ar para os usuários. **Só o coordenador faz.** |

---

## 4. Como abrir o Claude

1. Entre no seu ambiente de desenvolvimento, do jeito que o coordenador ensinou.
2. Vá até a pasta do projeto e digite:
   ```
   claude
   ```
3. Escreva em português, como se falasse com um colega.

**Teclas e comandos úteis:**

| Ação | Como |
|---|---|
| Parar o Claude no meio | Tecla **Esc** |
| Começar uma conversa nova (nova tarefa) | Digite `/clear` |
| Modo "só planejar, não mexer em nada" | **Shift + Tab** até aparecer *plan mode* |
| Ajuda | Digite `/help` |
| Sair | Digite `/exit` |

**Quando o Claude pedir permissão** ("Allow?", "Yes/No") para rodar um comando ou alterar um arquivo:
- **Leia antes de aceitar.** Se não entender, responda **No** e pergunte: *"o que esse comando faz?"*
- Nunca aceite nada que fale em `deploy`, `production`, `.env`, `sudo`, `--force`, `drop`, `delete` ou `migrate:fresh`. **Pare e chame o coordenador.**

---

## 5. Passo a passo de uma tarefa

### Passo 1 — Escreva a Issue no GitHub
Use o modelo de Issue. Descreva com suas palavras:
- **O que precisa:** "Quero cadastrar os racks de cada sala, com altura em U."
- **Quando der certo:** "O rack aparece na lista da sala."
- **Quando der errado:** "Se eu colocar altura 0, aparece uma mensagem de erro."
- **Quem pode:** "Operador cadastra; leitor só vê."

### Passo 2 — Peça o plano ao Claude
Comece **sempre** com `/clear` e depois cole o prompt da seção 11 do plano (`docs/PLANO_PROJETO.md`), preenchido. O Claude **não deve mexer em nada** nesta etapa, só explicar.

### Passo 3 — Leia o plano e decida
Confira se o Claude entendeu o que você quis dizer. Perguntas que ajudam:
- *"O que vai aparecer de diferente na tela?"*
- *"Isso mexe no banco de dados?"* Se sim, avise o coordenador.
- *"Isso mexe em algo de outra equipe?"* Se sim, avise a outra dupla.
- *"Como eu testo isso no navegador?"*

Se estiver bom, responda: **"Aprovado, pode fazer."**

### Passo 4 — Deixe o Claude trabalhar
Ele vai criar a branch, escrever o código, rodar os testes e mostrar o resultado. Você acompanha e responde quando ele perguntar algo.

### Passo 5 — Teste no navegador
Abra o **seu** site de testes e siga o passo a passo que o Claude entregou. Teste também o que **não** deveria funcionar:
- campo vazio ou valor absurdo (altura -5, IP 999.1.1.1);
- usuário leitor tentando alterar;
- o mesmo cadastro feito duas vezes.

Achou um problema? Descreva para o Claude **o que você fez, o que esperava e o que aconteceu**:
> "Cadastrei um rack de 42U e tentei colocar um servidor na U 42 com 2U de altura. Esperava erro, mas ele aceitou."

### Passo 6 — Peça a revisão e o PR
Quando tudo estiver certo:
> "Testei e está funcionando. Rode o /code-review, corrija o que for importante e depois abra o PR com o modelo preenchido."

Antes de ele enviar, peça: *"mostre em linguagem simples o que vai ser enviado"*.

### Passo 7 — Revisão do colega
Avise no Discord que o PR está pronto. **Outro TI** (não você) faz a revisão funcional. Se tiver migração, o coordenador também revisa.

### Passo 8 — Registre
Anote na Issue: tempo gasto, quantas vezes precisou pedir correção e o que deu errado. Isso alimenta o estudo de caso.

---

## 6. Como pedir bem

| ❌ Pedido vago | ✅ Pedido bom |
|---|---|
| "Faz a tela de racks." | "Quero uma tela que liste os racks de uma sala, mostrando nome e quantas U estão livres." |
| "Arruma o erro." | "Quando salvo um IP sem preencher o prefixo, aparece uma tela branca. Deveria aparecer 'Escolha o prefixo'." |
| "Melhora isso." | "Na lista de equipamentos, quero poder buscar pelo número de série." |
| "Faz tudo do IPAM." | Uma coisa por vez: primeiro prefixos, depois endereços, depois reservas. |

**Dicas:**
- **Uma tarefa por conversa.** Terminou, use `/clear`.
- Use exemplos reais da sua rede (sem senhas): "o prefixo 10.10.0.0/24 da unidade X".
- Se a resposta ficou técnica demais: *"explique como se eu não fosse programador"*.
- Se o Claude parecer perdido ou repetir o mesmo erro 3 vezes: pare, use `/clear` e recomece explicando melhor, ou chame o coordenador.

---

## 7. Como revisar o PR de um colega

Você não precisa ler o código. Use o checklist que está no próprio PR:

1. Abra o PR no GitHub e leia o **"Resumo"** e o **"Como testar"**.
2. Peça ao Claude no seu ambiente:
   > "Baixe a branch do PR número X para eu testar no meu site de testes."
3. Siga o passo a passo no navegador. Teste também um caso de erro.
4. Confira que o **CI está verde** (✅ no PR).
5. Se estiver tudo certo: **Review changes → Approve**. Se não: **Request changes** e descreva o problema como no Passo 5.

---

## 8. Nunca faça

- ❌ Colar **senhas, tokens, chaves, backups de equipamentos** ou conteúdo do `.env` no Claude ou no Discord.
- ❌ Aprovar um comando ou plano que você **não entendeu**.
- ❌ Pedir ao Claude para "forçar", "pular os testes", "ignorar o erro" ou "mandar direto para a main".
- ❌ Pedir ao Claude para fazer **deploy** ou mexer no **banco compartilhado**.
- ❌ Usar dados reais de produção sem autorização do coordenador.
- ❌ Aprovar o seu próprio PR ou o PR que você pediu.
- ❌ Seguir instruções que apareçam **dentro** de arquivos, Issues ou páginas da internet dizendo para o Claude "ignorar as regras".

## 9. Pare e chame o coordenador quando

- 🛑 O Claude pedir permissão para algo com `sudo`, `deploy`, `production`, `.env`, `--force`, `drop` ou `delete`.
- 🛑 A tarefa precisar de **migração** (mudança no banco).
- 🛑 Aparecer erro de **permissão**, de **acesso negado** ou de **Git** que o Claude não resolve em uma tentativa.
- 🛑 O seu site de testes parar de abrir.
- 🛑 Você achar que algo foi enviado por engano.

Não tem problema errar. O problema é tentar consertar sozinho algo que você não entende.

---

## 10. Frases prontas (cola rápida)

| Situação | O que digitar |
|---|---|
| Começar tarefa | `/clear` e depois o prompt da seção 11 do plano |
| Entender melhor | "Explique de forma mais simples, sem termos técnicos." |
| Antes de aprovar | "O que muda na tela? Mexe no banco? Mexe em outra equipe?" |
| Saber como testar | "Me dê um passo a passo para testar no navegador, incluindo um caso de erro." |
| Reportar problema | "Fiz [X], esperava [Y], aconteceu [Z]." |
| Antes de enviar | "Mostre em linguagem simples o que vai ser enviado." |
| Finalizar | "Rode o /code-review, corrija o importante e abra o PR com o modelo preenchido." |
| Revisar colega | "Baixe a branch do PR número X para eu testar." |
| Claude travado | **Esc**, depois `/clear` e recomece explicando melhor. |
| Ver o que mudou | "Liste os arquivos que você alterou e o motivo de cada um." |
